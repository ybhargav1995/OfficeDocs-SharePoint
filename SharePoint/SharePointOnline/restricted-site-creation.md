---
ms.date: 11/20/2024
title: "Restrict SharePoint site creation (preview)"
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
description: "Learn how to restrict users from creation SharePoint sites using Restricted site creation."
---

# Restrict SharePoint site creation (preview)

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

The Restricted site creation feature lets IT administrators use SharePoint Online PowerShell to designate which Microsoft Entra groups in their tenant can create SharePoint sites.

Users who aren't in the group aren't able to create a SharePoint site. Restricted site creation policy only controls the provisioning capability and not the site access permissions.

> [!NOTE]
> The sites in scope for preview are SharePoint team sites (group-connected and classic), communication sites, OneDrive, and All sites.

## Prerequisites

- Confirm you have the latest version of [Microsoft SharePoint Online PowerShell](https://www.microsoft.com/download/details.aspx?id=35588) installed.
- The Restricted site creation feature requires a [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md) subscription.

## Current limitations

- Only Microsoft Entra security groups (mail enabled or non-mail-enabled) are supported at this time.
- You can configure up to 10 groups per site type.

## Template exceptions

Choosing the All Sites option includes all sites except for any template listed in the following table. This capability supersedes all others.

|Type|Template name|Template ID|Reason|
|---|---|---|---|
|OneDrive|SPSPERS|21|OneDrive experience is separate|
|RaaS|CSPCONTAINER|70|RaaS experience is managed separately|
|Redirect site|REDIRECTSITE|301|Critical SharePoint functionality|
|My Site Host|MYSITEHOST|54|Core site|
|Tenant Admin|TENANTADMIN|16|Core site|

## Restricted site creation PowerShell commands

See the following table to learn more about the commands used to manage Restricted site creation for SiteTypes such as All, team, communication, and OneDrive:

|Action|PowerShell command|Example|
|---|---|---|
|Enable site access restriction|`Set-SPORestrictedSiteCreation –Enabled $true`||
|Add/reconfigure security group|`Set-SPORestrictedSiteCreation -SiteType <Enum> -RestrictedSiteCreationGroups <comma separated group GUIDS> -Allow`<br><br>`Set-SPORestrictedSiteCreation -SiteType <Enum> -RestrictedSiteCreationGroups <comma separated group GUIDS> -Deny`|`Set-SPORestrictedSiteCreation –Enabled:$true –Mode Allow`<br><br>`Set-SPORestrictedSiteCreation –SiteType "Team" -RestrictedSiteCreationGroups "78159241-04a9-41d2-8dd4-ac568e9766a3,1f95829b-e1c8-4406-b2be-508c36f4bca5"`<br><br>`Set-SPORestrictedSiteCreation –SiteType "All" -RestrictedSiteCreationGroups "281e395b-7316-4cb2-b5bb-8881426ee411"`<br><br>`Set-SPORestrictedSiteCreation –SiteType "Communication" -RestrictedSiteCreationGroups`|
|View security group|`Get-SPORestrictedSiteCreation -SiteType <Enum>`|`Get-SPORestrictedSiteCreation –SiteType All`|
|Disable site access restriction|`Set-SPORestrictedSiteCreation -Enabled:$false`||

## Manage Restricted site creation

The following processes let you enable Restricted site creation for the tenant and the two methods of managing the feature:

### Enable Restricted site creation for your tenant

To enable site creation restriction, run the following command in SharePoint Online PowerShell:

```powershell
Set-SPORestrictedSiteCreation -RestrictedSiteCreation $true
```

> [!IMPORTANT]
> Once you enable the Restricted site creation feature, consider if you want to deny certain groups from creating sites, or if you prefer to allow certain groups the ability to create sites.
>
>Choosing your strategy is important because swapping between the two modes will remove the existing Restricted site creation configuration.

### Restrict Microsoft Entra groups from creating sites

You can specify up to 10 Microsoft Entra groups to be restricted from creating sites. To exclude a group from site provisioning capabilities, run the following command:

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
> Acceptable enumerations or enums for this command are: All Sites, Team sites (group-connected and classic), Communication sites.

### Allow Microsoft Entra groups to create sites

To specify up to 10 Microsoft Entra groups to be allowed to create sites, run the following command:

```powershell
Set-SPORestrictedSiteCreation -SiteType <Enum> -SetRestrictedSiteCreationGroups <comma separated group GUIDS> -Allow  
```

> [!NOTE]
> Changing from deny to allow mode will prompt the message: “Are you sure you want to switch from Deny to Allow? Switching will remove all current configuration of restrictions.”

### Manage Microsoft Entra groups in existing Restricted site creation configurations

If you enabled Restricted site creation and need to edit or remove a Microsoft Entra group, you must use the **-Deny** command to replace the existing configuration. The **-Deny** command replaces the existing configuration and you're able to specify a new group configure.

```powershell
Set-SPORestrictedSiteCreation -SiteType <Enum> -SetRestrictedSiteCreationGroups <comma separated group GUIDS> -Deny
```

## Related topics

[Microsoft SharePoint Premium – SharePoint Advanced Management overview](advanced-management.md)
