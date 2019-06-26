---
title: "Download SQL Server Management Studio (SSMS) | Microsoft Docs"
ms.prod: sql
ms.prod_service: "sql-tools"
ms.reviewer: ""
ms.technology: ssms
ms.topic: conceptual
keywords: 
  - "install ssms, download ssms, latest ssms"
  - "SQL Server Management Studio"
  - "ssms.exe"
  - "sql man studio"
  - "sql management studio"
  - "sql management studio install"
  - "download sql management studio"
  - "ms sql management studio"
  - "install sql management studio"
  - "ssms download"
  - "sql server ssms"
  - "ssms express"
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
ms.reviewer: sstein
manager: craigg
ms.custom: ""
ms.date: 06/12/2019
---

# Download SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SQL Server Management Studio (SSMS) is an integrated environment for managing any SQL infrastructure, from SQL Server to Azure SQL Database. SSMS provides tools to configure, monitor, and administer instances of SQL Server and databases. Use SSMS to deploy, monitor, and upgrade the data-tier components used by your applications, as well as build queries and scripts.

Use SSMS to query, design, and manage your databases and data warehouses, wherever they are - on your local computer, or in the cloud.

SSMS is free!

## Download SSMS 18.1

**SSMS 18.1 is now available, and is the latest general availability (GA) version of *SQL Server Management Studio* that provides support for [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]!**

**[![download](../ssdt/media/download.png) Download SQL Server Management Studio 18.1 ](https://go.microsoft.com/fwlink/?linkid=2094583)**

SSMS 18.1 is the latest general availability (GA) version of SSMS. If you have SSMS 18.0 (GA) installed, installing SSMS 18.1 upgrades it to 18.1. If you have an older *preview* version of SSMS 18.0 installed, you must uninstall it before installing SSMS 18.1.

**Version Information**

- Release number: 18.1<br>
- Build number: 15.0.18131.0<br>
- Release date: June 11, 2019

If you have comments or suggestions, or you want to report issues, the best way to reach out to the SSMS Team is at [UserVoice](https://aka.ms/sqlfeedback).

The SSMS 18.x installation does not upgrade or replace SSMS versions 17.x or earlier. SSMS 18.x installs side by side with previous versions so both versions are available for use.

If a computer contains side by side installations of SSMS, verify you start the correct version for your specific needs. The latest version is labeled **Microsoft SQL Server Management Studio 18**

## Available Languages (SSMS 18.1)

This release of SSMS can be installed in the following languages:

SQL Server Management Studio 18.1:<br>
[Chinese (Simplified)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Chinese (Traditional)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [English (United States)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [French](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [German](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italian](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Japanese](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Korean](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Portuguese (Brazil)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Russian](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Spanish](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

> [!NOTE]
> The SQL Server PowerShell module is a separate install through the PowerShell Gallery. For more information, see [Download SQL Server PowerShell Module](download-sql-server-ps-module.md).

## New in this Release (SSMS 18.1)

- **Database diagrams** - Database diagrams were added back into SSMS. For details, see [Database Diagrams](https://feedback.azure.com/forums/908035/suggestions/37507828).
- **SSBDIAGNOSE.EXE** - The SQL Server Diagnose command line tool was added back into the SSMS package.
- **Integration Services (SSIS)** - Support for scheduling SSIS package, located in SSIS Catalog in Azure or File System, in Azure. There are three entries for launching the New Schedule dialog, *New Schedule…* menu item shown when right-clicking the SSIS package in SSIS Catalog in Azure, *Schedule SSIS Package in Azure* menu item under *Migrate to Azure* menu item under *Tools* menu item and "Schedule SSIS in Azure" shown when right-clicking Jobs folder under SQL Server agent of Azure SQL Database Managed Instance.

For details about what's new in this release, see [the SSMS release notes](release-notes-ssms.md).

## Supported SQL offerings (SSMS 18.1)

* This version of SSMS works with all [supported versions of SQL Server 2008 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) and provides the greatest level of support for working with the latest cloud features in Azure SQL Database and Azure SQL Data Warehouse.
* Additionally, SSMS 18.x can be installed side by side with SSMS 17.x, SSMS 16.x, or SQL Server 2014 SSMS and earlier.
* SQL Server Integration Services (SSIS) - SSMS version 17.x or later does not support connecting to the legacy SQL Server Integration Services service. To connect to an earlier version of the legacy Integration Services, use the version of SSMS aligned with the version of SQL Server. For example, use SSMS 16.x to connect to the legacy SQL Server 2016 Integration Services service. SSMS 17.x and SSMS 16.x can be installed side-by-side on the same computer. Since the release of SQL Server 2012, the SSIS Catalog database, SSISDB, is the recommended way to store, manage, run, and monitor Integration Services packages. For details, see [SSIS Catalog](../integration-services/catalog/ssis-catalog.md).

## Supported Operating systems (SSMS 18.1)

This release of SSMS supports the following 64-bit platforms when used with the latest available service pack:

- Windows 10 (64-bit) <sup>*</sup>
- Windows 8.1 (64-bit)
- Windows Server 2019 (64-bit)
- Windows Server 2016 (64-bit) <sup>*</sup>
- Windows Server 2012 R2 (64-bit)
- Windows Server 2012 (64-bit)
- Windows Server 2008 R2 (64-bit)

<sup>*</sup> Requires version 1607 (10.0.14393) or later

> [!NOTE]
> SSMS runs on Windows only. If you need a tool that runs on platforms other than Windows, take a look at Azure Data Studio. Azure Data Studio is a new cross-platform tool that runs on macOS, Linux, as well as Windows. For details, see [Azure Data Studio](../azure-data-studio/what-is.md).

## Release Notes (SSMS 18.1)

There are a few [known issues](release-notes-ssms.md#known-issues-181) with this release.

For details about this release, see [the SSMS release notes](release-notes-ssms.md).

## Previous SSMS releases

[Previous SQL Server Management Studio Releases](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## See Also

- [Tutorial: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [SQL Server Management Studio documentation](sql-server-management-studio-ssms.md)
- [Additional updates and service packs](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Download SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
