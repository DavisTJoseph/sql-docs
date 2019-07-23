---
title: "What's new in SQL Server 2019 | Microsoft Docs"
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ""
ms.technology: release-landing
ms.topic: "article"
author: MikeRayMSFT
ms.author: mikeray
monikerRange: ">=sql-server-ver15||=sqlallproducts-allversions"
---
# What's new in [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] builds on previous releases to grow SQL Server as a platform that gives you choices of development languages, data types, on-premises or cloud, and operating systems.

This article summarizes new features and enhancements for [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

For more information and known issues, see the [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Release Notes](sql-server-ver15-release-notes.md).

**Use the [latest tools](what-s-new-in-sql-server-ver15-prerelease.md#tools) for the best experience with [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## CTP 3.2 July 2019

Community technology preview (CTP) 3.2 is the latest public release of [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. This release includes improvements from previous CTP releases to fix bugs, improve security, and optimize performance. For a list of features introduced or improved in each of the CTP releases before [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2, see [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP announcement archive](what-s-new-in-sql-server-ver15-prerelease.md).

### New in big data clusters

|New feature or update | Details |
|:---|:---|
|Public preview |Prior to CTP 3.2, SQL Server big data cluster was available to registered early adopters. This release allows anyone to experience the features of SQL Server Big data clusters. <br/><br/> See [Get started with SQL Server big data clusters](../big-data-cluster/deploy-get-started.md).|
|`azdata` |CTP 3.2 introduces `azdata` - a command-line utility written in Python that enables cluster administrators to bootstrap and manage the big data cluster via REST APIs. `azdata` replaces `mssqlctl`. See [Install `azdata`](../big-data-cluster/deploy-install-azdata.md). |
|PolyBase |External table column names are now used for querying SQL Server, Oracle, Teradata, MongoDB, and ODBC data sources. |
|HDFS tiering refresh |Introducing refresh functionality for HDFS tiering so that an existing mount can be refreshed for the latest snapshot of the remote data. See [HDFS tiering](../big-data-cluster/hdfs-tiering.md) |
|Notebook-based troubleshooting |CTP 3.2 introduces Jupyter notebooks to assist with [deployment](../big-data-cluster/deploy-notebooks.md) and [discovery, diagnosis, and troubleshooting](../big-data-cluster/manage-notebooks.md) for components in a SQL Server big data cluster. |
| &nbsp; | &nbsp; |

### New in Analysis Services

| New feature or update | Details |
|:---|:---| 
| Governance setting for Power BI cache refreshes.  | The Power BI service caches dashboard tile data and report data for initial load of Live Connect report, causing an excessive number of cache queries being submitted to SSAS, and in extreme cases overload the server. This release  introduces the **ClientCacheRefreshPolicy** property. This property allows you to override this behavior at the server level. To learn more, see [General Properties](../analysis-services/server-properties/general-properties.md). |
| Online attach  | This feature provides the ability to attach a tabular model as an online operation. Online attach can be used for synchronization of read-only replicas in on-premises query scale-out environments. To learn more see [Online attach](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32) in Details. |
| &nbsp; | &nbsp; |

## [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] features by component

The following sections highlight new components and features that were enhanced in earlier releases of [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## Big data clusters

| New feature or update | Details |
|:---|:---|
| Scalable big data solution | [Deploy scalable clusters](../big-data-cluster/deploy-get-started.md) of SQL Server, Spark, and HDFS containers running on Kubernetes <br/><br/> Read, write, and process big data from Transact-SQL or Spark<br/><br/> Easily combine and analyze high-value relational data with high-volume big data<br/><br/>Query external data sources<br/><br/>Store big data in HDFS managed by SQL Server<br/><br/>Query data from multiple external data sources through the cluster<br/><br/> Use the data for AI, machine learning, and other analysis tasks<br/><br/> Deploy and run applications in big data clusters <br/>|
| &nbsp; | &nbsp; |

For more details, see [What are SQL Server big data clusters](../big-data-cluster/big-data-cluster-overview.md)

[[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP) announcement archive](what-s-new-in-sql-server-ver15-prerelease.md) contains a list of features announced and changed for all previous CTP releases of this feature.

## Database engine

### Security

|New feature or update | Details |
|:---|:---|
|Feature restrictions| Prevent some forms of SQL injection from leaking information about the database, even when the SQL injection is successful. See [Feature restrictions](../relational-databases/security/feature-restrictions.md)|
|Index encrypted columns|Create indexes on columns encrypted using randomized encryption and enclave-enabled keys, to improve the performance of rich queries (using `LIKE` and comparison operators). See [Always Encrypted with Secure Enclaves](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Suspend and resume initial scan for Transparent Data Encryption (TDE)|See [Transparent Data Encryption (TDE) scan - suspend and resume](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|Certificate management in SQL Server Configuration Manager|See [Certificate Management (SQL Server Configuration Manager)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |

### Graph

|New feature or update | Details |
|:---|:---|
|Edge constraint cascade delete actions |Define cascaded delete actions on an edge constraint in a graph database. See[Edge constraints](../relational-databases/tables/graph-edge-constraints.md). |
|New graph function - `SHORTEST_PATH` | Use `SHORTEST_PATH` inside `MATCH` to find the shortest path between any 2 nodes in a graph or to perform arbitrary length traversals.|
|Partition tables and indexes| The data of partitioned tables and indexes is divided into units that can be spread across more than one filegroup in a graph database. |
|Use derived table or view aliases in graph match query |See [Graph Edge Constraints](../relational-databases/tables/graph-edge-constraints.md). |
| &nbsp; | &nbsp; |

### Indexes

|New feature or update | Details |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Turns on an optimization within the database engine that helps improve throughput for high-concurrency inserts into the index. This option is intended for indexes that are prone to last-page insert contention, typically seen with indexes that have a sequential key such as an identity column, sequence, or date/time column. See [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys) for more information.|
|Build and rebuild online clustered columnstore index | See [Perform Index Operations Online](../relational-databases/indexes/perform-index-operations-online.md). |
| &nbsp; | &nbsp; |

### In memory databases

|New feature or update | Details |
|:---|:---|
|DDL control for hybrid buffer pool |With [hybrid buffer pool](../database-engine/configure-windows/hybrid-buffer-pool.md), database pages sitting on database files placed on a persistent memory (PMEM) device will be directly accessed when required.|
|Memory-optimized tempdb metadata|See [Memory-Optimized TempDB Metadata](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
| &nbsp; | &nbsp; |

### Linked servers

|New feature or update | Details |
|:---|:---|
|Linked Servers support UTF-8 character encoding. |[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### PolyBase

|New feature or update | Details |
|PolyBase |External table column names are now used for querying SQL Server, Oracle, Teradata, MongoDB & ODBC data sources. |
| &nbsp; | &nbsp; |

### Collation

|New feature or update | Details |
|:---|:---|
|Support UTF-8 character encoding |Enabled for a BIN2 collation (`Latin1_General_100_BIN2_UTF8`). See [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md). |
|Select UTF-8 collation as default during setup | See [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md#ctp23). |
| &nbsp; | &nbsp; |

### Server settings

|New feature or update | Details |
|:---|:---|
|Set `MIN` and `MAX` server memory values at setup |During setup, you can set server memory values. Use the default values, the calculated recommended values, or manually specify your own values once you've chosen the **Recommended** option [Server Memory Server Configuration Options](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).|
|SQL Server Setup enables MAXDOP settings |New recommendations follow the documented guidelines.[Configure the max degree of parallelism Server Configuration Option](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|Hybrid buffer pool| New feature of the SQL Server database engine where database pages sitting on database files placed on a persistent memory (PMEM) device will be directly accessed when required. See [Hybrid buffer pool](../database-engine/configure-windows/hybrid-buffer-pool.md) .|
| &nbsp; | &nbsp; |

### Performance monitoring

|New feature or update | Details |
|:---|:---|
|Scalar UDF inlining |Automatically transforms scalar user-defined functions (UDF) into relational expressions and embeds them in the calling SQL query. See [Scalar UDF Inlining](../relational-databases/user-defined-functions/scalar-udf-inlining.md). |
| `sys.dm_exec_requests` column `command` | Shows `SELECT (STATMAN)` if a `SELECT` is waiting for a synchronous statistics update operation to complete prior to continuing query execution. See [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | New wait type in `sys.dm_os_wait_stats` dynamic management view. It shows the accumulated instance-level time spent on synchronous statistics refresh operations. See [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Custom capture policy for the Query Store|When enabled, additional Query Store configurations are available under a new Query Store Capture Policy setting, to fine-tune data collection in a specific server. For more information, see [ALTER DATABASE SET Options](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`sys.dm_exec_query_plan_stats` |New DMF returns the equivalent of the last known actual execution plan for most queries. See [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | New database scoped configuration to enable `sys.dm_exec_query_plan_stats`. See [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|New database scoped configuration. See [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`query_post_execution_plan_profile` | Extended Event collects the equivalent of an actual execution plan based on lightweight profiling, unlike `query_post_execution_showplan` which uses standard profiling. See [Query profiling infrastructure](../relational-databases/performance/query-profiling-infrastructure.md).|

### Language extensions

|New feature or update | Details |
|:---|:---|
|New Java language SDK | Simplifies development of Java programs that can be run from SQL Server. See [What's new in SQL Server Machine Learning Services](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
|SQL Server Language Extensions - [Java language extension](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|The [Microsoft Extensibility SDK for Java for Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) is now open source and [available on GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Register external languages|New DDL, `CREATE EXTERNAL LANGUAGE`, registers external languages, like Java, in SQL Server. See [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
|Support for Java data types|See [Java data types](../language-extensions/how-to/java-to-sql-data-types.md).|

### Spatial

|New feature or update | Details |
|:---|:---|
| New spatial reference identifiers (SRIDs) |[Australian GDA2020](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) provides more robust and accurate datum which is more closely aligned to global positioning systems. The new SRIDs are:<br/><br/> - 7843 - geographic 2D<br/> - 7844 - geographic 3D <br/><br/>[sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) view contains definitions of new SRIDs. |
| &nbsp; | &nbsp; |

### Performance

|New feature or update | Details |
|:---|:---|
|Accelerated database recovery | Enable accelerated database recovery per-database. See [Accelerated database recovery](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
|Forcing fast forward and static cursors | Query Store plan forcing support for fast forward and static cursors. See [Plan forcing support for fast forward and static cursors](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Reduced recompilations for workloads| Improves using temporary tables across multiple scopes. See [Reduced recompilations for workloads](../relational-databases/tables/tables.md#ctp23) |
|Indirect checkpoint scalability |See [Improved indirect checkpoint scalability](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
| &nbsp; | &nbsp; |

### Availability groups

|New feature or update | Details |
|:---|:---|
|Up to five synchronous replicas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] increases the maximum number of synchronous replicas to 5, up from 3 in [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. You can configure this group of five replicas to have automatic failover within the group. There is one primary replica, plus four synchronous secondary replicas.|
|Secondary-to-primary replica connection redirection| Allows client application connections to be directed to the primary replica regardless of the target server specified in the connection string. For details, see [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md).|
| &nbsp; | &nbsp; |

### Error messages

|New feature or update | Details |
|:---|:---|
|Verbose truncation warnings | Truncation error message defaults to include table and column names, and truncated value. See [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## SQL Server on Linux

| New feature or update | Details |
|:-----|:-----|
|New container registry|[Get started with SQL Server containers on Docker](../linux/quickstart-install-connect-docker.md) |
|Always On Availability Group on Docker containers with Kubernetes |[Always On Availability Groups for containers](../linux/sql-server-ag-kubernetes.md) |
|Replication support |[SQL Server Replication on Linux](../linux/sql-server-linux-replication.md)
|Support for the Microsoft Distributed Transaction Coordinator (MSDTC) |[How to configure MSDTC on Linux](../linux/sql-server-linux-configure-msdtc.md) |
|OpenLDAP support for third-party AD providers |[Tutorial: Use Active Directory authentication with SQL Server on Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning on Linux |[Configure Machine Learning on Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Tempdb improvements | By default, a new installation of SQL Server on Linux creates multiple tempdb data files based on the number of logical cores (with up to 8 data files). This does not apply to in-place minor or major version upgrades. Each tempdb file is 8 MB with an auto growth of 64 MB. This behavior is similar to the default SQL Server installation on Windows. |
| PolyBase on Linux | [Install PolyBase](../relational-databases/polybase/polybase-linux-setup.md) on Linux for non-Hadoop connectors.<br/><br/>[PolyBase type mapping](../relational-databases/polybase/polybase-type-mapping.md). |
| &nbsp; | &nbsp; |

## <a id="ml"></a> SQL Server Machine Learning Services

|New feature or update | Details |
|:---|:---|
|Partition-based modeling|Process external scripts per partition of your data using the new parameters added to `sp_execute_external_script`. This functionality supports training many small models (one model per partition of data) instead of one large model. See [Create partition-based models](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)|
|Windows Server Failover Cluster| Configure high availability for Machine Learning Services on a Windows Server Failover Cluster.|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| New feature or update | Details |
|:---|:---|
|Supports Azure SQL Database managed instance databases.| Host [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] on a managed instance. See [[!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] installation and configuration](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).|
|New HTML controls| HTML controls replace all former Silverlight components. Silverlight dependency removed.|
| &nbsp; | &nbsp; |

## Analysis Services

| New feature or update | Details |
|:---|:---|
|Calculation groups in tabular model| [Calculation groups in tabular model](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|MDX query support for tabular models with calculation groups | See [Calculation groups](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Dynamic formatting of measures using calculation groups |This feature allows you to conditionally change format strings for measures with [calculation groups](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). For example, with currency conversion, a measure can be displayed using different foreign currency formats.|
|Many-to-many relationships in tabular models|[Many-to-many relationships in tabular models](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Property settings for resource governance|[Property settings for resource governance](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

For specific features excluded from support, see the [release notes](sql-server-ver15-release-notes.md).

In addition, the following features are added or enhanced for [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2.

## See also

- [`SqlServer` PowerShell module](https://www.powershellgallery.com/packages/Sqlserver)
- [SQL Server PowerShell documentation](../powershell/sql-server-powershell.md)

## Next steps

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Release Notes](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: Technical white paper](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Published in September 2018. Applies to Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 for Windows, Linux, and Docker containers.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
