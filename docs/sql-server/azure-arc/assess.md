---
title: Configure SQL assessment for Azure Arc enabled SQL Server
titleSuffix:
description: Configure on-demand assessment for Azure Arc enabled instance of SQL Server
author: anosov1960
ms.author: sashan 
ms.reviewer: mikeray
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
---
# Configure on-demand SQL assessment for Azure Arc enabled SQL Server instance

You can enable SQL assessment for your SQL Server instances by following these steps.

## Prerequisites

* Your SQL Server instance is connected to Azure Arc. Follow these the instructions to [onboard your SQL Server instance to  Arc-enabled SQL Server](connect.md).

* The MMA extension is installed and configured on the machine. Follow these the instructions to [Install Microsoft Monitoring Agent (MMA)](configure-advanced-data-security.md#install-microsoft-monitoring-agent-mma). For more information, see [Log Analytics Agent](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent).

* Your SQL Server has the [TCP/IP protocol enabled](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).

* The [SQL Server browser](../../tools/configuration-manager/sql-server-browser-service.md) is running if you are operating a named instance of SQL Server.

* You reviewed the SQL Server document at [Services Hub On-Demand Assessments Prerequisites](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents).

## Enable on-demand SQL Assessment

1. Open your SQL Server – Azure Arc resource and select __Environment Health__ in the left menu.

   ![SQL Assessment selection](media/assess/sql-assessment-heading-sql-server-arc.png)

1. Specify a working directory on the data collection machine. During collection and analysis, data is temporarily stored under that folder. If the folder doesn't exist, it is created automatically.

1. Click on __Download configuration script__ and copy the downloaded script to the target machine.

1. Launch an admin instance of __powershell.exe__ and do one of the following: 
   * If your are using a domain account, run the following commands. You will be prompted for the user account and password. 

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1'
      ```

    * If you are using an MSA account, run the following commands.

      ```powershell
      Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass -Force
      & '.\AddSqlAssessment.ps1' -ManagedServiceAccountName <MSA account name>
      ```

   > [!NOTE]
   > The script will schedule a task named *SQLAssessment* to run within an hour of running the previous script and then every 7 days. The task can be modified to run on a different date and time or even forced to run immediately from the task scheduler library > Microsoft > Operations Management Suite > AOI*** > Assessments > SQLAssessment. This task triggers data collection.

## View the assessment results

The button __View SQL assessment result__ on the _Environment Health_ blade is disabled until the the results are ready in Log Analytics. Once the button is activated, you can click on it to view the results. It could take up to 2 hours to see the results in Log Analytics after the data files are processed on the target machine.

![SQ: assessment results](media/assess/sql-assessment-results.png)

You can see the state of data processing on the collection machine by checking the files in the working folder. After the scheduled task is completed, you should see several files with the _new._ prefix in the working directory:

![Data files ready](media/assess/sql-assessment-data-files-ready.png)

The Microsoft Monitoring Agent scans the working folder every 15 minutes looking for _new.*_ files, and sends the data to the Log analytics workspace. Once the file is uploaded, the prefix will change from _new._ to _processed._:

![Data files processed](media/assess/sql-assessment-data-files-processed.png)

## Next steps

See the SQL Server document at [Services Hub On-Demand Assessments Prerequisites](https://docs.microsoft.com/services-hub/health/assessment-prereq-docs#on-demand-assessment-prerequisite-documents) for more information.

To obtain comprehensive support of the On-demand SQL Assessment, a Premier or Unified support subscription is required. See [Azure Premier Support](https://azure.microsoft.com/support/plans/premier) for details.
