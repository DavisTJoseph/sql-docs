---
title: mssqlctl bdc debug reference
titleSuffix: SQL Server big data clusters
description: Reference article for mssqlctl bdc debug commands.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
---

# mssqlctl bdc debug

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

The following article provides reference for the **bdc debug** commands in the **mssqlctl** tool. For more information about other **mssqlctl** commands, see [mssqlctl reference](reference-mssqlctl.md).

## Commands
|     |     |
| --- | --- |
[mssqlctl bdc debug copy-logs](#mssqlctl-bdc-debug-copy-logs) | Copy logs.
[mssqlctl bdc debug dump](#mssqlctl-bdc-debug-dump) | Trigger logging dump.
## mssqlctl bdc debug copy-logs
Copy the debug logs from the Big Data Cluster - kube config is required on your system.
```bash
mssqlctl bdc debug copy-logs --namespace -n 
                             [--container -c]  
                             [--target-folder -d]  
                             [--pod -p]  
                             [--timeout -t]
```
### Required Parameters
#### `--namespace -n`
BDC name, used for kubernetes namespace.
### Optional Parameters
#### `--container -c`
Copy the logs for the containers with similar name, Optional, by default copies logs for all containers. Cannot be specified multiple times. If specified multiple times, last one will be used
#### `--target-folder -d`
Target folder path to copy logs to. Optional, by default creates the result in the local folder.  Cannot be specified multiple times. If specified multiple times, last one will be used
#### `--pod -p`
Copy the logs for the pods with similar name. Optional, by default copies logs for all pods. Cannot be specified multiple times. If specified multiple times, last one will be used
#### `--timeout -t`
The number of seconds to wait for the command to complete. The default value is 0 which is unlimited
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org/]) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## mssqlctl bdc debug dump
Trigger logging dump and copy it out from container - kube config is required on your system.
```bash
mssqlctl bdc debug dump --namespace -n 
                        --container -c  
                        [--target-folder -d]
```
### Required Parameters
#### `--namespace -n`
BDC name, used for kubernetes namespace.
#### `--container -c`
Copy the logs for the containers with similar name, Optional, by default copies logs for all containers. Cannot be specified multiple times. If specified multiple times, last one will be used
### Optional Parameters
#### `--target-folder -d`
Target folder path to copy logs to. Optional, by default creates the result in the local folder.  Cannot be specified multiple times. If specified multiple times, last one will be used
`./output/dump`
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org/]) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.

## Next steps

For more information about other **mssqlctl** commands, see [mssqlctl reference](reference-mssqlctl.md). For more information about how to install the **mssqlctl** tool, see [Install mssqlctl to manage SQL Server 2019 big data clusters](deploy-install-mssqlctl.md).