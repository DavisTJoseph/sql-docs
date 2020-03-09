---
title: Install SQL Server Machine Learning Services (Python, R) on Linux
description: 'Learn how to install SQL Server Machine Learning Services (Python and R) on Linux: Red Hat, Ubuntu, and SUSE.'
author: cawrites
ms.author: chadam
ms.reviewer: vanto
manager: cgronlun
ms.date: 03/05/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: ">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
---
# Install SQL Server Machine Learning Services (Python and R) on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

This article guides you in the installation of [SQL Server Machine Learning Services](../advanced-analytics/index.yml) on Linux. Python and R scripts can be executed in-database using Machine Learning Services.

[!NOTE]
> Machine Learning Services is installed by default on SQL Server Big Data Clusters. For more information, see [Use Machine Learning Services (Python and R) on Big Data Clusters](../big-data-cluster/machine-learning-services.md)

## What are Machine Learning Services

Machine Learning Services is a feature add-on to the database engine.

Install and configure the SQL Server database engine first so that you can resolve any issues before adding more components.

## Pre-install checklist

[Install SQL Server on Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup) and verify install.

* Check the SQL Server Linux repositories for the Python and R extensions. 
* If you already configured source repositories for the database engine install, you can run the **mssql-mlservices** package install commands using the same repo registration.

* [Microsoft R Open](#mro) provides the base R distribution for the R feature in SQL Server

* You should have a tool for running T-SQL commands. 
* A query editor is necessary for post-install configuration and validation. 
* We recommend [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), a free download that runs on Linux.


<a name="mro"></a>

### Microsoft R Open (MRO) installation

Microsoft's base distribution of R is a prerequisite for using RevoScaleR, MicrosoftML, and other R packages installed with Machine Learning Services.

The required version is MRO 3.5.2.

Choose from the following two approaches to install MRO:

+ Download the MRO tarball from MRAN, unpack it, and run its install.sh script. You can follow the [installation instructions on MRAN](https://mran.microsoft.com/releases/3.5.2) if you want this approach.

+ Register the **packages.microsoft.com** repo as described below to install the MRO distribution: microsoft-r-open-mro and microsoft-r-open-mkl. 

<a name="RHEL"></a>

## Install on RedHat

### Install (MRO) on Red Hat

```bash
# Import the Microsoft repository key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc


# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm

# Update packages on your system (optional)
yum update
```

Installation Options for Python and R:

*  Install language support based on your requirements (single or multiple languages).
*  The *full installation* provides all available features the including pre-trained machine learning models.
*  The *minimal installation* excludes the models but still has all of the functionality.

> [!Tip]
> If possible, run `yum clean all` to refresh packages on the system prior to installation.

### Example 1 -  Full installation

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  extensions (Python, R)
*  machine learning libraries
*  pre-trained models for Python and R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo yum install mssql-mlservices-mlm-py-9.4.7*
sudo yum install mssql-mlservices-mlm-r-9.4.7*
```

### Example 2 - Minimum installation

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  core Revo* libraries
*  machine learning libraries

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo yum install mssql-mlservices-packages-py-9.4.7*
sudo yum install mssql-mlservices-packages-r-9.4.7*
```
<a name="ubuntu"></a>

## Install on Ubuntu

### Install (MRO) on Ubuntu

```bash
# Install as root
sudo su

# Optionally, if your system does not have the https apt transport option
apt-get install apt-transport-https

# Set the location of the package repo the "prod" directory containing the distribution.
# This example specifies 16.04. Replace with 14.04 if you want that version
wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the repo
dpkg -i packages-microsoft-prod.deb

# Update packages on your system (required), including MRO installation
sudo apt-get update
```

Installation Options for Python and R:

*  Install language support based on your requirements (single or multiple languages).
*  The *full installation* provides all available features the including pre-trained machine learning models.
*  The *minimal installation* excludes the models but still has all of the functionality.

> [!Tip]
> If possible, run `apt-get update` to refresh packages on the system prior to installation. 

### Example 1 -  Full installation 

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  Python extensions
*  R extensions
*  machine learning libraries
*  pre-trained models for Python and R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# There is no asterisk in this full install
sudo apt-get install mssql-mlservices-mlm-py 
sudo apt-get install mssql-mlservices-mlm-r 
```

### Example 2 - Minimum installation 

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  core Revo* libraries
*  machine learning libraries

```bash
# Install as root or sudo
# Minimum install of R, Python
# No asterisk
sudo apt-get install mssql-mlservices-packages-py
sudo apt-get install mssql-mlservices-packages-r
```

<a name="SLES"></a>

## Install on SUSE

### Install (MRO) on SUSE(SLES)

```bash
# Install as root
sudo su

# Set the location of the package repo at the "prod" directory containing the distribution
# This example is for SLES12, the only supported version of SUSE in Machine Learning Server
zypper ar -f https://packages.microsoft.com/sles/12/prod packages-microsoft-com

# Update packages on your system (optional)
zypper update
```

Installation Options for Python and R:

*  Install language support based on your requirements (single or multiple languages).
*  The *full installation* provides all available features the including pre-trained machine learning models.
*  The *minimal installation* excludes the models but still has all of the functionality.

### Example 1 -  Full installation 

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  extensions for Python and R
*  machine learning libraries
*  pre-trained models for Python and R

```bash
# Install as root or sudo
# Add everything (all R, Python)
# Be sure to include -9.4.7* in mlsservices package names
sudo zypper install mssql-mlservices-mlm-py-9.4.7*
sudo zypper install mssql-mlservices-mlm-r-9.4.7* 
```

### Example 2 - Minimum installation 

Includes:
*  open-source Python
*  open-source R
*  extensibility framework
*  microsoft-openmpi
*  core Revo* libraries
*  machine learning libraries 

```bash
# Install as root or sudo
# Minimum install of R, Python extensions
# Be sure to include -9.4.6* in mlsservices package names
sudo zypper install mssql-mlservices-packages-py-9.4.7*
sudo zypper install mssql-mlservices-packages-r-9.4.7*
```

## Post-install config (required)

Additional configuration is primarily through the [mssql-conf tool](sql-server-linux-configure-mssql-conf.md).


1. Add the mssql user account used to run the SQL Server service.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

2. Accept the licensing agreements for open-source Python and R extensions. Use the following command:

   ```bash
   # Run as SUDO or root
   # Use set + EULA 
   sudo /opt/mssql/bin/mssql-conf set EULA accepteulaml Y
   ```
3. Setup detects the mssql-mlservices packages and prompts for EULA acceptance (if not previously accepted) when `mssql-conf setup` is run. For more information about EULA parameters, see [Configure SQL Server with the mssql-conf tool](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

4. Enable outbound network access. Outbound network access is disabled by default. To enable outbound requests, set the "outboundnetworkaccess" Boolean property using the mssql-conf tool. For more information, see [Configure SQL Server on Linux with mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

5. For R feature integration only, set the **MKL_CBWR** environment variable to [ensure consistent output](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) from Intel Math Kernel Library (MKL) calculations.

   + Edit or create a file `named.bash_profile` in your user home directory, adding the line `export MKL_CBWR="AUTO"` to the file.

   + Execute this file by typing `source.bash_profile` at a bash command prompt.

6. Restart the SQL Server Launchpad service and the database engine instance to read the updated values from the INI file. A notification message is displayed when an extensibility-related setting is modified.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

7. Enable external script execution using Azure Data Studio or another tool like SQL Server Management Studio (Windows only) that runs Transact-SQL. 

   ```bash
   EXEC sp_configure 'external scripts enabled', 1 
   RECONFIGURE WITH OVERRIDE 
   ```

7. Restart the Launchpad service again.

## Verify installation

R libraries (MicrosoftML, RevoScaleR, and others) can be found at `/opt/mssql/mlservices/libraries/RServer`.

Python libraries (microsoftml and revoscalepy) can be found at `/opt/mssql/mlservices/libraries/PythonServer`.

To validate installation:

- Run a T-SQL script that executes a system stored procedure invoking Python or R using a query tool. 

For Windows use: 
*  Azure Data Studio
*  SQL Server Management Studio or PowerShell

If you have a Windows computer with these tools, use it to connect to your Linux installation of the database engine.

Execute the following SQL command to test R execution in SQL Server. Errors? Try a service restart, `sudo systemctl restart mssql-server.service`.

```
EXEC sp_execute_external_script   
@language =N'R', 
@script=N' 
OutputDataSet <- InputDataSet', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```
 
Execute the following SQL command to test Python execution in SQL Server. 
 
```python
EXEC sp_execute_external_script  
@language =N'Python', 
@script=N' 
OutputDataSet = InputDataSet; 
', 
@input_data_1 =N'SELECT 1 AS hello' 
WITH RESULT SETS (([hello] int not null)); 
GO 
```

<a name="install-all"></a>

## Unattended installation

Using the [unattended install](https://docs.microsoft.com/sql/linux/sql-server-linux-setup?view=sql-server-2017#unattended) for the Database Engine, add the packages for mssql-mlservices and EULAs.

 Use one of the mlservices-specific EULA parameters for the open-source R and Python distributions:

```bash
sudo /opt/mssql/bin/mssql-conf setup accept-eula-ml
```

The complete EULA is documented at [Configure SQL Server on Linux with the mssql-conf tool](sql-server-linux-configure-mssql-conf.md#mlservices-eula).

## Offline installation

Follow the [Offline installation](sql-server-linux-setup.md#offline) instructions for steps on installing the packages. Download specific packages using the package list below.

> [!Tip]
> Several of the package management tools provide commands that can help you determine package dependencies. For yum, use `sudo yum deplist [package]`. For Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` followed by `dpkg -I [package name].deb`.


#### Download site

Download packages from [https://packages.microsoft.com/](https://packages.microsoft.com/). All of the mlservices packages for Python and R are colocated with database engine package. Base version for the mlservices packages is 9.4.6. Recall that the microsoft-r-open packages are in a [different repository](#mro).

#### RHEL/7 paths

|||
|--|----|
| mssql/mlservices packages | [https://packages.microsoft.com/rhel/7/mssql-server-2019/](https://packages.microsoft.com/rhel/7/mssql-server-2019/) |
| microsoft-r-open packages | [https://packages.microsoft.com/rhel/7/prod/](https://packages.microsoft.com/rhel/7/prod/) | 


#### Ubuntu/16.04 paths

|||
|--|----|
| mssql/mlservices packages | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/) |
| microsoft-r-open packages | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/) | 

#### SLES/12 paths

|||
|--|----|
| mssql/mlservices packages | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |
| microsoft-r-open packages | [https://packages.microsoft.com/sles/12/prod/](https://packages.microsoft.com/sles/12/prod/) |

## Package list

Available installation Packages:

| Package name | Applies-to | Description |
|--------------|----------|-------------|
|mssql-server-extensibility  | All | Extensibility framework used to run Python and R. |
| microsoft-openmpi  | Python, R | Message passing interface used by the Rev* libraries for parallelization on Linux. |
| mssql-mlservices-python | Python | Open-source distribution of Anaconda and Python. |
|mssql-mlservices-mlm-py  | Python | *Full install*. Provides revoscalepy, microsoftml, pre-trained models for image featurization and text sentiment analysis.| 
|mssql-mlservices-packages-py  | Python | *Minimum install*. Provides revoscalepy and microsoftml. <br/>Excludes pre-trained models. | 
| [microsoft-r-open*](#mro) | R | Open-source distribution of R, composed of three packages. |
|mssql-mlservices-mlm-r  | R | *Full install*. Provides: RevoScaleR, MicrosoftML, sqlRUtils, olapR, pre-trained models for image featurization and text sentiment analysis.| 
|mssql-mlservices-packages-r  | R | *Minimum install*. Provides RevoScaleR, sqlRUtils, MicrosoftML, olapR. <br/>Excludes pre-trained models. |

Select extensions you want to use and download the packages necessary for a specific language. The filenames include platform information in the suffix.

File List:

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# R
microsoft-openmpi-3.0.0
microsoft-r-open-mkl-3.5.2
microsoft-r-open-mro-3.5.2
mssql-mlservices-packages-r-9.4.7.64
mssql-mlservices-mlm-r-9.4.7.64


# Python
microsoft-openmpi-3.0.0
mssql-mlservices-python-9.4.7.64
mssql-mlservices-packages-py-9.4.7.64
mssql-mlservices-mlm-py-9.4.7.64
```

## Next steps

R developers can get started with some simple examples, and learn the basics of how R works with SQL Server. For your next step, see the following links:

+ [Tutorial: Run R in T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: In-database analytics for R developers](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)

Python developers can learn how to use Python with SQL Server by following these tutorials:

+ [Tutorial: Run Python in T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: In-database analytics for Python developers](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

To view examples of machine learning that are based on real-world scenarios, see [Machine learning tutorials](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).
