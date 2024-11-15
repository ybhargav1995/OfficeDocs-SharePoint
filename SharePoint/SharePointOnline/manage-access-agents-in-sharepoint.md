---
ms.date: 11/14/2024
title: Manage access to agents in SharePoint
ms.reviewer: 
ms.author: ruihu
author: maggierui
manager: jtremper
recommendations: true
audience: Admin
f1.keywords:
- NOCSH
ms.topic: how-to
ms.service: sharepoint-online
ms.collection: 
- M365-collaboration
- m365copilot
- magic-ai-copilot
- Tier2

ms.localizationpriority: medium
search.appverid:
- MET150
description: "Learn how to manage access to agents in SharePoint with built-in SharePoint premission models, SharePoint advanced management features such as restricted access control, and restricted content discovery."
---
# Manage access to agents in SharePoint

## Control access with built-in SharePoint features

SharePoint provides many tools to control access to a site:
- Make a site private to ensure only the people who have explicit permission to access the site.
- If the site is associated with a Microsoft 365 group and the site is private, control group membership to control who can visit the site.
- If the site isn’t associated with a group and is private, use site permissions to control access.
- Use access governance policies available in the SharePoint admin center and PowerShell to control access based on other criteria.

Learn more about using SharePoint built-in features to control access [here](/sharepoint/sharepoint-copilot-best-practices#step-2---prevent-oversharing-and-control-access-with-sharepoint-and-onedrive).

## Control access with SharePoint advanced management

Currently, to restrict access to a site by Microsoft 365 Copilot, the SharePoint Admin can set up a [restricted access control policy](/sharepoint/restricted-access-control). As a result, all access to the site is restricted to only the group of users specified in the policy. Accordingly, the content from this site is visible in Microsoft 365 Copilot only for this restricted group of users. You can restrict access to individual sites or OneDrive.
Learn more about additional features to prevent oversharing, control access, and enhance your content governance with SharePoint advanced management [here](/sharepoint/get-ready-copilot-sharepoint-advanced-management).

## Turn off agents in SharePoint with restricted content discovery

You as a SharePoint Admin can turn off all agent-related features on individual sites with the [restricted content discovery](/sharepoint/restricted-access-control). Once a site is flagged with restricted content discovery, users can't see the Copilot icon on the upper right of the site. Therefore, they don’t have access to use the ready-made agent, create new agents, or add content from that site to any other agents. The restricted content discovery policy leaves site access unchanged but prevents the site's content from being surfaced in Microsoft 365 Copilot or organization-wide Search for all users.  
