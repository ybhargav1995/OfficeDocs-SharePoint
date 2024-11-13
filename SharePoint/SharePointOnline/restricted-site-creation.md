---
ms.date: 11/20/2024
title: "Restrict SharePoint site creation"
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
description: "Learn how to restrict users from creation SharePoint sites using restricted site creation."
---

# Restrict SharePoint site creation

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

The restricted site creation feature lets IT administrators use [SharePoint Online PowerShell](/powershell/sharepoint/sharepoint-online/introduction-sharepoint-online-management-shell#getting-started-with-sharepoint-online-powershell) to designate which Microsoft Entra security groups in their tenant can create SharePoint sites.

You can choose between two ways to manage site creation within your tenant: deny mode (the specified groups are unable to create sites) and allow mode (only the specified groups are allowed to create sites). Once enabled for your tenant, restricted site creation is set to deny mode by default.

Restricted site creation policies only control site provisioning capabilities and not site access permissions.

> [!NOTE]
> The sites in scope for this feature are SharePoint team sites (group-connected and classic), communication sites, OneDrive, and all sites.

## Prerequisites

- Confirm you have the latest version of [Microsoft SharePoint Online PowerShell](https://www.microsoft.com/download/details.aspx?id=35588) installed.
- The restricted site creation feature requires a [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md) subscription.

## Current limitations

- Only Microsoft Entra security groups (mail-enabled or non-mail-enabled) are supported at this time.
- You can configure up to 10 security groups per site type.

## Restricted site creation PowerShell commands

See the following table to learn more about the commands used to manage restricted site creation for SiteTypes: all sites, SharePoint team sites (group-connected and classic), communication, and OneDrive: See [Create a site](/sharepoint/create-site-collection) to learn more about different types of SharePoint sites.

|Action|PowerShell command|Example|
|---|---|---|
|Enable site access restriction|`Set-SPORestrictedSiteCreation –Enabled $true`||
|Add/reconfigure security group|`Set-SPORestrictedSiteCreation -SiteType <Enum> -RestrictedSiteCreationGroups <comma separated group GUIDS> -Allow`<br><br>`Set-SPORestrictedSiteCreation -SiteType <Enum> -RestrictedSiteCreationGroups <comma separated group GUIDS> -Deny`|`Set-SPORestrictedSiteCreation –Enabled:$true –Mode Allow`<br><br>`Set-SPORestrictedSiteCreation –SiteType "Team" -RestrictedSiteCreationGroups "78159241-04a9-41d2-8dd4-ac568e9766a3,1f95829b-e1c8-4406-b2be-508c36f4bca5"`<br><br>`Set-SPORestrictedSiteCreation –SiteType "All" -RestrictedSiteCreationGroups "281e395b-7316-4cb2-b5bb-8881426ee411"`<br><br>`Set-SPORestrictedSiteCreation –SiteType "Communication" -RestrictedSiteCreationGroups`|
|View security group|`Get-SPORestrictedSiteCreation -SiteType <Enum>`|`Get-SPORestrictedSiteCreation –SiteType All`|
|Disable site access restriction|`Set-SPORestrictedSiteCreation -Enabled:$false`||

## Manage restricted site creation

The following processes let you enable restricted site creation for the tenant and the two methods of managing the feature:

### Enable restricted site creation for your tenant

To enable site creation restriction, run the following command in SharePoint Online Management Shell:

```powershell
Set-SPORestrictedSiteCreation -RestrictedSiteCreation $true
```

> [!IMPORTANT]
> Once you enable the restricted site creation feature, consider if you want to deny certain groups from creating sites, or if you prefer to allow certain groups the ability to create sites.
>
>Choosing your strategy is important because swapping between the two modes will remove the existing restricted site creation configuration.

The restricted site creation feature only supports either all deny, or all allow configurations.

### Restrict Microsoft Entra security groups from creating sites

You can specify up to 10 Microsoft Entra security groups to be restricted from creating sites. To exclude a security group from site provisioning capabilities, run the following command:

```PowerShell
Set-SPORestrictedSiteCreation -SiteType <Enum> -SetRestrictedSiteCreationGroups <comma separated group GUIDS>  -Deny
```

Once site creation restriction is enabled, users can receive the following messages depending on the type of restricted site:

Communication site creation error message:
:::image type="content" source="media/restricted-site-creation/1-restricted-site-creation-sharepoint.png" alt-text="screenshot of failed communication site creation." lightbox="media/restricted-site-creation/1-restricted-site-creation-sharepoint.png":::

OneDrive creation error message:
:::image type="content" source="media/restricted-site-creation/2-restricted-site-creation-onedrive.png" alt-text="screenshot of failed OneDrive site creation." lightbox="media/restricted-site-creation/2-restricted-site-creation-onedrive.png":::

Teams site creation error message if created from the admin UI:
:::image type="content" source="media/restricted-site-creation/3-restricted-site-creation-onedrive-created-admin-ui.png" alt-text="screenshot of failed OneDrive site creation if created from admin UI." lightbox="media/restricted-site-creation/3-restricted-site-creation-onedrive-created-admin-ui.png":::

> [!NOTE]
> Acceptable enumerations or enums for this command are: all sites, team sites (group-connected and classic), communication sites.

### Allow Microsoft Entra security groups to create sites

To specify up to 10 Microsoft Entra security groups to be allowed to create sites, run the following command:

```powershell
Set-SPORestrictedSiteCreation -SiteType <Enum> -SetRestrictedSiteCreationGroups <comma separated group GUIDS> -Allow  
```

> [!NOTE]
> Changing from deny to allow mode will prompt the message: “Are you sure you want to switch from Deny to Allow? Switching will remove all current configuration of restrictions.”

### Manage Microsoft Entra security groups in existing restricted site creation configurations

If you enabled restricted site creation and need to edit or remove a Microsoft Entra security group, you must use the **-Deny** command to replace the existing configuration. The **-Deny** command replaces the existing configuration and you're able to specify a new group configure.

```powershell
Set-SPORestrictedSiteCreation -SiteType <Enum> -SetRestrictedSiteCreationGroups <comma separated group GUIDS> -Deny
```

## Related topics

[Microsoft SharePoint Premium – SharePoint Advanced Management overview](advanced-management.md)
