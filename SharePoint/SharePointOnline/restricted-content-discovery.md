---
ms.date: 11/14/2024
title: "Restrict discovery of SharePoint sites and content"
ms.reviewer: nibandyo
manager: jtremper
recommendations: true 
ms.author: mactra
author: MachelleTranMSFT
audience: Admin
f1.keywords: 
- NOCSH 
ms.topic: article
ms.service: sharepoint-online
ms.localizationpriority: medium
ms.custom:
  - has-azure-ad-ps-ref
ms.collection: 
- M365-collaboration
- M365-SAM
- Tier2
search.appverid:
description: "Learn how to restrict the discovery of SharePoint sites from Microsoft 365 Copilot Business Chat and tenant-wide search."
---

# Restrict discovery of SharePoint sites and content

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

For organizations onboarding to Microsoft 365 Copilot, maintaining strong data governance controls for SharePoint content is critical to deploying Copilot in a safe manner. Sites identified with the highest risk of oversharing can use Restricted Content Discovery to protect content while taking time to ensure that permissions are accurate and well-managed.

## What is Restricted Content Discovery?

With Restricted Content Discovery, organizations can limit the ability of end users to search for files from specific SharePoint sites. Enabling Restricted Content Discovery for each site prevents the sites from surfacing in organization-wide search and Microsoft 365 Copilot Business Chat, unless a user had a recent interaction.  

> [!NOTE]
> Restricted Content Discovery does not impact existing permissions on sites. Users with access can still open files on sites with Restricted Content Discovery toggled on.

While child content is hidden by default, users in your organization can still discover files they own or recently interacted with. End users can still find relevant content they need for their day-to-day tasks, even if Restricted Content Discovery is applied to the parent site.

Restricted Content Discovery doesn't affect searches originating from a site context or other intelligent features such as Microsoft 365 Feed and Recommendations.

## Use cases for Restricted Content Discovery

Restricted Content Discovery can be applied to any SharePoint site in your organization. The key use case for this feature is to prevent accidental discovery of high-risk sites.

We recommend using tools such as Data access governance reports and SharePoint admin center's **Active sites** tab to first compile a selective list of targeted sites.

> [!NOTE]
> This feature can't be applied to OneDrive sites.

> [!CAUTION]
> Overuse of Restricted Content Discovery can negatively affect performance across search, SharePoint, and Copilot. Removing sites or files from tenant-wide discovery means that there's less content for search and Copilot to ground on, leading to inaccurate or incomplete results.

Restricted Content Discovery is a site-level setting that needs to be propagated to the search index, a large number of transactions could lead to a long queue in the ingestion pipeline and higher update latency times.

## Prerequisites

The Restricted Content Discover policy requires the following prerequisites:

- Have a [Microsoft SharePoint Premium - SharePoint Advanced Management subscription](advanced-management.md).
- Download and install the latest version of SharePoint Online Management Shell.
- Connect to SharePoint Online as a SharePoint Administrator in Microsoft 365.

## Configure Restricted Content Discovery

By default, Restricted Content Discovery is off for all sites. As an IT administrator, you can enable or disable this feature, and check the current state of a given site.

### Enable Restricted Content Discovery for a site

Complete the following steps to apply Restricted Content Discovery on a site:

To apply Restricted Content Discovery on a SharePoint site, run the following command:

```powershell
Set-SPOSite –identity <site-url> -RestrictContentOrgWideSearch $true
```

### Check the state of Restricted Content Discovery

Check for the state of Restricted Content Discovery with the following command:

```powershell
Get-SPOSite –identity <site-url> | Select RestrictContentOrgWideSearch
```

### Remove Restricted Content Discovery from a site

To remove Restricted Content Discovery on a SharePoint site, run the following command:

```powershell
Set-SPOSite –identity <site-url> -RestrictContentOrgWideSearch $false
```

## Next steps

Restricted Content Discovery gives organizations time to review and/or audit permissions and deploy access controls while onboarding Copilot in a safe manner.

Ultimately for sites that are overshared, the goal is to ensure that proper controls are in place to manage access. SharePoint Advanced Management has a suite of features, such as advanced site content lifecycle management, to help site owners and admins create a robust SharePoint governance framework.

## Frequently Asked Questions

**Is my organization eligible to use Restricted Content Discovery?**

Customers who are licensed for Copilot and have SharePoint Advanced Management available to them can configure Restricted Content Discovery.

**What search scenarios enforce Restricted Content Discovery?**

Restricted Content Discovery only affects tenant-wide search (SharePoint home, Office.com, Bing) and Microsoft 365 Copilot. Only Copilot Discovery scenarios are in scope; Copilot experiences that use data-in-use, such as "summarize the current document" in Word aren't impacted.  

**Does Restricted Content Discovery impact other features with dependencies on the search index, such as the Microsoft Purview product suite?**

No, Restricted Content Discovery doesn't remove content from the tenant search index, which means Microsoft Purview features such as eDiscovery and autolabeling aren't impacted.

**How soon can I expect Search and Copilot to reflect an update made to the Restricted Content Discovery configuration of a site?**

Restricted Content Discovery is a site-level property. Index update latency is highly dependent on the number of items in the site and the number of sites getting updated at the same time. For sites with more than 500,000 items, the Restricted Content Discovery update could take more than a week to fully process and reflect in search and Copilot.

**How does Restricted Content Discovery affect the end user experience in Copilot?**

Based on usage of this feature, Copilot has less information available to reference, which could negatively affect its ability to provide accurate and comprehensive responses.

**How does Restricted Content Discovery fit into an overall approach to prepare SharePoint data for Microsoft 365 Copilot?**

Restricted Content Discovery is designed to limit the ability of end users to search for content from specific SharePoint sites. For a more comprehensive guidance on preparing your data for Copilot, check out this [blueprint](https://aka.ms/Copilot/OversharingBlueprintLearn).

## Related topics

[Overview of SharePoint Advanced Management](advanced-management.md)

[Manage access agents in SharePoint](manage-access-agents-in-sharepoint.md)
