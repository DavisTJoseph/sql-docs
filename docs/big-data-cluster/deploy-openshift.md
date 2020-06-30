---
title: Deploy on OpenShift
titleSuffix: SQL Server Big Data Cluster
description: Learn how to upgrade SQL Server Big Data Clusters on OpenShift .
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
---

# Deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on OpenShift on-premises and Azure Red Hat OpenShift

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

This article explains how to deploy a SQL Server Big Data Cluster (BDC) on OpenShift environments, on-premises or on Azure Red Hat OpenShift (ARO).

> [!TIP]
> For a quick way to bootstrap a sample environment using ARO and then BDC deployed on this platform, you can use the Python script available [here](quickstart-big-data-cluster-deploy-aro.md).


SQL Server 2019 CU5 introduces support for SQL Server Big Data Clusters on OpenShift. You can deploy big data clusters to on-premises OpenShift or on Azure Red Hat OpenShift (ARO). Deployment requires OpenShift cluster version minimum 4.3. While the deployment workflow is similar to deploying in other Kubernetes based platforms ([kubeadm](deploy-with-kubeadm.md) and [AKS](deploy-on-aks.md)), there are some differences. The difference is mainly in relation to running applications as non-root user and the security context used for the namespace BDC is deployed in.

For deploying the OpenShift cluster on-premises see the [Red Hat OpenShift documentation](https://docs.openshift.com/container-platform/4.3/release_notes/ocp-4-3-release-notes.html#ocp-4-3-installation-and-upgrade). For ARO deployments see the [Azure Red Hat OpenShift](/azure/openshift/intro-openshift).

This article outlines deployment steps that are specific to the OpenShift platform, points out options you have for accessing the target environment and the namespace you are using to deploy the big data cluster.

## Pre-requisites

> [!IMPORTANT]
> Below pre-requisites must be performed by a OpenShift cluster admin (cluster-admin cluster role) that has sufficient permissions to create these cluster level objects. For more information on cluster roles in OpenShift see [Using RBAC to define and apply permissions](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

1. Create a custom security context constraint (SCC) using the attached [`bdc-scc.yaml`](#bdc-sccyaml-file).

   ```console
   oc apply -f bdc-scc.yaml
   ```

   > [!NOTE]
   > The custom SCC for BDC is based on the built-in *nonroot* SCC in OpenShift, with additional permissions. To learn more about security context constraints in OpenShift see [Managing Security Context Constraints](https://docs.openshift.com/container-platform/4.3/authentication/managing-security-context-constraints.html). For a detailed information on what additional permissions are required for big data clusters on top of the *nonroot* SCC, download the whitepaper [here](https://aka.ms/sql-bdc-openshift-security).

2. Create a namespace/project:

   ```console
   oc new-project <namespaceName>
   ```

3. Assign the custom SCC to the service accounts for users within the namespace where BDC is deployed:

   ```console
   oc adm policy add-scc-to-group bdc-scc system:serviceaccounts:<namespaceName>
   ```

4. Assign appropriate permission to the user deploying BDC. Do one of the following. 

   1. If the user deploying BDC has cluster-admin role, proceed to [deploy big data cluster](#deploy-big-data-cluster).

   1. If the user deploying BDC is a namespace admin, assign the user cluster-admin local role for the namespace created. This is the preferred option for the user deploying and managing the big data cluster to have namespace level admin permissions.

   ```console
   oc adm policy add-role-to-user cluster-admin <deployingUser> -n <namespaceName>
   ```

   The user deploying big data cluster must then log in to the OpenShift console:

   ```console
   oc login -u <deployingUser> -p <password>
   ```

## Deploy big data cluster

1. Install latest [azdata](deploy-install-azdata.md).

2. Clone one of the built-in configuration files for OpenShift.

    1. If your target environment is OpenShift.
    2. Clone one of the built-in configuration files for OpenShift, depending on your target environment (OpenShift on premises or ARO) and deployment scenario. See this section [link](//TODO add link) on settings that are specific to OpenShift in the built-in configuration files. For more details on available configuration files see [deployment guidance](deployment-guidance.md).

   List all the available built-in configuration files.

   ```console
   azdata bdc config list
   ```

   To clone one of the built-in configuration files, run below command (optionally, you can replace the profile based on your targeted platform/scenario):

   ```console
   azdata bdc config init --source openshift-dev-test --target custom-openshift
   ```

   For a deployment on ARO, we recommend to start with one of the *aro-* profiles, that includes default values for *serviceType* and *storageClass* appropriate for this environment. For example:

   ```console
   azdata bdc config init --source aro-dev-test --target custom-openshift
   ```

3. Customize the configuration files control.json and bdc.json. Here are some additional resources that guide you through the customizations supported for various use cases:

   1. [Storage](concept-data-persistence.md)
   1. [AD related settings](deploy-active-directory.md)
   1. [Other customizations](deployment-custom-configuration.md)

   > [!NOTE]
   > Integrating with Azure Active Directory for BDC is not supported, hence you can not use this authentication method when deploying on ARO.

4. Set [environment variables](deployment-guidance.md#env)

5. Deploy big data cluster

   ```console
   azdata bdc create --config custom-openshift --accept-eula yes
   ```

6. Upon successful deployment, you can log in and list the external cluster endpoints:

```console
   azdata login -n mssql-cluster
   azdata bdc endpoint list
```

## OpenShift specific settings in the deployment configuration files

SQL Server 2019 CU5 introduces two feature switches to control the collection of pod and node metrics. These parameters  are set to *false*  by default in the built-in profiles for OpenShift since the monitoring containers require [privileged security context](https://www.openshift.com/blog/managing-sccs-in-openshift), which will relax some of the secuirty constraints for the namespace BDC is deployed on.

```json
    "security": {
      "allowNodeMetricsCollection": false,
      "allowPodMetricsCollection": false
}
```

The name of the default storage class in ARO is managed-premium (as opposed to AKS where the default storage class is called default). You would find this in the `control.json` corresponding to `aro-dev-test` and `aro-dev-test-ha`:

```json
    },
    "storage": {
      "data": {
        "className": "default",
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "className": "managed-premium",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
      }
```

## `bdc-scc.yaml` file

```yaml
apiVersion: security.openshift.io/v1
kind: SecurityContextConstraints
metadata:
  annotations:
    kubernetes.io/description: SQL Server BDC Nonroot scc is based on 'nonroot' scc plus additional capabilities.
  generation: 2
  name: bdc-scc
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: true
allowPrivilegedContainer: false
allowedCapabilities:
- SETUID
- SETGID
- CHOWN
- SYS_PTRACE
defaultAddCapabilities: null
fsGroup:
  type: RunAsAny
readOnlyRootFilesystem: false
requiredDropCapabilities:
- KILL
- MKNOD
runAsUser:
  type: MustRunAsNonRoot
seLinuxContext:
  type:MustRunAs
supplementalGroups:
  type:RunAsAny
volumes:
- configMap
- downwardAPI
- emptyDir
- persistentVolumeClaim
- projected
- secret
```

## Next steps

[Tutorial: Load sample data into a SQL Server big data cluster](tutorial-load-sample-data.md)
