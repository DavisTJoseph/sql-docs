---
title: "OLE DB Connection Manager | Microsoft Docs"
ms.custom: ""
ms.date: "05/24/2019"
ms.prod: sql
ms.prod_service: "integration-services"
ms.reviewer: ""
ms.technology: integration-services
ms.topic: conceptual
f1_keywords: 
  - "sql13.dts.designer.oledbconnection.f1"
helpviewer_keywords: 
  - "OLE DB connection manager"
  - "data sources [Integration Services], connections"
  - "connection managers [Integration Services], OLE DB"
  - "connections [Integration Services], OLE DB"
ms.assetid: 91e3622e-4b1a-439a-80c7-a00b90d66979
author: janinezhang
ms.author: janinez
manager: craigg
---
# OLE DB Connection Manager

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  An OLE DB connection manager enables a package to connect to a data source by using an OLE DB provider. For example, an OLE DB connection manager that connects to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can use the [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].    
    
> [!NOTE]
>  The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11.0 OLEDB provider does not support the new connection string key words (MultiSubnetFailover=True) for Multi-Subnet Failover Clustering. For more information, see the [SQL Server Release  Notes](https://go.microsoft.com/fwlink/?LinkId=247824) and the blog post, [Always On Multi-Subnet Failover and SSIS](https://www.mattmasson.com/2012/03/alwayson-multi-subnet-failover-and-ssis/), on www.mattmasson.com.    
> 
> [!NOTE]
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 or [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, the data source requires a different data provider than earlier versions of Excel or Access. For more information, see [Connect to an Excel Workbook](../../integration-services/connection-manager/connect-to-an-excel-workbook.md) and [Connect to an Access Database](../../integration-services/connection-manager/connect-to-an-access-database.md).    
    
 Several [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tasks and data flow components use an OLE DB connection manager. For example, the OLE DB source and OLE DB destination use this connection manager to extract and load data, and the Execute SQL task can use this connection manager to connect to a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database to run queries.    
    
 The OLE DB connection manager is also used to access OLE DB data sources in custom tasks written in unmanaged code that uses a language such as C++.    
    
 When you add an OLE DB connection manager to a package, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creates a connection manager that will resolve to an OLE DB connection at run time, sets the connection manager properties, and adds the connection manager to the **Connections** collection on the package.    
    
 The **ConnectionManagerType** property of the connection manager is set to **OLEDB**.    
    
 The OLE DB connection manager can be configured in the following ways:    
    
-   Provide a specific connection string configured to meet the requirements of the selected provider.    
    
-   Depending on the provider, include the name of the data source to connect to.    
    
-   Provide security credentials as appropriate for the selected provider.    
    
-   Indicate whether the connection that is created from the connection manager is retained at run time.    
    
## Logging    
 You can log the calls that the OLE DB connection manager makes to external data providers. You can use this logging capability to troubleshoot the connections that the OLE DB connection manager makes to external data sources. To log the calls that the OLE DB connection manager makes to external data providers, enable package logging and select the **Diagnostic** event at the package level. For more information, see [Troubleshooting Tools for Package Execution](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).    
    
## Configuration of the OLEDB Connection Manager    
 You can set properties through [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer or programmatically. For more information about the properties that you can set in [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, see [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md). For information about configuring a connection manager programmatically, see the documentation for **T:Microsoft.SqlServer.Dts.Runtime.ConnectionManager** class in the Developer Guide.    
    
## Related Content    
    
-   Wiki article, [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670) on social.technet.microsoft.com.    
    
-   Technical article, [Connection Strings for OLE DB Providers](https://go.microsoft.com/fwlink/?LinkId=220744), on carlprothman.net.    
    
## Configure OLE DB Connection Manager
  Use the **Configure OLE DB Connection Manager** dialog box to add a connection to a data source, which can be either a new connection or a copy of an existing connection.  
  
> [!NOTE]  
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, the data source requires a different connection manager than earlier versions of Excel. For more information, see [Connect to an Excel Workbook](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
>   
>  If the data source is [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 2007, the data source requires a different OLE DB provider than earlier versions of Access. For more information, see [Connect to an Access Database](../../integration-services/connection-manager/connect-to-an-access-database.md).  
  
 To learn more about the OLE DB connection manager, see [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
### Options  
 **Data connections**  
 Select an existing OLE DB data connection from the list.  
  
 **Data connection properties**  
 View properties and values for the selected OLE DB data connection.  
  
 **New**  
 Create an OLE DB data connection by using the **Connection Manager** dialog box.  
  
 **Delete**  
 Select a data connection, and then delete it by using the **Delete** button.  
  
### Managed Identities for Azure Resources Authentication
When running SSIS packages on [Azure-SSIS integration runtime in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime), you can use the [managed identity](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) that is associated with your data factory for Azure SQL Database (or Managed Instance) authentication. The designated factory can access and copy data from or to your database by using this identity.

To use managed identity authentication for Azure SQL Database, follow these steps to configure your database:

1. **Create a group in Azure AD.** Make the managed identity a member of the group.
    
   1. [Find the data factory managed identity from the Azure portal](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity). Go to your data factory's **Properties**. Copy the **Managed Identity Object ID**.
    
   1. Install the [Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2) module. Sign in by using the `Connect-AzureAD` command. Run the following commands to create a group and add the managed identity as a member.
      ```powershell
      $Group = New-AzureADGroup -DisplayName "<your group name>" -MailEnabled $false -SecurityEnabled $true -MailNickName "NotSet"
      Add-AzureAdGroupMember -ObjectId $Group.ObjectId -RefObjectId "<your data factory managed identity object ID>"
      ```
    
1. **[Provision an Azure Active Directory administrator](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-azure-sql-database-server)** for your Azure SQL server on the Azure portal if you haven't already done so. The Azure AD administrator can be an Azure AD user or Azure AD group. If you grant the group with managed identity an admin role, skip steps 3 and 4. The administrator will have full access to the database.

1. **[Create contained database users](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#create-contained-database-users-in-your-database-mapped-to-azure-ad-identities)** for the Azure AD group. Connect to the database from or to which you want to copy data by using tools like SSMS, with an Azure AD identity that has at least ALTER ANY USER permission. Run the following T-SQL: 
    
    ```sql
    CREATE USER [your AAD group name] FROM EXTERNAL PROVIDER;
    ```

1. **Grant the Azure AD group needed permissions** as you normally do for SQL users and others. For example, run the following code:

    ```sql
    ALTER ROLE [role name] ADD MEMBER [your AAD group name];
    ```

To use managed identity authentication for Azure SQL Database Managed Instance, follow these steps to configure your database:
    
1. **[Provision an Azure Active Directory administrator](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure#provision-an-azure-active-directory-administrator-for-your-managed-instance)** for your managed instance on the Azure portal if you haven't already done so. The Azure AD administrator can be an Azure AD user or Azure AD group. If you grant the group with managed identity an admin role, skip steps 2-5. The administrator will have full access to the database.

1. **[Find the data factory managed identity from the Azure portal](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)**. Go to your data factory's **Properties**. Copy the **Managed Identity Application ID** (NOT **Managed Identity Object ID**).

1. **Convert the data factory managed identity to binary type**. Connect to **master** database in your managed instance by using tools like SSMS, with your SQL/Active Directory admin account. Run the following T-SQL against **master** database to get your managed identity application ID as binary:
    
    ```sql
    DECLARE @applicationId uniqueidentifier = '{your managed identity application ID}'
    select CAST(@applicationId AS varbinary)
    ```

1. **Add the data factory managed identity as a user** in Azure SQL Database Managed Instance. Run the following T-SQL against **master** database:
    
    ```sql
    CREATE LOGIN [{a name for the managed identity}] FROM EXTERNAL PROVIDER with SID = {your managed identity application ID as binary}, TYPE = E
    ```

1. **Grant the data factory managed identity needed permissions**. Run the following T-SQL against the database from or to which you want to copy data:

    ```sql
    CREATE USER [{the managed identity name}] FOR LOGIN [{the managed identity name}] WITH DEFAULT_SCHEMA = dbo
    ALTER ROLE db_owner ADD MEMBER [{the managed identity name}]
    ```

Then **configure OLE DB provider** for the OLE DB connection manager. There are two options to do this.
    
1. Configure at design time. In SSIS Designer, double-click the OLE DB connection manager to open the **Connection Manager** window. In the **Provider** drop-down list, select [**Microsoft OLE DB Driver for SQL Server**](https://go.microsoft.com/fwlink/?linkid=871294).
    > [!NOTE]
    >  Other providers in the drop-down list MIGHT NOT support managed identity authentication.
    
1. Configure at run time. When you execute the package via [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) or [Azure Data Factory Execute SSIS Package activity](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity), find the connection manager property **ConnectionString** for the OLE DB connection manager and update the connection property **Provider** to **MSOLEDBSQL** (i.e, Microsoft OLE DB Driver for SQL Server).
    ```vb
    Data Source=serverName;Initial Catalog=databaseName;Provider=MSOLEDBSQL;...
    ```

Finally **configure managed identity authentication** for the OLE DB connection manager. There are two options to do this.
    
1. Configure at design time. In SSIS Designer, right-click the OLE DB connection manager and click **Properties** to open the **Properties Window**. Update the property **ConnectUsingManagedIdentity** to **True**.
    > [!NOTE]
    >  Currently the connection manager property **ConnectUsingManagedIdentity** DOES NOT take effect (indicating that managed identity authentication does not work) when you run SSIS package in SSIS Designer or [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server.

1. Configure at run time. When you execute the package via SSMS or Execute SQL Package activity, find the OLE DB connection manager and update its property **ConnectUsingManagedIdentity** to **True**.
    > [!NOTE]
    >  In Azure-SSIS integration runtime, all other authentication methods (e.g., integrated security, password) preconfigured on the OLE DB connection manager will be **overridden** when managed identity authentication is used to establish database connection.

> [!NOTE]
>  To configure managed identity authentication on existing packages, please be sure to rebuild your SSIS project with the [latest SSIS Designer](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt) at least once and redeploy that SSIS project to your Azure-SSIS integration runtime so that the new connection manager property **ConnectUsingManagedIdentity** will automatically be added to all OLE DB connection managers in your SSIS project.

## See Also    
 [OLE DB Source](../../integration-services/data-flow/ole-db-source.md)     
 [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md)     
 [Execute SQL Task](../../integration-services/control-flow/execute-sql-task.md)     
 [Integration Services &#40;SSIS&#41; Connections](../../integration-services/connection-manager/integration-services-ssis-connections.md)    
    
  
