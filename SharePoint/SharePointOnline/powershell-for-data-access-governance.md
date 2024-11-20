---
ms.date: 11/19/2024
title: "Manage Data access governance reports using SharePoint Online PowerShell"
ms.reviewer: pullabhk
ms.author: mactra
author: MachelleTranMSFT
manager: jtremper
recommendations: true
audience: Admin
f1.keywords: NOCSH
ms.topic: article
ms.service: sharepoint-online
ms.localizationpriority: medium
ms.collection:  
- Strat_SP_admin
- Highpri
- Tier2
- M365-sam
- M365-collaboration
ms.custom:
- seo-marvel-apr2020
- admindeeplinkSPO
search.appverid: MET150
description: "Learn about how to use SharePoint Online PowerShell module to manage Data access governance reports"
---

# Manage Data access governance reports using SharePoint Online PowerShell

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

While [Data access governance](data-access-governance-reports.md) is available in SharePoint admin center portal, large organizations usually look for PowerShell support in order to manage scale via scripting and automation. This document discusses all appropriate PowerShell commands available via SharePoint Online PowerShell module to manage reports from Data access governance.

> [!IMPORTANT]
> PowerShell support for Data access governance is available from module "Microsoft.Online.SharePoint.PowerShell" and version "16.0.25409" onwards.

> [!IMPORTANT]
> Run the ‘Connect-SPOService’ command WITHOUT the **Credential** parameter. We do NOT support login using the **Credential** parameter inline with the latest security practices.

## Creating reports using PowerShell

Use the **Start-SPODataAccessGovernanceInsight** command to generate [all reports](data-access-governance-reports.md#access-the-reports-in-the-sharepoint-admin-center) with appropriate filters and parameters

### Oversharing baseline report using permissions

The definition of 'oversharing' can be different for different customers. Data access governance considers 'number of users' as one possible pivot to establish a baseline and then track key contributors of potential 'oversharing' such as sharing links created and sharing to large groups such as 'Everyone Except External users' in the last 28 days. You can define your threshold of 'number of users' and generate a report of sites that many users access, at the time of report generation. This report is considered a 'snapshot' report.

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity PermissionedUsers -ReportType Snapshot -Workload SharePoint -CountOfUsersMoreThan 100 -Name "ReportForTestingLatestFixes"
```

This command generates a list of all sites where more than 100 users can access any content within the site. More information about the list of sites and how to interpret the results is provided [here](data-access-governance-reports.md#understanding-the-oversharing-baseline-report).

> [!NOTE]
> Currently the report consists of both SharePoint sites and OneDrive accounts and can generate up to 1M sites and/or accounts.

### Sharing link reports

These reports are useful in identifying sites which are active in collaboration and hence needs quicker intervention to mitigate any potential oversharing risk. These 'RecentActivity' based reports identify sites which are generating the most number of sharing links in the last 28 days.

#### Anyone sharing links created in last 28 days

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity SharingLinks_Anyone -Workload SharePoint -ReportType RecentActivity
```

Provide the workload value as 'OneDriveForBusiness' to get all OneDrive accounts with the same criteria.

#### PeopleInYourOrg sharing links created in last 28 days

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity SharingLinks_PeopleInYourOrg -Workload SharePoint -ReportType RecentActivity
```

Provide the workload value as 'OneDriveForBusiness' to get all OneDrive accounts with the same criteria.

#### Specific people (guests) sharing links created in last 28 days

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity SharingLinks_Guests -Workload SharePoint -ReportType RecentActivity
```

Provide the workload value as 'OneDriveForBusiness' to get all OneDrive accounts with the same criteria.

### Content shared with Everyone except external users in last 28 days

While Sharing links are one possible contributor for potential oversharing, another key contributor is 'Everyone except external users' (EEEU) which makes content 'public' that is, visible to entire organization and makes it easy for others to discover content and get access. These reports identify sites which actively used EEEU at various scopes in last 28 days.

#### Sites shared with Everyone except external users in last 28 days

When EEEU is added to a site membership (owners, members, or visitors), the entire content of the site becomes public and more prone to oversharing. The following PowerShell command triggers the report to capture such sites in the last 28 days:

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity EveryoneExceptExternalUsersAtSite -Workload SharePoint -ReportType RecentActivity -Name "PublicSiteViaEEEU"
```

> [!NOTE]
> Currently report for OneDriveForBusiness with EEEU at the site level is not supported.

#### Items shared with Everyone except external users in last 28 days

The following PowerShell command triggers the report to capture sites where specific items (files/folders/lists) were shared with EEEU in the last 28 days:

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity EveryoneExceptExternalUsersAtSite -Workload SharePoint -ReportType RecentActivity -Name "PublicSiteViaEEEU"
```

Provide the workload value as 'OneDriveForBusiness' to get all OneDrive accounts with the same criteria.

### Sensitivity label in files report

This PowerShell command triggers the report to list sites where specific items were labeled with a given 'label', as of report generation date.

First, retrieve the label name or label GUID using "Security and compliance" PowerShell module.

```powershell
Get-Label | Format-Table -Property DisplayName, Name, GUID, ContentType
```

Then, use the Name AND GUID to retrieve sites with files labeled with the given label name or GUID.

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity SensitivityLabelForFiles -Workload SharePoint -ReportType Snapshot -FileSensitivityLabelGUID "a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1" -FileSensitivityLabelName Secret
```

> [!NOTE]
> Currently, the report for 'OneDriveForBusiness' accounts with labelled files is not supported.

## Tracking reports using PowerShell

> [!IMPORTANT]
> All report creations will result in a GUID as output which could be used to track the report status

```powershell
Start-SPODataAccessGovernanceInsight -ReportEntity SensitivityLabelForFiles -Workload SharePoint -ReportType Snapshot -FileSensitivityLabelGUID "a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1" -FileSensitivityLabelName Secret
```

```output
ReportId                             Status
--------                             ------
a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1 NotStarted
```

Use the **Get-SPODataAccessGovernanceInsight** command to retrieve the current status of a specific Data access governance report using the report ID.

```powershell
Get-SPODataAccessGovernanceInsight -ReportID a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
```

```output
ReportId          : a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
ReportEntity      : SharingLinks_Anyone
Status            : InQueue
Workload          : SharePoint
TriggeredDateTime : 11/13/2024 19:32:34
CreatedDateTime   : 11/13/2024 20:09:23
ReportStartTime   : 10/17/2024 19:32:33
ReportEndTime     : 11/13/2024 19:32:33
ReportType        : RecentActivity
SitesFound        : 120
```

The ReportStartTime and ReportEndTime indicate the period of data to generate the report. The status is marked as 'Completed' when the report generation is complete.

You can also view the current status of DAG reports by using the filter **ReportEntity** instead of ID. The reportID is listed in the output and is required later to download a specific report.

```powershell
Get-SPODataAccessGovernanceInsight -ReportEntity PermissionedUsers
```

```output
ReportId             : a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
ReportName           : PermissionReportFor1AsOfSept
ReportEntity         : PermissionedUsers
Status               : Completed
Workload             : SharePoint
TriggeredDateTime    : 09/18/2024 11:06:16
CreatedDateTime      : 09/22/2024 12:12:48
ReportType           : Snapshot
CountOfUsersMoreThan : 1
CountOfSitesInReport : 7
CountOfSitesInTenant : 22
Privacy              : All
Sensitivity          : {All}
Templates            : {All}

ReportId             : b1b1b1b1-cccc-dddd-eeee-f2f2f2f2f2f2
ReportName           : PermissionReportFor1AsOfOct
ReportEntity         : PermissionedUsers
Status               : Completed
Workload             : SharePoint
TriggeredDateTime    : 10/09/2024 14:15:40
CreatedDateTime      : 10/09/2024 15:18:23
ReportType           : Snapshot
CountOfUsersMoreThan : 100
CountOfSitesInReport : 0
CountOfSitesInTenant : 26
Privacy              : All
Sensitivity          : {All}
Templates            : {All}
```

## View and download reports using PowerShell

To download a specific report, you need the reportID. Retrieve the reportID using the **Get-SPODataAccessGovernanceInsight** command and use the **Export-SPODataAccessGovernanceInsight** command to download the report to a specified path.

```powershell
Export-SPODataAccessGovernanceInsight -ReportID a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1 -DownloadPath "C:\Users\TestUser\Documents\DAGReports"
```

This downloads a CSV file to the specified path. Details of the CSV/view for each report are discussed [here](data-access-governance-reports.md#access-the-reports-in-the-sharepoint-admin-center).

> [!NOTE]
> The default download path is the 'Downloads' folder.

## Remedial actions using PowerShell

Once Data access governance reports are generated, SharePoint admins can perform remedial actions as described [here](data-access-governance-reports.md#remedial-actions-from-data-access-governance-reports). The following section describes PowerShell commands to trigger and track 'site access review' as a remedial action.

### Initiate Site access review using PowerShell

Use **Start-SPOSiteReview** command to initiate a site access review for a specific site, listed under a Data access governance report. The Data access governance report provides the context under which the review should be initiated. Retrieve the reportID, site ID from the CSV file and provide comments to give clarity to the site owner regarding the purpose of the review.

```powershell
Start-SPOSiteReview -ReportID a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1 -SiteID c2c2c2c2-dddd-eeee-ffff-a3a3a3a3a3a3 -Comment "Check for org wide access"
```

```output
ReviewId                : a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
SiteId                  : c2c2c2c2-dddd-eeee-ffff-a3a3a3a3a3a3
ReviewInitiatedDateTime : 13-11-2024 20:55:41
ReportEntity            : PermissionedUsers
Status                  : Pending
AdminComment            : Check for org wide access
SiteName                : All Company
```

This triggers emails to site owner as described [here](site-access-review.md#how-to-initiate-a-site-access-review).

### Track Site access reviews using PowerShell

Use **Start-SPOSiteReview** command to track the status of site access reviews. For specific reviews, you can use the `ReviewID` value as shown in the output. To retrieve all review related to a reporting module, use the `ReportEntity` parameter.

```powershell
Get-SPOSiteReview -ReportEntity PermissionedUsers
```

```output
ReviewId                : a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
SiteId                  : c2c2c2c2-dddd-eeee-ffff-a3a3a3a3a3a3
ReviewInitiatedDateTime : 13-11-2024 20:55:41
ReviewCompletedDateTime :
ReportCreatedDateTime   : 13-11-2024 23:25:41
ReportEndDateTime       : 13-11-2024 23:25:41
ReportEntity            : PermissionedUsers
Status                  : Pending
AdminComment            : Check for org wide access
SiteName                : All Company
ReviewerEmail           :
ReviewerComment         :

ReviewId                : a0a0a0a0-bbbb-cccc-dddd-e1e1e1e1e1e1
SiteId                  : c2c2c2c2-dddd-eeee-ffff-a3a3a3a3a3a3
ReviewInitiatedDateTime : 24-10-2024 11:07:39
ReviewCompletedDateTime : 15-11-2024 11:07:39
ReportCreatedDateTime   : 15-10-2024 09:24:47
ReportEndDateTime       : 15-10-2024 11:39:52
ReportEntity            : PermissionedUsers
Status                  : Completed
AdminComment            : Check for org wide access
SiteName                : All Company
ReviewerEmail           : Jon@contosofinance.com
ReviewerComment         : Removed EEEU for sensitive documents
```
