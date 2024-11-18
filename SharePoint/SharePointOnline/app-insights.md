---
ms.date: 11/18/2024
title: "Generate App insights reports"
ms.reviewer: goagarwal
ms.author: mactra
author: MachelleTranMSFT
manager: jtremper
audience: Admin
f1.keywords:
- NOCSH
ms.topic: article
ms.service: sharepoint-online
ms.localizationpriority: medium
ms.collection:
- Highpri
- Tier2
- M365-sam
- M365-collaboration
- SAM-FY25
search.appverid:
recommendations: false
description: "Learn how to generate App insights reports to view how non-Microsoft applications registered on your Microsoft Entra admin center access your SharePoint content."
---

# Generate App insights reports

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

App insights is a [SharePoint Advanced Management](advanced-management.md) feature that lets [IT administrators](/microsoft-365/admin/add-users/about-admin-roles) gain insights on the various non-Microsoft applications registered to your Microsoft Entra admin center and how they access your SharePoint content. This report can help you maintain and protect the integrity of your content.

The report is based on the Microsoft audit data logged when a non-Microsoft application accesses content through the following set of events:

- FileAccessed
- FileDownloaded
- FileModified
- FileUploaded  

## Prerequisites

This feature requires Microsoft SharePoint Premium - SharePoint Advanced Management license.  

## App insights reports in SharePoint admin center

### Create report

1. Sign in to SharePoint admin center with your SharePoint admin credentials.
2. In the left pane, expand **Reports** and then select **App insights**.
3. Once on the **App insights** landing page, select **Add a report** to generate a new report. :::image type="content" alt-text="Screenshot of the create reports page for app insights dashboard in SharePoint admin center." source="media/app-insights/1-enterprise-app-insights-landing-page.png" lightbox="media/app-insights/1-enterprise-app-insights-landing-page.png":::

    Under **Report range**, you can specify and filter data from a respective time frame for your report. :::image type="content" alt-text="Screenshot of the report range for app insights in SharePoint admin center." source="media/app-insights/2-enterprise-app-insights-create-new-report.png" lightbox="media/app-insights/2-enterprise-app-insights-create-new-report.png":::

4. Select **Add and run**.
  
> [!NOTE]
>
> - It can take up to a several hours for generated reports to be available.
> - Only one report is allowed per report range.
> - Reports can be rerun after 24 hours.

### Manage reports in SharePoint admin center

#### View report status

To check if a report is ready or when it was last updated, see the **Status** column. When a report is ready, select it to view the data.

:::image type="content" alt-text="Screenshot of created app insight report in SharePoint admin center." source="media/app-insights/3-enterprise-app-insights-view-report.png" lightbox="media/app-insights/3-enterprise-app-insights-view-report.png":::

You're able to see the top 100 (by request volume) results on the screen.

You can also filter by App name, App permissions, and Site sensitivity to view relevant results form the top 100 rows.

:::image type="content" alt-text="Screenshot of list of insight reports in SharePoint admin center." source="media/app-insights/4-enterprise-app-insights-manage-reports.jpg" lightbox="media/app-insights/4-enterprise-app-insights-manage-reports.jpg":::

> [!IMPORTANT]
> To view up to 1 million results, you must select **Download detailed report**.

#### Delete report

To delete a report, select the existing report you want to delete and select **Delete report**.

#### Rerun a report

To get updated data for a given report range, select an existing report and select **Run**.

> [!TIP]
> A rerun prompt also appears if you select **Add a report** and select a report range for which there already exists a report.  

## App insights reports in SharePoint PowerShell Module

You can generate and manage App insights reports using SharePoint Online Management Shell.

1. [Download](https://go.microsoft.com/fwlink/p/?LinkId=255251) and install the latest version of SharePoint Online Management Shell.
2. Connect to SharePoint Online as a [SharePoint Administrator](sharepoint-admin-role.md) in Microsoft 365. For more information about SharePoint Online Management Shell, see [Getting started with SharePoint Online Management Shell](/powershell/sharepoint/sharepoint-online/connect-sharepoint-online).
3. Ensure you have the SharePoint Premium - SharePoint Advanced Management license.

### PowerShell commands for App insights reports

To perform the necessary operations, use the following commands:

#### Create a one-day default duration report

To generate report for the default duration of one day, run the following command:

```powershell
Start-SPOEnterpriseAppInsightsReport
```

#### Create report for any other duration

To generate report for any other duration, run the following command:

```powershell
Start-SPOEnterpriseAppInsightsReport -ReportPeriodInDays $ReportPeriodInDays (possible values = 1, 7, 14, 28) 
```

#### Check status of all active and available reports

To check status of all active and available reports, run the following command:

```powershell
Get-SPOEnterpriseAppInsightsReport
```

#### Check status of a specific report

To check status of a specific report, run the following command:

```powershell
Get-SPOEnterpriseAppInsightsReport -reportID $reportID (for the given report ID)
```

#### View a specific report

To view a specific report, run the following command:

```powershell
Get-SPOEnterpriseAppInsightsReport -reportID $reportID
```

#### Download a report

To download the report, run the following command:

```powershell
Get-SPOEnterpriseAppInsightsReport -reportID $reportID -action download
```

> [!IMPORTANT]
> Re-run and delete report capabilities are unavailable for PowerShell. The [Create report cmdlets](#create-a-one-day-default-duration-report) can be used with relevant report duration.

## Known experiences

1. In new tenants, it can take a few days for data to be available and for these reports to be generated successfully. In large tenants, the data can be delayed by up to 48 hours (about two days).  
2. A report can be rerun only after 24 hours since the last report generation.
3. There can only be one report for each value of **Report range**. This means that you can see a maximum of four reports in the **Enterprise Application Insights** homepage.
4. These reports are powered by Audit data and don't include all audit events.  
5. You might see App ID of the non-Microsoft app, or App name of a mid-tier app in some cases.
