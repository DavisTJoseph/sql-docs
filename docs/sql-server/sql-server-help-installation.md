---
title: Install previous versions of SQL Server help content to view offline
ms.prod: sql
ms.technology: 
ms.reviewer: ""
ms.topic: conceptual
ms.assetid: 51f8a08c-51d0-41d8-8bc5-1cb4d42622fb
author: markingmyname
ms.author: maghan
ms.custom: ""
ms.date: 04/20/2020
---

# Install previous versions of SQL Server help content to view offline

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

This article describes how to download and view offline SQL Server content in [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md).

Offline documentation for older versions of Microsoft SQL Server is still available.

Internet access is required to download the SQL Server content. You can then migrate the content to a computer that doesn't have internet access.

Offline content is available for these SQL Server versions:

- SQL Server 2019
- SQL Server 2017
- SQL Server 2016
- SQL Server 2014
- SQL Server 2012

## How to download and configure offline content

You can use download and install SQL Server help packages from online sources or local disk.

Below are steps on how to load offline content for different versions of SQL Server.

### Add SQL Server 2019 offline content

For this approach, you use the **Online** Installation source.

1. In SSMS, select **Add and Remove Help Content** on the Help menu.

   ![Help Viewer Add Remove Content](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   The Help Viewer opens to the Manage Content tab.

2. To find the latest help content for SQL Server 2019, under the **Manage Content** tab choose **Online** under the Installation source and then type in *sql server 2019* in the search bar.

   ![SQL Server 2019 documentation search in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-search.png)

   > [!Note]
   > The Local store path on the Manage Content tab shows where on the local computer the content is installed. To change the location, select **Move**, enter a different folder path in the **To** field, and then select **OK**. If the help installation fails after changing the Local store path, close and reopen Help Viewer. Ensure the new location appears in the Local store path and then try the installation again.

3. To install the latest help content for SQL Server 2019, select **Add** next to each content package (book) that you want to install and then select **Update** in the lower right.

   ![SQL Server 2019 books add and update in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2019-add-update.png)

   > [!NOTE]
   > If the Help Viewer freezes (hangs) while adding content, change the Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" line in the %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings file to some date in the future. For more information about this issue, see [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio).

4. You can verify that the SQL Server 2019 content is loaded by searching under the content pane on the left for *sql server 2019*.

   ![SQL Server 2019 books automatically updated](../sql-server/media/sql-server-help-installation/sql-2019-content.png)

### Add SQL Server 2017 offline content

For this approach, you use the **Online** Installation source.

1. In SSMS, select **Add and Remove Help Content** on the Help menu.

   ![Help Viewer Add Remove Content](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   The Help Viewer opens to the Manage Content tab.

2. To find the latest help content for SQL Server 2017, under the **Manage Content** tab choose **Online** under the Installation source and then type in *sql server 2017* in the search bar.

   ![SQL Server 2017 books search in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-search.png)

   > [!Note]
   > The Local store path on the Manage Content tab shows where on the local computer the content is installed. To change the location, select **Move**, enter a different folder path in the **To** field, and then select **OK**. If the help installation fails after changing the Local store path, close and reopen Help Viewer. Ensure the new location appears in the Local store path and then try the installation again.

3. To install the latest help content for SQL Server 2017, select **Add** next to each content package (book) that you want to install and then select **Update** in the lower right.

   ![SQL Server 2017 books add and update in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2017-add-update.png)

   > [!NOTE]
   > If the Help Viewer freezes (hangs) while adding content, change the Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" line in the %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings file to some date in the future. For more information about this issue, see [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio).

4. You can verify that the SQL Server 2017 content is loaded by searching under the content pane on the left for *sql server 2017*.

   ![SQL Server 2017 books automatically updated](../sql-server/media/sql-server-help-installation/sql-2017-content.png)

### Add SQL Server 2016 offline content

For this approach, you use the **Online** Installation source.

1. In SSMS, select **Add and Remove Help Content** on the Help menu.

   ![Help Viewer Add Remove Content](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   The Help Viewer opens to the Manage Content tab.

2. To find the latest help content for SQL Server 2016, under the **Manage Content** tab choose **Online** under the Installation source and then type in *sql server 2016* in the search bar.

   ![SQL Server 2016 books search in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-search.png)

   > [!Note]
   > The Local store path on the Manage Content tab shows where on the local computer the content is installed. To change the location, select **Move**, enter a different folder path in the **To** field, and then select **OK**. If the help installation fails after changing the Local store path, close and reopen Help Viewer. Ensure the new location appears in the Local store path and then try the installation again.

3. To install the latest help content for SQL Server 2016, select **Add** next to each content package (book) that you want to install and then select **Update** in the lower right.

   ![SQL Server 2016 books add and update in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2016-add-update.png)

   > [!NOTE]
   > If the Help Viewer freezes (hangs) while adding content, change the Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" line in the %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings file to some date in the future. For more information about this issue, see [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio).

4. You can verify that the SQL Server 2016 content is loaded by searching under the content pane on the left for *sql server 2016*.

   ![SQL Server 2016 books automatically updated](../sql-server/media/sql-server-help-installation/sql-2016-content.png)

### Add SQL Server 2014 offline content

For this approach, you use the **Disk** Installation source.

1. Download the [Product Documentation for Microsoft SQL Server 2014 for firewall and proxy restricted environments](https://www.microsoft.com/download/details.aspx?id=42557) content from the download center and save it to a folder.

2. Unzip the file to view the.msha file.

   ![SQL Server 2014 Help documentation setup file](../sql-server/media/sql-server-help-installation/sql-2014-help-content-setup-msha.png)

3. In SSMS, select **Add and Remove Help Content** on the Help menu.

   ![HelpViewer Add Remove Content](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   The Help Viewer opens to the Manage Content tab.

4. To install the latest help content, choose **Disk** under Installation source and then the ellipses (...).

   ![Help Viewer Manage Content Disk Source](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > The Local store path on the Manage Content tab shows where on the local computer the content is located. To change the location, select **Move**, enter a different folder path in the **To** field, and then select **OK**.
   If the help installation fails after changing the Local store path, close and reopen the Help Viewer. Ensure the new location appears in the Local store path and then try the installation again.

5. Locate the folder where you unzipped the content. Select the **HelpContentSetup.msha** file in the folder then select **Open**.

   ![Open the SQL Server 2014 Help Content Setup.msha file](../sql-server/media/sql-server-help-installation/sql-2014-open-msha.png)

6. Type in *sql server 2014* in the search bar. Once you see the 2014 content available, select **Add** next to each content package (book) that you want to install to Help Viewer and then select **Update**.

   ![SQL Server 2014 books search in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-search.png)

   ![SQL Server 2014 books add and update in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2014-add-update.png)

    > [!NOTE]
    > If the Help Viewer freezes (hangs) while adding content, change the Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" line in the %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings file to some date in the future. For more information about this issue, see [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio).

7. You can verify that the SQL Server 2014 content installed by searching under the content pane on the left for *sql server 2014*.

   ![SQL Server 2014 books automatically updated](../sql-server/media/sql-server-help-installation/sql-2014-content.png)

### Add SQL Server 2012 offline content

For this approach, you use the **Disk** Installation source.

1. Download the [Product Documentation for Microsoft SQL Server 2012 for firewall and proxy restricted environments](https://www.microsoft.com/download/details.aspx?id=35750) content from the download center and save it to a folder.

2. Unzip the file to view the.msha file.

   ![SQL Server 2012 Help content setup file](../sql-server/media/sql-server-help-installation/sql-2012-help-content-setup-msha.png)

3. In SSMS, select **Add and Remove Help Content** on the Help menu.

   ![HelpViewer Add Remove Content](../sql-server/media/sql-server-help-installation/add-remove-content.png)

   The Help Viewer opens to the Manage Content tab.

4. To install the latest help content, choose **Disk** under Installation source and then the ellipses (...).

   ![Help Viewer Manage Content Disk Source](../sql-server/media/sql-server-help-installation/install-source-disk.png)

   > [!NOTE]
   > The Local store path on the Manage Content tab shows where on the local computer the content is located. To change the location, select **Move**, enter a different folder path in the **To** field, and then select **OK**.
   If the help installation fails after changing the Local store path, close and reopen the Help Viewer. Ensure the new location appears in the Local store path and then try the installation again.

5. Locate the folder where you unzipped the content. Select the **HelpContentSetup.msha** file in the folder then select **Open**.

   ![Open the SQL Server 2012 Help Content Setup.msha file](../sql-server/media/sql-server-help-installation/sql-2012-open-msha.png)

6. Type in *sql server 2012* in the search bar. Once you see the 2012 content available, select **Add** next to each content package (book) that you want to install to Help Viewer and then select **Update**.

   ![SQL Server 2012 books search in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-search.png)

   ![SQL Server 2012 books add and update in Help Viewer](../sql-server/media/sql-server-help-installation/sql-2012-add-update.png)

    > [!NOTE]
    > If the Help Viewer freezes (hangs) while adding content, change the Cache LastRefreshed="\<mm/dd/yyyy> 00:00:00" line in the %LOCALAPPDATA%\Microsoft\HelpViewer2.x\HlpViewer_SSMSx_en-US.settings or HlpViewer_VisualStudiox_en-US.settings file to some date in the future. For more information about this issue, see [Visual Studio Help Viewer freezes](/visualstudio/welcome-to-visual-studio).

7. You can verify that the SQL Server 2012 content is loaded by searching under the content pane on the left for *sql server 2012*.

   ![SQL Server 2012 documentation automatically updated](../sql-server/media/sql-server-help-installation/sql-2012-content.png)

## View offline SQL Server docs

You can view SQL Server help content using the **HELP** menu in the latest version of [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md).

### View offline help content in SSMS

To view the installed help in SSMS, select **Launch in Help Viewer** from the Help menu, to launch the Help Viewer.

   ![Launch in Help Viewer](../sql-server/media/sql-server-help-installation/helpviewer-view-offline.png)  

Help Viewer opens to the Manage Content tab, with the installed help table of contents in the left pane. select articles in the table of contents to display them in the right pane.

> [!TIP]
> If the contents pane is not visible, select Contents on the left margin. select the pushpin icon to keep the contents pane open.  

   ![Help Viewer with content](../sql-server/media/sql-server-help-installation/view-offline-all.png)

## Life-cycle policy

Review the Microsoft Product Lifecycle for information about how a specific product, service, or technology is supported:

- [Microsoft Lifecycle Policy](https://support.microsoft.com/lifecycle/selectindex)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## Next steps

To learn more about archived content and about Help viewer, please reference the links below.

- [A direct link to previous versions of SQL Server documentation](https://docs.microsoft.com/previous-versions/sql/)
- [Microsoft Help Viewer - Visual Studio](https://docs.microsoft.com/visualstudio/help-viewer/overview)
- [SQL Server Documentation, start](../sql-server/index.yml?view=sql-server-2016)
- [Versioning system for SQL documentation](../sql-server/versioning-system-monikers-ui-sql-server.md?view=sql-server-2016)