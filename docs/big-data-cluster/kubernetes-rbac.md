---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: This article describes how SQL Server Big Data Clusters uses RBAC with Kubernetes.
author: mihaelablendea 
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
---

# Kubernetes RBAC model & impact on users managing BDC

This following section describes the permissions required for the users managing big data clusters.

> [!NOTE]
> For additional resources on Kubernetes RBAC model see [Using RBAC Authorization - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) and [Using RBAC to define and apply permissions - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

## Role required for deployment

BDC uses service accounts (such as `sa-mssql-controller` or `master`) to orchestrate the provisioning of the cluster pods, services, high availability, monitoring, etc. When BDC deployment starts (for example, `azdata bdc create`), `azdata` does the following following:

1. Checks if provided namespace exists.
2. If it does not exist, it creates one and applies the `MSSQL_CLUSTER` label.
3. Creates the `sa-mssql-controller` service account.
4. Creates a `<namespaced>-admin` role with full permissions on the namespace or project but not cluster level permissions.
5. Creates a role assignment of that service account to the role.

Once these steps complete, the control plane pods are provisioned and the service account deploys the rest of big data cluster.  

Consequentially, the deploying user must have permissions to:

- List the namespaces in the cluster (1).
- Patch the new or existing namespace with the label (2).
- Create the service account `sa-mssql-controller`, the `<namespaced>-admin` role and the role binding (3-5).

The default `admin` role does not have these permissions, so the user deploying the big data cluster must have at least namespace level admin permissions.

## Cluster role required for pods and nodes metrics collection

Starting with SQL Server 2019 CU5, Telegraf requires a service account with cluster wide role permissions to collect the pod and node metrics. During the deployment (or upgrade for existing deployments), we attempt to create the necessary service account and cluster role, but if the user deploying the cluster or performing the upgrade does not have sufficient permissions, deployment or upgrade will still proceed with a warning and succeed. In this case, the pod & node metrics will not be collected. The user deploying the cluster must ask a cluster administrator to create the role and service account (either before or after the deployment or upgrade). After they are created, BDC uses them. 

Here is a script that shows how to create the required artifacts:
​
```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

The service account, cluster role and the cluster role binding can be created either before or post BDC deployment. Kubernetes automatically updates the permission for the Telegraf service account. If these are created as a pod deployment, you will see a few minutes delay in the pod and node metrics being collected.

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

​> [!NOTE]
> The service account, cluster role and the cluster role binding can be created either before or post BDC deployment. Kubernetes will automatically update the permission for the Telegraf service account. If these are created pod deployment, you will see a few minutes delay in the pod and node metrics being collected.

> [!NOTE]
> SQL Server 2019 CU5 introduces two feature switches to control the collection of pod and node metrics. By default these parameters are set to true in all environment targets, except OpenShift where the default is overridden. 

You can customize the these settings in  the security section in the `control.json` deployment configuration file:

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

If these settings are set to `false`, BDC deployemnt workflow will not attempt to create the service account, cluster role, and the binding for Telegraf.
