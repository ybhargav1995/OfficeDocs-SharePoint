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

Agents in SharePoint, powered by AI, help employees quickly find information and insights on SharePoint sites, pages, and document libraries. Agents in SharePoint access your organization's data the same way [Copilot in other Microsoft 365 apps](/sharepoint/sharepoint-copilot-best-practices#copilot-and-sharepoint) does, responding to users based on their access permissions to the data. As a SharePoint admin, you can manage employees' access to an agent in multiple ways by managing:
-	Who can access the agents
-	What information the user can access through the agent
-	Whether agents are available in a specific SharePoint site 

## Manage who can access the agents

Currently, users with a [Microsoft 365 Copilot license](/copilot/microsoft-365/microsoft-365-copilot-licensing) can use the agents. You can use the [Microsoft 365 Copilot setup guide](https://admin.microsoft.com/Adminportal/Home?Q=learndocs#/modernonboarding/microsoft365copilotsetupguide) in the Microsoft 365 admin center to assign the required licenses to users. For more information, see [Assign licenses to users in the Microsoft 365 admin center](/microsoft-365/admin/manage/assign-licenses-to-users) and [Microsoft 365 Copilot requirements](/copilot/microsoft-365/microsoft-365-copilot-requirements).

> [!NOTE]
> From December 1, 2024, to June 30, 2025, enterprise tenants with 50 or more Microsoft 365 Copilot licenses will receive 10,000 free Agents in SharePoint queries for unlicensed users every month as a trial. SharePoint administrators or above can [check the trial promotion status](/powershell/module/sharepoint-online/get-spocopilotpromooptinstatus) and [set trial promotion](/powershell/module/sharepoint-online/set-spocopilotpromooptinstatus) using PowerShell cmdlets. Please see terms of trial usage [here](/legal/microsoft-365/in-app-trials-terms-of-service). 

## Manage what information a user can access through the agents

### With built-in SharePoint features

Agents in SharePoint use SharePoint sites, pages and document libraries as knowledge sources to respond to the user. You can control a user’s access to the information when they use an agent by controlling their access to the site. SharePoint provides many tools to control access to a site:

- Make a site private to ensure only the people who have explicit permission to access the site.
- If the site is associated with a Microsoft 365 group and the site is private, control group membership to control who can visit the site.
- If the site isn’t associated with a group and is private, use site permissions to control access.
- Use access governance policies available in the SharePoint admin center and PowerShell to control access based on other criteria.

Learn more about using SharePoint built-in features to control access [here](/sharepoint/sharepoint-copilot-best-practices#step-2---prevent-oversharing-and-control-access-with-sharepoint-and-onedrive).

## With SharePoint advanced management

Currently, to restrict access to a site by Microsoft 365 Copilot, the SharePoint Admin can set up a [restricted access control policy](/sharepoint/restricted-access-control). As a result, all access to the site is restricted to only the group of users specified in the policy. Accordingly, the content from this site is visible in Microsoft 365 Copilot only for this restricted group of users. You can restrict access to individual sites or OneDrive.
Learn more about additional features to prevent oversharing, control access, and enhance your content governance with SharePoint advanced management [here](/sharepoint/get-ready-copilot-sharepoint-advanced-management).

## Turn off agents in SharePoint with restricted content discovery

You as a SharePoint Admin can turn off all agent-related features on individual sites with the [restricted content discovery](/sharepoint/restricted-access-control). Once a site is flagged with restricted content discovery, users can't see the Copilot icon on the upper right of the site. Therefore, they don’t have access to use the ready-made agent, create new agents, or add content from that site to any other agents. The restricted content discovery policy leaves site access unchanged but prevents the site's content from being surfaced in Microsoft 365 Copilot or organization-wide Search for all users.  

