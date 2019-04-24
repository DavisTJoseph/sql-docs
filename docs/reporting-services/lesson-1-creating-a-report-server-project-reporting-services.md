---
title: "Lesson 1: Creating a Report Server Project (Reporting Services) | Microsoft Docs"
ms.date: 04/22/2019
ms.prod: reporting-services
ms.prod_service: "reporting-services-native"
ms.technology: reporting-services

ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
---
# Lesson 1: Creating a Report Server Project (Reporting Services)

In this lesson, you'll create a *report server project* and a *report definition (.rdl)* file in [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)] within Visual Studio.  

To create a report with [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], first you need a report server project where you can save your report definition (.rdl) file and other resource files you need for your report.  

In the following lessons, you define a data source for your report, define a dataset, and define the report layout. When you run the report, the data is retrieved and combined with the layout, and then rendered on your screen. From there you can export it, print it, or save it.  
  
## To create a report server project  
  
1. Open [!INCLUDE[ssBIDevStudio_md](../includes/ssbidevstudio-md.md)].  
  
2. On the **File** menu select > **New** > **Project**.  

    ![ssrs-ssdt-file-01-new-project](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
3. Under **Installed** > **Templates** select **Reporting Services**.

    <!-- ![ssrs-ssdt-01-new-rs-project](../reporting-services/media/ssrs-ssdt-01-new-rs-project.png) -->
    ![select-report-server-project-template](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

   >**Note**: If you don't see the **Reporting Services** or **Report Server Project** options, you need to update Report Designer with the Reporting Services templates. See [Download SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  
  
4. Select the **Report Server Project** icon &nbsp;&nbsp;![ssrs_ssdt_report_server_project](../reporting-services/media/ssrs-ssdt-report-server-project.png) &nbsp;&nbsp;in the center template display area.

5. In the **Name** text box, type **Tutorial**. By default, it's created in your "visual studio 2017\projects" folder in a new directory.

6. Select **OK** to create the project. The Tutorial project is displayed in the Solution Explorer pane on the right.
  
## To create a new report definition file  
  
1. In the **Solution Explorer** pane, right-click the **Reports** > **Add** > **New Item**.

    >**Tip**: If you don't see the **Solution Explorer** pane, on the **View** menu, select the **Solution Explorer** tab on the far right.

    ![ssrs_ssdt_add_report](../reporting-services/media/ssrs-ssdt-add-report.png)
  
2. In the **Add New Item** window, select the **Report** icon &nbsp;&nbsp;![ssrs_ssdt_report](../reporting-services/media/ssrs-ssdt-report.png).  
3. In the **Name** text box type **Sales Orders.rdl** and then select **Add**.  
  
    Report Designer opens and displays the new .rdl file in Design view.  

    ![ssrs-ssdt-01-new-report-designer](../reporting-services/media/ssrs-ssdt-01-new-report-designer.png)
  
     Report Designer is a [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] component that runs in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. It has **Design** and **Preview** views. Select the appropriate tab to change views.  
  
    You define your data in the **Report Data** pane. You define your report layout in **Design** view. You can run the report and see what it looks like in **Preview** view.  
  
## Next lesson

You have successfully created a report project called "Tutorial" and added a report definition (.rdl) file to the report project. Next, you will specify a data source to use for the report. See [Lesson 2: Specifying Connection Information &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md).  
  
## See Also

[Create a Basic Table Report &#40;SSRS Tutorial&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
