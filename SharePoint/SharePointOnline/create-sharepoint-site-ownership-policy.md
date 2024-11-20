---
ms.date: 10/28/2024
title: Create SharePoint site ownership policy
ms.reviewer: anupam.francis
ms.author: mactra
author: MachelleTranMSFT
manager: jtremper
audience: Admin
f1.keywords:
- NOCSH
ms.topic: how-to
ms.service: one-drive
ms.localizationpriority: medium
ms.collection: 
- M365-collaboration
- M365-sam
ms.custom:
search.appverid:
ms.assetid: 0ecb2cf5-8882-42b3-a6e9-be6bda30899c
description: Learn how to create a SharePoint site ownership policy to manage site lifecycle.
---

# Create SharePoint site ownership policy

The site lifecycle management feature from Microsoft SharePoint Premium - SharePoint Advanced Management lets you improve site governance by having automated policies configured in the SharePoint admin center.

Site ownership policies are a part of site lifecycle management and help effectively manage ownership of SharePoint sites in your organization. Ensuring that each site has owners that are responsible and accountable for its content, access, and other aspects of collaboration is important to keep your organization secure and compliant. With scale, it becomes hard for SharePoint admins and others to keep track of site ownership and take the necessary steps to identify cases where new owners need to be identified or take the required action.

Site ownership policies help solve this problem by allowing you to configure your organization's ownership policies and run every month to identify sites that don't comply with them. They also notify relevant users in line with the behavior you configure to facilitate addition of new owners with minimal admin overhead.  

## Requirements

To access and use this feature, your organization must have [Microsoft SharePoint Premium – SharePoint Advanced Management](/sharepoint/advanced-management).

## Scope of site ownership policies

You can create different policies with different scopes based on your organization's requirements.

You can choose the sites to be scoped under the policy based on site templates, creation sources, sensitivity labels and include sites under retention policies and retention holds. If you wish to exclude specific sites, you can add the site URLs of up to 100 sites in the Exclude sites section while configuring the policy.

> [!NOTE]
>
> - OneDrive sites, sites created by system users, app catalog sites, root sites, home sites, tenant admin sites are excluded from site ownership policies.
>
> - Sites marked as read-only by site ownership policies will be detected and added to the report if they are not compliant as per policy configurations. All other sites locked with no access or read-only access are excluded from site ownership policies.  

## Ownership criteria

Different organizations have different needs. Site ownership policies allow you to customize how ownership is determined by allowing you to:

- Choose who is considered responsible for managing a site in your organization - site owners or site admins or both.  

- Define the minimum number of owners or admins a site should have, currently up to 2.

The policy identifies all sites that aren't compliant with the configured ownership criteria and generate the report. If your policy is active, email notifications would then be sent for identified sites.  

We recommend choosing 2 as the minimum owner count so that sites with a single owner are identified and another owner is added immediately. Having more than one site owner can help to reduce the risk of sites becoming ownerless.

## Create a site ownership policy

To create a site ownership policy, go to the SharePoint admin center.

1. Expand **Policies** and select **Site lifecycle management**.

    :::image type="content" source="media/site-ownership-policy/1-create-site-ownership-policy.png" alt-text="Screenshot of ownership policy being created in SharePoint admin center dashboard." lightbox="media/site-ownership-policy/1-create-site-ownership-policy.png":::

2. Select **+ Create policy** and select **Next**.

    :::image type="content" source="media/site-ownership-policy/2-create-site-ownership-policy.png" alt-text="Screenshot of ownership policy created in SharePoint admin center dashboard." lightbox="media/site-ownership-policy/2-create-site-ownership-policy.png":::

3. Enter your policy scope parameters that determine which sites the policy would act on and select **Next**.

    :::image type="content" source="media/site-ownership-policy/3-create-site-ownership-policy.png" alt-text="Screenshot of site ownership policy with set policy scope in SharePoint admin center dashboard." lightbox="media/site-ownership-policy/3-create-site-ownership-policy.png":::

4. Define the ownership criteria, who should be notified if a site doesn't meet these criteria and what action to take if the site fails to meet these criteria for three months. Select **Next**.

    :::image type="content" source="media/site-ownership-policy/4-create-site-ownership-policy.png" alt-text="Screenshot of ownership policy configuration page in SharePoint admin center dashboard." lightbox="media/site-ownership-policy/4-create-site-ownership-policy.png":::

5. Name your policy, add a description (optional) and select a policy mode. Select **Finish**.

    :::image type="content" source="media/site-ownership-policy/5-create-site-ownership-policy.png" alt-text="Screenshot of ownership policy with notifications options selected." lightbox="media/site-ownership-policy/5-create-site-ownership-policy.png":::

6. Select **Done**. Your policy is now created and can be viewed and managed by selecting Site ownership policies in the Site lifecycle management dashboard.

## Reporting

After each run of the configured policy, you can view a report about the sites it identifies.  

In the **Site ownership policies** page, select the desired policy from the list.

The report outlines the number of sites identified as not meeting the ownership criteria, along with the number of sites that didn't have anyone to notify.

:::image type="content" source="media/site-ownership-policy/6-create-site-ownership-policy-reporting.png" alt-text="Screenshot of ownership policy report." lightbox="media/site-ownership-policy/6-create-site-ownership-policy-reporting.png":::

Select **Download report** to download the detailed report in a .csv format. This report contains the following fields:

- Site name
- URL
- Template
- Sensitivity label
- Retention policy
- Minimum owners or admins configured
- Number of site owners
- Email address of site owners
- Number of site admins
- Email address of site admins
- Managers of previous owners or admins
- Active members
- Total notifications count
- Action status of policy
- Action taken on (UTC)
- Last activity date (UTC)
- Site creation date (UTC)
- Storage used (GB)

## Notifications

Notifications are triggered only if the policy is running in Active mode.

Each policy runs every month to identify noncompliant sites. Email notifications are then sent to the configured set of recipients as per the policy.  

The potential recipients of these email notifications, if configured in the policy, are:

- **Current site owners:** If the minimum owner or admin count is set to 2 and the site has an existing site owner, they receive an email notification asking them to add another owner.  

- **Current site admins:** If the minimum owner or admin count is set to 2 and the site has an existing site admin, they receive an email notification asking them to add another owner.  

- **Managers of previous owners or admins:** If an owner or admin of a site leaves the organization, their managers are informed that the site needs an owner for effective management. If managers are members of a site, they can accept ownership. If they're visitors or don't have access to the site, they can coordinate with SharePoint admins to find the next best owner.  

  - As a user's details are deleted from the system 30 days after leaving the organization, managers might get only one notification about the site.

  - If the policy runs after 30 days of a user's leaving the organization, manager information won't be available, and notifications can't be sent.  

- **Active site members:** Based on policy configuration, emails are sent to the most active members of a site to accept ownership. Activity is determined based on the number of modifications, additions, and deletions the site members make to the documents located in a site.  

  > [!NOTE]
  > If a site has no one to be notified as per the email recipients provided during policy configuration, the count is provided in the summary. You can triage the sites and determine the next course of action.  

## Actions

If a site is identified as not meeting the ownership criteria for three consecutive months, one of the following actions is taken depending on what is configured:

**Do nothing**: There's no change to access, but subsequent notifications are paused and will resume after three months.

**Set access to read-only**: Site members and visitors can view content but no longer make edits. No further notifications are sent.

- If option is chosen and no one can be notified during the three months, the site continues to have its access set to read-only.

## Read-only mode

A site ownership policy configured with the read-only enforcement action sends additional notifications to inform recipients when there's no response.

A notification is sent when the site goes into read-only mode.

Once the site is in read-only mode, a banner is added to the site for users to identify this has happened.

To remove a site from read-only mode in the **SharePoint admin center**, go to the **Active sites** page, select the site, and then select **Unlock** from the site page panel.

Site owners can't remove a site from read-only mode and must contact the tenant admin to remove read-only mode.

## Related topics

- [SharePoint Advanced Management overview](advanced-management.md)
- [Site lifecycle policies - SharePoint Advanced Management](site-lifecycle-management.md)
