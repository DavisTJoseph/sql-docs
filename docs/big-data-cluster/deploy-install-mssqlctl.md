---
title: Install mssqlctl
titleSuffix: SQL Server big data clusters
description: Learn how to install the mssqlctl tool for installing and managing SQL Server 2019 big data clusters (preview).
author: rothja 
ms.author: jroth 
manager: jroth
ms.date: 06/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
---

# Install mssqlctl to manage SQL Server big data clusters

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

This article describes how to install the **mssqlctl** tool for CTP 3.1 on Windows or Linux.

**mssqlctl** is a command-line utility written in Python that enables cluster administrators to bootstrap and manage the big data cluster via REST APIs. The minimum Python version required is v3.5. You must also have `pip` that is used to download and install **mssqlctl** tool. The instructions below provide examples for Windows and Ubuntu. For installing Python on other platforms, see the [Python documentation](https://wiki.python.org/moin/BeginnersGuide/Download).

> [!IMPORTANT]
> If you are installing a newer version of big data clusters, you must backup your data and delete the old cluster *before* upgrading **mssqlctl** and installing the new release. For more information, see [Upgrading to a new release](deployment-upgrade.md).

## <a id="windows"></a> Windows mssqlctl installation

1. On a Windows client, download the necessary Python package from [https://www.python.org/downloads/](https://www.python.org/downloads/). For python3.5.3 and later, pip3 is also installed when you install Python. 

   > [!TIP] 
   > When installing Python3, select to add Python to your **PATH**. If you do not, you can later find where pip3 is located and manually add it to your **PATH**.

1. Open a new Windows PowerShell session so that it gets the latest path with Python in it.

1. If you have any previous releases of **mssqlctl** installed, it is important to uninstall **mssqlctl** first before installing the latest version.

   If you are uninstalling **mssqlctl** corresponding to CTP version 2.2 or lower run:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   For CTP 2.3 or higher, run the following command. Replace `ctp3.0` in the command with the version of **mssqlctl** that you are uninstalling. If the version is prior to CTP 3.0, add a dash before the version number (for example, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Install **mssqlctl** with the following command:

   ```powershell
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

## <a id="linux"></a> Linux mssqlctl installation

On Linux, you must install Python 3.5 and then upgrade pip. The following example shows the commands that would work for Ubuntu. For other Linux platforms, see the [Python documentation](https://wiki.python.org/moin/BeginnersGuide/Download).

1. Install the necessary Python packages:

   ```bash
   sudo apt-get update && /
   sudo apt-get install -y python3 && /
   sudo apt-get install -y python3-pip
   ```

1. Upgrade pip3:

   ```bash
   sudo -H pip3 install --upgrade pip
   ```

1. If you have any previous releases of **mssqlctl** installed, it is important to uninstall **mssqlctl** first before installing the latest version.

   If you are uninstalling **mssqlctl** corresponding to CTP version 2.2 or lower run:

   ```powershell
   pip3 uninstall mssqlctl
   ```

   For CTP 2.3 or higher, run the following command. Replace `ctp3.0` in the command with the version of **mssqlctl** that you are uninstalling. If the version is prior to CTP 3.0, add a dash before the version number (for example, `ctp-2.5`).

   ```powershell
   pip3 uninstall -r  https://private-repo.microsoft.com/python/ctp3.0/mssqlctl/requirements.txt
   ```

1. Install **mssqlctl** with the following command:

   ```bash
   pip3 install -r  https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt --user
   ```

   > [!NOTE]
   > The `--user` switch installs mssqlctl to the Python user install directory. This is typically `~/.local/bin` on Linux. Either add this directory to your path or navigate to the user install directory and run `./mssqlctl` from there.

## Next steps

For more information about big data clusters, see [What are SQL Server 2019 big data clusters?](big-data-cluster-overview.md).
