---
ms.date: 10/30/2024
title: "Manage inactive site policies with Site lifecycle management"
ms.reviewer: nvasudevan
manager: jtremper
recommendations: true 
ms.author: mactra
author: MachelleTranMSFT
audience: Admin
f1.keywords: 
- NOCSH 
ms.topic: how-to
ms.service: sharepoint-online
ms.localizationpriority: medium
ms.collection: 
- Highpri
- Tier2
- M365-sam
- M365-collaboration
- essentials-manage
search.appverid:
description: "Learn how to manage inactive site policies for SharePoint sites using Site lifecycle management."
---

# Manage inactive site policies with Site lifecycle management

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

The site lifecycle management feature in Microsoft SharePoint Premium - SharePoint Advanced Management allows you to manage inactive sites across your tenant from the [SharePoint admin center](get-started-new-admin-center.md).

## Types of inactive site policies

You can set up an inactive site policy to automatically detect inactive sites and notify site owners via email. Owners can then confirm if the site is still active. When setting up a site lifecycle policy, you can choose between a simulation policy and an active policy. The simulation policy runs once and generates a report based on the set parameters. If it fails, you need to delete it and create a new one. You can also convert a simulation policy to an active policy.

The active policy runs monthly, generating reports and sending notifications to site owners to confirm the site's status. If it fails during a particular month, it will run again on the next schedule. The active policy enforces actions on inactive sites that haven't been certified by the site owner or admin, provided you've configured it to take enforcement actions.

:::image type="content" source="media/site-lifecycle-management/1-inactive-site-policy-dashboard.png" alt-text="screenshot of site lifecycle management dashboard" lightbox="media/site-lifecycle-management/1-inactive-site-policy-dashboard.png":::

## Requirements

Site lifecycle management requires a [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md) subscription.

## Create an inactive site policy

To create an inactive site policy, follow these steps:

1. Go to the SharePoint admin center.

1. Expand **Policies** and select **Site lifecycle management**.

1. Select **+ Create policy** and then select **Next**.

1. Enter your policy scope parameters and select **Next**. :::image type="content" source="media/site-lifecycle-management/4-inactive-site-policy-create-policy-set-scope-filled.png" alt-text="screenshot of site lifecycle management set policy scope." lightbox="media/site-lifecycle-management/4-inactive-site-policy-create-policy-set-scope-filled.png":::

1. Name the policy, add a description (optional), and select a policy mode. Select **Next**.

    :::image type="content" source="media/site-lifecycle-management/5-inactive-site-policy-name-policy.png" alt-text="screenshot of site lifecycle management name policy." lightbox="media/site-lifecycle-management/5-inactive-site-policy-name-policy.png":::

    > **October 2024 Parameters Update** - During this step, you can now:
    >
    > - Choose to send emails to site owners/admins.
    > - Choose enforcement actions if there is no response from site owners or admins after three notifications:
        >     - Mark the inactive site as read-only.
        >     - Mark the inactive site as read-only for a configurable duration (3, 6, 9, or 12 months) followed by archiving using Microsoft 365.
            >
            >     See the [Overview of Microsoft 365 Archive](/microsoft-365/archive/archive-setup) for more details on this storage solution for inactive SharePoint content.

1. Select **Done**. Your policy is now created and can be viewed and managed from the Site lifecycle management dashboard.

## Site owner notifications

Notifications inform SharePoint site owners when a site has been inactive for a specified number of months. To keep the site, the owner should select the **Certify site** button in the notification email. Once certified, site lifecycle management won't check the site's activity for one year.

Site owners receive monthly notifications for three months. After this period, no notifications are sent for the next three months. If the site remains inactive after six months, monthly notifications resume. The policy execution report lists inactive sites as unactioned by the site owner. You can download this report and filter out sites marked as unactioned.

> [!TIP]
> Before creating an inactive site policy, check for any site access restriction policies that could disrupt site attestation by the respective site owner.

## Read-only mode

If the tenant admin configures the policy to take automated enforcement action when there's no response from the notification recipients, additional notifications are sent to inform the site owners or admins.

A notification is sent when the site goes into read-only mode.

:::image type="content" source="media/site-lifecycle-management/9-inactive-site-policy-read-only-mode.png" alt-text="screenshot of site lifecycle management read-only mode notification." lightbox="media/site-lifecycle-management/9-inactive-site-policy-read-only-mode.png":::

Once the site is in read-only mode, the following banner is added to the site:

:::image type="content" source="media/site-lifecycle-management/10-inactive-site-policy-read-only-mode-banner.png" alt-text="screenshot of site lifecycle management read-only mode banner at the top of a SharePoint site." lightbox="media/site-lifecycle-management/10-inactive-site-policy-read-only-mode-banner.png":::

### Remove read-only banner from a site

As a SharePoint administrator, you can remove the read-only mode for a site from the SharePoint admin center.

To remove a site from read-only mode:

1. Expand Sites and select **Inactive sites**.
1. Select the site you want to edit and select **Unlock**. Alternatively, go to the **Active sites** page, select on the site, and then select **Unlock** from the site page panel.

Site owners can't remove a site from read-only mode and must contact you to unarchive the site.

### Unarchive a site

To unarchive a site, follow these steps in SharePoint admin center:

1. Expand sites and select **Archived sites**.
1. Select the site you want to unarchive and select **Unarchive site**.

## Sites managed by multiple inactive site policies

If a site falls under multiple inactive site policies, notification emails aren't repeated. If a notification was sent within the last 30 days from any inactive site policy, the site remains inactive, and no further notifications are sent. The policy execution report shows the site's status as "Notified by another policy."

## Scope of inactive site policies

You can configure parameters for an inactive site policy like inactive time period, template type, site creation source, sensitivity labels, and exclusion of up to 100 sites.

### In-scope site activities

Inactive site policies analyze activity across SharePoint and connected platforms like Teams, Viva Engage (formerly Yammer), and Exchange to detect a site's last activity.

|Platform type | Activities  |
|---------|---------|
|**SharePoint**     |Viewed files, edited files, shared files internally and externally, synced files, viewed pages, visited pages          |
|**Viva Engage (formerly Yammer)**     |Posted messages, read conversations, liked messages         |
|**Teams**     |Posted channel messages in a team across all channels, posted messages in Teams and all channels, replied to messages, mentioned in messages, reacted to messages, sent urgent messages, conducted meetings (recurring, ad hoc, one-time)          |
|**Exchange**     | Received emails in the Exchange mailbox       |

### In-scope site templates

Site lifecycle management reviews the activity of communication sites, classic sites, Teams-connected sites, and group-connected sites with the following site template types:

|Site type|Template type|
|---|---|
|Communication site|SitePagePublishing#0|
|Classic sites|STS#0, STS#1, STS#2, WIKI#0, BLOG#0, SGS#0, SPS#0, SPSNEWS#0, ENTERWIKI#0, COMMUNITY#0, DEV#0, EXPRESS#0, EHS#1, EHS#2|
|Teams-connected site|STS#3 or Group#0|
|Group-connected site|STS#3 or Group#0|

### Out-of-scope sites

The following sites are considered out-of-scope and excluded from site activity detection:

- Ownerless sites
- Number of site owners
- OneDrive sites
- Sites with retention policies applied
- Sites with other compliance policies applied
- Locked sites
- Sites created by system users
- App catalog sites
- Root sites
- Home sites
- Tenant admin sites

## Reporting

Sites with inactivity for six months are listed in the policy execution report. The report is available for download as a .csv file and lets you filter out sites that are considered unactioned by site owners.

:::image type="content" source="media/site-lifecycle-management/8-inactive-site-policy-downloaded-csv-report.png" alt-text="screenshot of inactive site policy downloaded csv report." lightbox="media/site-lifecycle-management/8-inactive-site-policy-downloaded-csv-report.png":::

The following table describes the information included in the policy execution report:

|Column  | Definition  |
|---------|---------|
|**Site name**     |Name of inactive site         |
|**URL**     |URL of inactive site         |
|**Template**     |Template of inactive site         |
|**Sensitivity label**     |Sensitivity label of inactive site       |
|**Site owner emails**     |Email addresses of site owners receiving inactive site activity email notifications           |
|**Last site activity**     |Date of last activity detected by inactive site policy across SharePoint site and connected workloads (Exchange, Viva Engage (formerly Yammer), or Teams)         |
|**Date created**     |Date when the inactive site was created         |
|**Storage used**     |Storage consumed by inactive site    |
|**Action status**     |Status of the site (First/second/third notification sent, Site in read-only mode, Site archived)|
|**Retention policy applied**|Whether a retention policy has been applied to the site or not|
|**Number of Site owners**|Number of site owners for a site|
|**Number of Site admins**|Number of site admins for a site|
|**Total notifications count**|Total number of notifications sent to site owners or admins|
|**Enforced on**|Date on which the enforcement action was taken (date when site was archived or put in read-only mode)|
|**Duration in read-only mode**|Number of months the site has been in the enforced read-only state|

## Related articles

- [Microsoft 365 group expiration policy](/microsoft-365/solutions/microsoft-365-groups-expiration-policy)
- [Restore deleted sites](restore-deleted-site-collection.md)
- [Overview of SharePoint Premium - SharePoint Advanced Management](advanced-management.md)
- [Overview of Microsoft 365 Archive](/microsoft-365/archive/archive-setup)
