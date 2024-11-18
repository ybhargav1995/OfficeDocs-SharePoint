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
- MET150
recommendations: false
description: "Learn how to generate App insights reports and learn how Microsoft Entra third-party applications access your SharePoint content."
---

# Generate App insights reports

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

App Insights is a [SharePoint Advanced Management](advanced-management.md) feature that lets [IT administrators](/microsoft-365/admin/add-users/about-admin-roles) gain insights into the various Microsoft Entra third-party applications accessing SharePoint content. This report can help you maintain and protect the integrity of your content.

The report is based on the Microsoft audit data logged when a third-party application accesses content via the below set of events:

- FileAccessed
- FileDownloaded
- FileModified
- FileUploaded  

## Prerequisites

This feature requires Microsoft SharePoint Premium - SharePoint Advanced Management license.  

## Create report in SharePoint admin center

1. Sign in to SharePoint admin center with your SharePoint admin credentials your organization.
2. In the left pane, expand **Reports** and then select **App insights**.
3. Once on the **App insights** landing page, select **Add a report** to generate a new report. Under **Report range**, you can specify and filter data from a respective time frame for your report.
4. Select **Add and run**.
  
It can take up to a several hours for generated report to be available.  
Note: Only one report is allowed per report range, and reports can be re-run after 24 hours.  


:::image type="content" alt-text="Screenshot of site lifecycle management insights dashboard in SharePoint admin center." source="media/ai-insights/0-ai-insights-inactive-sites.png" lightbox="media/ai-insights/0-ai-insights-inactive-sites.png":::