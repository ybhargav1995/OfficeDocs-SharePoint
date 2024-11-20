---
ms.date: 11/20/2024
title: "Microsoft SharePoint Premium - SharePoint Advanced Management frequently asked questions"
ms.reviewer: daminasy
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
- ContentEnagagementFY24
search.appverid:
- MET150
recommendations: false
description: "Learn about Microsoft SharePoint Premium - SharePoint Advanced Management through this FAQ."
---

# SharePoint Advanced Management frequently asked questions

Here's a list of frequently asked questions regarding [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md):

## My site owners did their site access review and reduced the number of Anyone and other links. Why does my report still show the same number of shared links as before?

Site access review is linked to the Data access governance report from which it's generated. If you want to see the effects of the latest status of site owner actions, run the Data access governance permission report again.

## I made sure to install the latest SharePoint Online Management Shell, but the SharePoint Advanced Management commands I want aren’t present! How do I get the latest commands?

You have more than one SharePoint Online Management Shell module installed on the machine you're using to run the commands. Admins would need to run the following to clean up all the modules, and then update to the latest.  

Uninstall-Module Microsoft.Online.SharePoint.PowerShell -Force -AllVersions  

Then, uninstall the SharePoint Online Management Shell via the Control Panel and reinstall the [latest version](<https://www.microsoft.com/download/details.aspx?id=35588>).

## Do I need to manually assign SharePoint Advanced Management licenses to users?

No.

## Which specific reports in Data access governance require SharePoint Advanced Management?

1. Permissions report: This report lists sites where the count of users that can access is greater than a specified number. It helps identify sites with potentially excessive access.
2. Site access review for Permissions Report: This allows tenant admins to initiate a site access review for any site within the permissions report via PowerShell. The site owner can then view the details in the site UI and take necessary actions.
3. Site access review for 'Sharing links' report: Data access governance provides a sharing links report for tenant admins, listing sites with the highest volume of sharing links generated in the last 28 days. Tenant admins can ask the corresponding site owner to review these links and take necessary actions.
4. Autorun Data access governance reports: You can schedule Data access governance reports to run automatically every 28 days and receive notifications when the autorun completes.
5. Content shared with 'Everyone except external users' (EEEU) report: This report identifies sites, files, and folders shared with the EEEU domain group in the last 28 days.

Reports that don't require SharePoint Advanced Management are:

- Basic Permissions Reports: These reports provide a snapshot of the current state of permissions without the advanced features like site access reviews or automated scheduling.
- Activity Reports: These reports offer insights into activities within the past 28 days, helping to manage and review access to content that might be at risk of being overshared.  

## What is the difference between SharePoint Premium and SharePoint Advanced Management?

SharePoint Premium is an advanced content management platform that builds on the familiar SharePoint experience. It brings AI, automation, and added security to content experiences, processing, and governance. It's designed to enhance content management and experiences in Microsoft 365 as an expansion and rebranding of Microsoft Syntex.

SharePoint Advanced Management, on the other hand, focuses on security and content governance. It includes features like manually applying sensitivity labels and policies, as well as automatically applying sensitivity labels and dynamic policies with Microsoft 365 E5. SharePoint Advanced Management is available as an add-on license and is administered by SharePoint administrators in the SharePoint admin center.

## Do organizations really require the entire company to be licensed to take advantage of specific features or can a subset of licenses be purchased and targeted to only users impacted by SharePoint Advanced Management solutions?

To use SharePoint Advanced Management, organizations must have a license for each user in the organization who will be using or benefiting from the features.

However, not all features require the entire company to be licensed. Here are some key points:

- Restrict SharePoint site access: If this feature is applied to a site, all members and site owners of that site need to be licensed.

- Restrict OneDrive content access: If this feature is applied, all users in the tenant need to be licensed, specifically E3/E5 users.

- Data Access Governance reports for SharePoint Sites: If only the reports are used, only the admins need a license. However, if you trigger the Site access review policy, all site owners need to be licensed.

- Conditional access policy for SharePoint and OneDrive sites: If this is applied to a site, all members and owners of that site need to be licensed.

- Advanced sites content lifecycle management: Admins and site owners need to be licensed.

- Block download policy: If applied to a site, the members and owners of that site need a license. If you enable the block download policy for Teams Recordings and Transcripts at the tenant level, all users in the tenant need to be licensed, specifically E3/E5 users.

- Review recent changes: Only admins need to be licensed.

## If I get the SharePoint Advanced Management trial can I run Data access governance reports for my entire organization or does that go beyond licensing requirements?

Yes, you can run Data Access Governance reports for your entire organization with a SharePoint Advanced Management trial license. However, there are some important considerations to keep in mind:

- Licensing requirements: While you can generate Data access governance reports during the trial period, all users who benefit from the features must be licensed once the trial ends. This means that if you decide to continue using SharePoint Advanced Management features after the trial, you'll need to purchase licenses for all relevant users.

- Report generation: During the trial, you can generate Data access governance reports to discover sites with potentially overshared or sensitive content. These reports help you assess and apply appropriate security and compliance policies.

- Post-trial access: Any reports or data generated during the trial will remain available to you after the trial ends. However, the features stop working, and no new data are generated if SharePoint Advanced Management isn't purchased.

## Are there any impacts to SharePoint Advanced Management in a multi-geo environment?

SharePoint Advanced Management in a multi-geo environment has several considerations to keep in mind:

- Data residency: Multi-Geo capabilities in SharePoint and OneDrive allow organizations to control where their data is stored at rest, meeting data residency requirements. Each user, Group mailbox, and SharePoint site have a Preferred Data Location (PDL) which denotes the geo location where related data is to be stored.

- Site and group creation: When a user creates a SharePoint group-connected site in a multi-geo environment, their PDL is used to determine the geo location where the site and its associated Group mailbox are created. If the user's PDL value hasn't been set or is set to a geo location that hasn't been configured as a satellite location, the site and mailbox are created in the central location.

- Administrative options: Managing the multi-geo environment is available through the SharePoint admin center. Some actions, such as moving a SharePoint site or a OneDrive site, require Microsoft PowerShell.

- User experience: Users get a seamless experience when using Microsoft 365 services, including Office applications, OneDrive, and Search. SharePoint Hub sites enhance the discovery and engagement with content for employees, while creating a complete and consistent representation of projects, departments, or regions. In a Multi-Geo environment, sites from satellite locations can easily be associated with a hub site regardless of the hub site's geography location.

## Can I initiate a Site access review manually on a site without running a Data access governance report?

Initiating a Site access review manually on a site without running a Data Access Governance report isn't supported. The Site access review feature is designed to work with Data access governance reports to identify overshared sites and delegate the review process to site owner. This ensures that the review is context-specific and addresses the concerns identified in the Data access governance reports.

## How many Site access reviews can I start at once?

In SharePoint Advanced Management, you can initiate Site Access Reviews for up to 100 sites at once.  

## What defines a site owner in a Site access review in a non-group connected site?

In a Site access review for a nongroup connected site, a site owner is defined as the user who has full control of that particular SharePoint Online site. This means that the site owner is responsible for creating and managing lists, libraries, and pages within the site, as well as managing user access and permissions. Site owners are best positioned to review and address oversharing issues for their own sites, as they have the necessary permissions and understanding of the site's content and sharing settings.

## If there are many site owners, which site owners are picked for a Site access review?

When there are multiple site owners for a SharePoint site, the Site access review process sends review requests to all site owners. This ensures that all individuals with full control over the site are involved in the review process and can address any oversharing issues identified in the Data access governance reports.

## What SharePoint objects with granted permissions are reviewed for Site access reviews?

In SharePoint Advanced Management, Site access reviews focus on reviewing permissions for various SharePoint objects to ensure that access is appropriately managed. The objects reviewed include:

- Sites: The overall site permissions are reviewed to ensure that only authorized users have access.

- Lists and libraries: Permissions for lists and libraries within the site are reviewed to ensure that sensitive information isn't overshared.

- Folders and documents: Permissions for specific folders and documents are reviewed to ensure that access is restricted to authorized users only.

These reviews help identify and address any oversharing issues, ensuring that sensitive information is protected and access is appropriately managed.

## What is the difference between Inactive sites policy and M365 Group Expiration policies in Microsoft Entra?

The Inactive sites policy and Microsoft 365 Group Expiration policies in Microsoft Entra serve different purposes and have distinct functionalities:

- Inactive sites policy: This policy is designed to manage SharePoint sites that are no longer in use. It helps administrators identify and take action on sites that have been inactive for a specified period. Actions can include notifying site owners, archiving the site, or deleting it. This policy ensures that unused sites don't clutter the environment and helps maintain an organized and efficient SharePoint infrastructure.

- Microsoft 365 Group Expiration Policy: This policy focuses on the lifecycle management of Microsoft 365 groups. It automatically renews groups based on user activity, such as sending an email to the group, uploading a document to SharePoint, or visiting a Teams channel. If a group is inactive for a specified period, the group owners are notified to renew the group. If the group isn't renewed, it's deleted but can be restored within 30 days. This policy helps manage the proliferation of unused groups and ensures that only active groups remain in the environment.

## What if I have Inactive sites policies and Microsoft 365 Group Expiration policies running at the same time?

When both policies are active, they operate independently but can complement each other in managing site and group lifecycles. Here are some key points:

Notification management: If a site falls under multiple inactive site policies, notification emails aren't repeated. If a notification was sent within the last 30 days from any inactive site policy, the site remains inactive, and no further notifications are sent. The policy execution report shows the site's status as "Notified by another policy."

Policy execution: The Inactive Sites Policy helps manage SharePoint sites that are no longer in use by notifying site owners and taking actions such as archiving or deleting the site. The Microsoft 365 Group Expiration Policy, on the other hand, focuses on the lifecycle management of Microsoft 365 groups, automatically renewing or deleting groups based on user activity.

Effect on associated services: When a Microsoft 365 group expires, almost all of its associated services (such as the mailbox, Planner, SharePoint site, and Teams) are also deleted. This means that if a group expires, the associated SharePoint site will also be impacted.

## Related topics

[Microsoft SharePoint Premium - SharePoint Advanced Management overview](advanced-management.md)
