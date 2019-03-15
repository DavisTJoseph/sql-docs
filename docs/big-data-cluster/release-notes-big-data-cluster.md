---
title: Release notes
titleSuffix: SQL Server 2019 big data clusters
description: This article describes the latest updates and known issues for SQL Server 2019 big data clusters (preview). 
author: rothja 
ms.author: jroth 
manager: craigg
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
---
# Release notes for big data clusters on SQL Server

This article lists the updates and know issues for the most recent releases of SQL Server big data clusters.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp23"></a> CTP 2.3 (SQL 2019)

February 2019 &nbsp; &nbsp; / &nbsp; &nbsp; SQL Server 2019 &nbsp; &nbsp; / &nbsp; &nbsp; CTP2.3

### New features

| New feature | Details |
| :---------- | :------ |
| [Submit Spark jobs on SQL Server Big Data Clusters in IntelliJ](spark-submit-job-intellij-tool-plugin.md). | &nbsp; |
| [Common CLI for application deployment and cluster management](big-data-cluster-create-apps.md). | &nbsp; |
| [VS Code extension to deploy applications to SQL Server big data clusters](app-deployment-extension.md). | &nbsp; |
| [Changes to the **mssqlctl** tool command usage](#mssqlctlctp23). | &nbsp; |
| [Use Sparklyr in SQL Server 2019 Big data cluster](sparklyr-from-RStudio.md). | &nbsp; |
| Mount external HDFS-compatible storage into big data cluster with **HDFS tiering**. | See [HDFS tiering](hdfs-tiering.md). |
| New unified connection experience for the SQL Server master instance and the HDFS/Spark Gateway. | See [SQL Server master instance and the HDFS/Spark Gateway](connect-to-big-data-cluster.md). |
| Deleting a cluster with **mssqlctl cluster delete** now deletes only the objects in the namespace that were part of the big data cluster. | The namespace is not deleted. However, in earlier releases this command did delete the entire namespace. |
| _Security_ endpoint names have been changed and consolidated. | _Previous endpoints:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-security-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-security-nodeport**<br/><br/>_New endpoint:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-security** |
| _Proxy_ endpoint names have been changed and consolidated. | _Previous endpoints:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-proxy-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-proxy-nodeport**<br/><br/>_New endpoint:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-service-proxy** |
| _Controller_ endpoint names have been changed and consolidated. | _Previous endpoints:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-mssql-controller-lb**<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **service-mssql-controller-nodeport**<br/><br/>_New endpoint:_<br/> &nbsp; &nbsp; &nbsp; &bull; &nbsp; **endpoint-controller** |
| &nbsp; | &nbsp; |

### Known issues: Deployment

- Upgrading a big data data cluster from a previous release is not supported.

   > [!IMPORTANT]
   > You must backup your data and then delete your existing big data cluster (using the previous version of **mssqlctl**) before deploying the latest release. For more information, see [Upgrade to a new release](deployment-guidance.md#upgrade).

- The **ACCEPT_EULA** environment variable must be "yes" or "Yes" to accept the EULA. Previous releases permitted "y" and "Y" but these are no longer accepted and will cause the deployment to fail.

- The **CLUSTER_PLATFORM** environment variables does not have a default as it did in previous releases.

- After deploying on AKS, you might see the following two warning events from the deployment. Both of these events are known issues, but they do not prevent you from successfully deploying the big data cluster on AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- If a big data cluster deployment fails, the associated namespace is not removed. This could result in an orphaned namespace on the cluster. A workaround is to delete the namespace manually before deploying a cluster with the same name.

### Known issues: kubeadm deployments

If you use kubeadm to deploy Kubernetes on multiple machines, the cluster administration portal does not correctly display the endpoints needed to connect to the big data cluster. If you are experiencing this problem, use the following work around to discover the service endpoint IP addresses:

- If you are connecting from within the cluster, query Kubernetes for the service IP for the endpoint that you want to connect to. For example, the following **kubectl** command displays the IP address of the SQL Server master instance:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- If you are connecting from outside the cluster, use the following steps to connect:

   1. Get the IP address of the node running the SQL Server master instance: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`.

   1. Connect to SQL Server master instance using this IP address.

   1. Query the **cluster_endpoint_table** in master database for other external endpoints.

      If this fails with a connection timeout, it is possible the respective node is firewalled. In this case, you must contact your Kubernetes cluster administrator and ask for the node IP that is exposed externally. This could be any node. You can then use that IP and the corresponding port to connect to various services running in the cluster. For example, the administrator can find this IP by running:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

### <a id="mssqlctlctp23"></a> Known issues: mssqlctl

- The **mssqlctl** tool changed from a verb-noun command ordering to a noun-verb order. For example, `mssqlctl create cluster` is now `mssqlctl cluster create`.

- The `--name` parameter is now required when creating a cluster with `mssqlctl cluster create`.

   ```bash
   mssqlctl cluster create --name <cluster_name>
   ```

- For important information about upgrading to the latest version of big data clusters and **mssqlctl**, see [Upgrade to a new release](deployment-guidance.md#upgrade).

### Known issues: External tables

- It is possible to create a data pool external table for a table that has unsupported column types. If you query the external table, you get a message similar to the following:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- If you query a storage pool external table, you might get an error if the underlying file is being copied into HDFS at the same time.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- If you are creating an external table to Oracle that use character data types, the Azure Data Studio virtualization wizard interprets these columns as VARCHAR in the external table definition. This will cause a failure in the external table DDL. Either modify the Oracle schema to use the NVARCHAR2 type, or create EXTERNAL TABLE statements manually and specify NVARCHAR instead of using the wizard.

### Known issues: Application deployment

- When calling an R, Python, or MLeap application from the RESTful API, the call times-out in 5 minutes.

### Known issues: Spark and notebooks

- POD IP addresses may change in the Kubernetes environment as PODs restarts. In the scenario where the master-pod restarts, the Spark session may fail with `NoRoteToHostException`. This is caused by JVM caches that don't get refreshed with new IP addresses.

- If you have Jupyter already installed and a separate Python on Windows, Spark notebooks might fail. To work around this issue, upgrade Jupyter to the latest version.

- In a notebook, if you click the **Add Text** command, the text cell is added in preview mode rather than edit mode. You can click on the preview icon to toggle to edit mode and edit the cell.

### Known issues: HDFS

- If you right-click on a file in HDFS to preview it, you might see the following error:

   `Error previewing file: File exceeds max size of 30MB`

   Currently there is no way to preview files larger than 30 MB in Azure Data Studio.

- Configuration changes to HDFS that involve changes to hdfs-site.xml are not supported.

### Known issues: Security

- The SA_PASSWORD is part of the environment and discoverable (for example in a cord dump file). You must reset the SA_PASSWORD on the master instance after deployment. This is not a bug but a security step. For more information on how to change the SA_PASSWORD in a Linux container, see [Change the SA password](../linux/quickstart-install-connect-docker.md#sapassword).

- AKS logs may contain SA password for big data cluster deployments.

## <a id="ctp22"></a> CTP 2.2 (December 2018)

The following sections describe the new features and known issues for big data clusters in SQL Server 2019 CTP 2.2.

### What's in the CTP 2.2 release?

- Cluster Admin Portal accessed with `/portal` (**https://\<ip-address\>:30777/portal**).
- Master pool service name changed from `service-master-pool-lb` and `service-master-pool-nodeport` to `endpoint-master-pool`.
- New version of **mssqlctl** and updated images.
- Miscellaneous bug fixes and improvements.

### Known issues

The following sections provide known issues for SQL Server big data clusters in CTP 2.2.

#### Deployment

- Upgrading a big data data cluster from a previous release is not supported. You must backup and delete any existing big data cluster before deploying the latest release. For more information, see [Upgrade to a new release](deployment-guidance.md#upgrade).

- After deploying on AKS, you might see the following two warning events from the deployment. Both of these events are known issues, but they do not prevent you from successfully deploying the big data cluster on AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- If a big data cluster deployment fails, the associated namespace is not removed. This could result in an orphaned namespace on the cluster. A workaround is to delete the namespace manually before deploying a cluster with the same name.

#### Cluster administration portal

The cluster administration portal does not display the endpoint for the SQL Server master instance. To find the IP address and port for the master instance, use the following **kubectl** command:

```
kubectl get svc endpoint-master-pool -n <your-cluster-name>
```

#### External tables

- It is possible to create a data pool external table for a table that has unsupported column types. If you query the external table, you get a message similar to the following:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- If you query a storage pool external table, you might get an error if the underlying file is being copied into HDFS at the same time.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### Spark and notebooks

- POD IP addresses may change in the Kubernetes environment as PODs restarts. In the scenario where the master-pod restarts, the Spark session may fail with `NoRoteToHostException`. This is caused by JVM caches that don't get refreshed with new IP addresses.

- If you have Jupyter already installed and a separate Python on Windows, Spark notebooks might fail. To work around this issue, upgrade Jupyter to the latest version.

- In a notebook, if you click the **Add Text** command, the text cell is added in preview mode rather than edit mode. You can click on the preview icon to toggle to edit mode and edit the cell.

#### HDFS

- If you right-click on a file in HDFS to preview it, you might see the following error:

   `Error previewing file: File exceeds max size of 30MB`

   Currently there is no way to preview files larger than 30 MB in Azure Data Studio.

- Configuration changes to HDFS that involve changes to hdfs-site.xml are not supported.

#### Security

- The SA_PASSWORD is part of the environment and discoverable (for example in a cord dump file). You must reset the SA_PASSWORD on the master instance after deployment. This is not a bug but a security step. For more information on how to change the SA_PASSWORD in a Linux container, see [Change the SA password](../linux/quickstart-install-connect-docker.md#sapassword).

- AKS logs may contain SA password for big data cluster deployments.

## <a id="ctp21"></a> CTP 2.1 (November 2018)

The following sections describe the new features and known issues for big data clusters in SQL Server 2019 CTP 2.1.

### What's in the CTP 2.1 release?

- [Deploy Python and R apps](big-data-cluster-create-apps.md) in a big data cluster.
- New version of **mssqlctl** and updated images. 
- Miscellaneous bug fixes and improvements.

### Known issues

The following sections provide known issues for SQL Server big data clusters in CTP 2.1.

#### Deployment

- Upgrading a big data data cluster from a previous release is not supported. You must backup and delete any existing big data cluster before deploying the latest release. For more information, see [Upgrade to a new release](deployment-guidance.md#upgrade).

- After deploying on AKS, you might see the following two warning events from the deployment. Both of these events are known issues, but they do not prevent you from successfully deploying the big data cluster on AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- If a big data cluster deployment fails, the associated namespace is not removed. This could result in an orphaned namespace on the cluster. A workaround is to delete the namespace manually before deploying a cluster with the same name.

#### Admin portal

- When you [create an app using msqlctl-ctp command](big-data-cluster-create-apps.md) and deploy it on a SQL Server big data cluster, the Cluster Admin Portal shows the pods where the application was deployed as "Unknown" in the Controller section of the Admin Portion.

#### External tables

- It is possible to create a data pool external table for a table that has unsupported column types. If you query the external table, you get a message similar to the following:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- If you query a storage pool external table, you might get an error if the underlying file is being copied into HDFS at the same time.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### Spark and notebooks

- POD IP addresses may change in the Kubernetes environment as PODs restarts. In the scenario where the master-pod restarts, the Spark session may fail with `NoRoteToHostException`. This is caused by JVM caches that don't get refreshed with new IP addresses.

- If you have Jupyter already installed and a separate Python on Windows, Spark notebooks might fail. To work around this issue, upgrade Jupyter to the latest version.

- In a notebook, if you click the **Add Text** command, the text cell is added in preview mode rather than edit mode. You can click on the preview icon to toggle to edit mode and edit the cell.

#### HDFS

- If you right-click on a file in HDFS to preview it, you might see the following error:

   `Error previewing file: File exceeds max size of 30MB`

   Currently there is no way to preview files larger than 30 MB in Azure Data Studio.

- Configuration changes to HDFS that involve changes to hdfs-site.xml are not supported.

#### Security

- The SA_PASSWORD is part of the environment and discoverable (for example in a cord dump file). You must reset the SA_PASSWORD on the master instance after deployment. This is not a bug but a security step. For more information on how to change the SA_PASSWORD in a Linux container, see [Change the SA password](../linux/quickstart-install-connect-docker.md#sapassword).

- AKS logs may contain SA password for big data cluster deployments.

## <a id="ctp20"></a> CTP 2.0 (October 2018)

The following sections describe the new features and known issues for big data clusters in SQL Server 2019 CTP 2.0.

### What's in the CTP 2.0 release?

- Simple deployment experience using mssqlctl management tool
- Native notebook experience in Azure Data Studio
- Query HDFS files via Storage Instance of SQL Server
- Data virtualization via master to SQL Server, Oracle, MongoDB, and HDFS
- Data virtualization wizard for SQL Server and Oracle in Azure Data Studio
- ML Services on master
- Cluster administration portal that you can use for monitoring and troubleshooting
- Spark job submit in Azure Data Studio 
- Spark UI in the cluster administration portal
- Volume mounting to storage classes
- Queries over data pools from master
- Show plan for distributed queries in SSMS
- Pip package for mssqlctl management tool
- Built-in deployment engine through controller service

### Known issues

The following sections provide known issues for SQL Server big data clusters in CTP 2.0.

#### Deployment

- If you are using Azure Kubernetes Service (AKS), the recommended version of Kubernetes is 1.10.*, which does not support disk resizing. You should make sure you are sizing the storage accordingly at deployment time. For more information on how to adjust storage sizes, see the [Data persistence](concept-data-persistence.md) article. For Kubernetes deployed on VMs, the recommended version is 1.11.

- After deploying on AKS, you might see the following two warning events from the deployment. Both of these events are known issues, but they do not prevent you from successfully deploying the big data cluster on AKS.

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- If a big data cluster deployment fails, the associated namespace is not removed. This could result in an orphaned namespace on the cluster. A workaround is to delete the namespace manually before deploying a cluster with the same name.

#### External tables

- It is possible to create a data pool external table for a table that has unsupported column types. If you query the external table, you get a message similar to the following:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- If you query a storage pool external table, you might get an error if the underlying file is being copied into HDFS at the same time.

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### Spark and notebooks

- POD IP addresses may change in the Kubernetes environment as PODs restarts. In the scenario where the master-pod restarts, the Spark session may fail with `NoRoteToHostException`. This is caused by JVM caches that don't get refreshed with new IP addresses.

- If you have Jupyter already installed and a separate Python on Windows, Spark notebooks might fail. To work around this issue, upgrade Jupyter to the latest version.

- In a notebook, if you click the **Add Text** command, the text cell is added in preview mode rather than edit mode. You can click on the preview icon to toggle to edit mode and edit the cell.

#### HDFS

- If you right-click on a file in HDFS to preview it, you might see the following error:

   `Error previewing file: File exceeds max size of 30MB`

   Currently there is no way to preview files larger than 30 MB in Azure Data Studio.

- Configuration changes to HDFS that involve changes to hdfs-site.xml are not supported.

#### Security

- The SA_PASSWORD is part of the environment and discoverable (for example in a cord dump file). You must reset the SA_PASSWORD on the master instance after deployment. This is not a bug but a security step. For more information on how to change the SA_PASSWORD in a Linux container, see [Change the SA password](../linux/quickstart-install-connect-docker.md#sapassword).

- AKS logs may contain SA password for big data cluster deployments.

## Next steps

For more information about SQL Server big data clusters, see [What are SQL Server 2019 big data clusters?](big-data-cluster-overview.md).
