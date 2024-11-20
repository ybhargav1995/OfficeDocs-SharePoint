---
ms.date: 11/19/2024
title: "Restrict OneDrive and SharePoint site creation"
ms.reviewer: vgaddam
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
description: "Learn how to restrict users from creating OneDrive and SharePoint sites using restricted site creation."
---

# Restrict OneDrive and SharePoint site creation

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

The restricted site creation feature lets IT administrators use [SharePoint Online Management Shell](/powershell/sharepoint/sharepoint-online/introduction-sharepoint-online-management-shell#getting-started-with-sharepoint-online-powershell) to designate which Microsoft Entra security groups in their tenant can create OneDrive and SharePoint sites.

You can choose between two ways to manage site creation within your tenant: deny mode (the specified groups are unable to create sites) and allow mode (only the specified groups are allowed to create sites). Once you enable this feature for your tenant, restricted site creation is set to deny mode by default.

Restricted site creation policies only control site provisioning capabilities and not site access permissions.

## Prerequisites

- The latest version of [Microsoft SharePoint Online Management Shell](https://www.microsoft.com/download/details.aspx?id=35588) must be installed.
- The restricted site creation feature requires a [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md) subscription.

## Site types

Each restricted site creation policy includes a *site type* specifying the types of sites users in the specified groups are either allowed or denied from creating.

|Site type|Applies to|
|---|---|
|All|OneDrive and all SharePoint sites|
|SharePoint|All SharePoint sites (but not OneDrive)|
|OneDrive|Only OneDrive|
|Team|Only SharePoint team sites (group-connected and classic)|
|Communication|Only SharePoint communication sites|

Up to 10 Microsoft Entra security groups can be specified for each site type.

When restricted site creation is in allow mode, a user is only allowed to create a site if they are in a group configured with a site type which applies to the site they're attempting to create. For example, a user can create a OneDrive if they are in a security group configured with the All or OneDrive site types.

When restricted site creation is in deny mode, a user is blocked from creating a site if they are in any group configured with any site type which applies to the site they're attempting to create. For example, a user is blocked from creating a SharePoint communication site if they are in any group configured with the All, SharePoint, or Communication site types.

> [!NOTE]
> The restricted site creation mode is shared across all site type policies. It is not possible to use deny mode for one site type and allow mode for a different site type.

## Current limitations

- Only Microsoft Entra security groups (mail-enabled or non-mail-enabled) are supported at this time.
- You can configure up to 10 security groups per site type.
- This feature is currently unavailable for government cloud environments such as GCCH/GCC-Moderate/DoD/Gallatin.

## Manage restricted site creation

The `Set-SPORestrictedSiteCreation` and `Get-SPORestrictedSiteCreation` cmdlets in the SharePoint Online Management Shell allow the admin to configure and view the restricted site creation feature and policies for the tenant.

> [!IMPORTANT]
> You must use version 16.0.25513 (published November 2024) or later of the SharePoint Online Management Shell for these commands to function properly. Earlier versions do not have the current list of site types and will not operate correctly.

### Enable restricted site creation for your tenant

To enable restricted site creation, run the following command in the SharePoint Online Management Shell:

```powershell
Set-SPORestrictedSiteCreation –Enabled $true
```

Restricted site creation starts in deny mode without any policies, and doesn't affect any users by default.

### Set Allow or Deny mode

Once you enable the restricted site creation feature, consider whether you want to deny certain groups from creating sites or allow certain groups the ability to create sites.

For example, the following command sets restricted site creation to deny mode:

```powershell
Set-SPORestrictedSiteCreation –Mode Deny
```

> [!IMPORTANT]
> Swapping between the two modes will remove all existing site type configurations. The restricted site creation feature only supports either all deny or all allow configurations.

### Configure policies for site types

You can specify a comma separated list of up to 10 Microsoft Entra security groups for each site type. For example, if restricted site creation is in deny mode, the following command creates a policy blocking users in either of the following two groups from creating any SharePoint site.

```powershell
Set-SPORestrictedSiteCreation -SiteType SharePoint -RestrictedSiteCreationGroups "00aa00aa-bb11-cc22-dd33-44ee44ee44ee,11bb11bb-cc22-dd33-ee44-55ff55ff55ff"
```

> [!NOTE]
> Microsoft Entra security groups must be specified with the Object Id shown in the [Microsoft Entra admin center](/entra/fundamentals/how-to-manage-groups).

To clear the configuration for site type, specify **""** for the RestrictedSiteCreationGroups:

```powershell
Set-SPORestrictedSiteCreation -SiteType All -RestrictedSiteCreationGroups ""
```

### View configuration

Use the following command to view the existing restricted site creation configurations:

```powershell
Get-SPORestrictedSiteCreation
```

## User restriction

When a user is blocked from creating a site by a restricted site creation policy, they receive a message depending on the type of site they're creating and how they're creating it. See the following examples for reference:

When a user creates a communication site from the web, they see the error message "Due to organizational policies, you can't create this type of site."

:::image type="content" source="media/restricted-site-creation/1-restricted-site-creation-sharepoint.png" alt-text="screenshot of failed communication site creation." lightbox="media/restricted-site-creation/1-restricted-site-creation-sharepoint.png":::

When first signing in to their OneDrive from the web, the user sees the error message "You can't make a OneDrive. If you need one, contact your administrator or help desk."

:::image type="content" source="media/restricted-site-creation/2-restricted-site-creation-onedrive.png" alt-text="screenshot of failed OneDrive site creation." lightbox="media/restricted-site-creation/2-restricted-site-creation-onedrive.png":::

When a user creates a team site from the web, the user sees the message "We're still setting up the site for this group," but the site isn't created.

:::image type="content" source="media/restricted-site-creation/3-restricted-site-creation-onedrive-created-admin-ui.png" alt-text="screenshot of failed OneDrive site creation if created from admin UI." lightbox="media/restricted-site-creation/3-restricted-site-creation-onedrive-created-admin-ui.png":::

When creating sites through the SharePoint Online Management Shell, the cmdlet fails with the exception "Due to organizational policies, you can't create this type of site."

:::image type="content" source="media/restricted-site-creation/4-restricted-site-creation-spac-error.png" alt-text="screenshot of failed OneDrive site creation if created from SharePoint admin center." lightbox="media/restricted-site-creation/4-restricted-site-creation-spac-error.png":::

## Related topics

[Microsoft SharePoint Premium – SharePoint Advanced Management overview](advanced-management.md)
