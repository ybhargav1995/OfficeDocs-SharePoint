---
ms.date: 11/18/2024
title: "Initiate site access reviews for Data access governance reports"
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
- admindeeplinkSPO
search.appverid:
description: "Learn about how to initiate site access reviews as a remedial action for data access governance for SharePoint sites."
---

# Initiate site access reviews for Data access governance reports

[!INCLUDE[Advanced Management](includes/advanced-management.md)]

Site access review in the [SharePoint admin center](https://go.microsoft.com/fwlink/?linkid=2185219) lets [IT administrators](/microsoft-365/admin/add-users/assign-admin-roles) delegate the review process of [data access governance reports](data-access-governance-reports.md) to the site owners of overshared sites.

Site access review involves site owners in the review process so they can address the concern of overshared sites identified in data access governance reports. This feature is crucial because:

- IT administrators can't have access to file-level or item-level details due to compliance reasons.
- Site owners are best positioned to review and address oversharing issues for their own sites.

## Prerequisites

To use the site access review feature, you must fulfill the following prerequisites:

- Have a [Microsoft SharePoint Premium - SharePoint Advanced Management](advanced-management.md) subscription
- Run a non-government cloud tenant environment. Site access review isn't supported in government cloud environments such as GCCH/GCC-Moderate/DoD/Gallatin
- Have admin credentials to access the SharePoint admin center to initiate an access review
- Have site owners respond to the review requests, take necessary actions, and complete the review

## How site access review works

- Site access review is accessible only for the top 100 sites shown in the data access governance reports. Site access review specifically targets the oversharing scenario identified in the selected data access governance report.
- When you initiate a review, the system generates a context-specific email for the site owner.
- For example, if you initiate a site access review for a report from the "Content shared with 'Everyone except external users'" category, the review email exclusively addresses sharing issues regarding that particular report.

## Support matrix

Currently, site access review is available for

- All Sharing link reports (Anyone, PeopleInYourOrg, Specific people shared externally)
- "Content shared with 'Everyone except external users'" reports.
- Oversharing baseline report using permissions

## Initiate a site access review

1. Sign in to SharePoint admin center with your admin credentials.
1. Expand the **Reports** section and select **Data access governance**.
1. Under "Content shared with 'Everyone except external users", select **View reports**.
1. Select a report and choose the sites you want to review.

   :::image type="content" source="./media/data-access-governance/initiate-site-access-review.png" alt-text="Screenshot that shows Initiate site access review for sites listed within DAG report" lightbox="./media/data-access-governance/initiate-site-access-review.png":::

1. Select **Initiate site access review**.
1. Add comments in the provided section to give context to site owners.

    :::image type="content" source="./media/data-access-governance/comments-site-access-review.png" alt-text="Screenshot that shows provide comments for context setting for site owners":::

1. Select **Send** to initiate the review request.

For reports available only via PowerShell such as Oversharing baseline report using permissions, site access review can also be initiated using [PowerShell commands](powershell-for-data-access-governance.md#initiate-site-access-review-using-powershell).

### Track initiated site access reviews

To see a list of all initiated site access reviews, select the **My review requests** tab from the data access governance landing page.

:::image type="content" source="./media/data-access-governance/my-review-requests.png" alt-text="Screenshot that shows track all reviews initiated from a central page" lightbox="./media/data-access-governance/my-review-requests.png":::

When you initiate a site access review, it remains in a pending state until the site owner completes the review. Once the site owner completes the review, the status and comments are updated with the name of the reviewer and time and date of completion. A review can be marked as failed if site access review couldn't determine a valid email ID for the site owner to deliver the site access review.

For reports available only via PowerShell such as Oversharing baseline report using permissions, site access review can also be tracked using this [PowerShell command](powershell-for-data-access-governance.md#track-site-access-reviews-using-powershell).

### Site access review process (for site owners)

When you initiate a review, site owners receive an email for each site that requires attention. The email includes:

- Relevant title
- Your comments (if any)
- A request to review site permissions
- A link to a detailed access review page. This page is specific for the scenario as specified in the data access governance report.

The following image shows the email notification regarding 'Everyone except external users' last 28 days report:

:::image type="content" source="./media/data-access-governance/email-eeeu-files-folders-lists.png" alt-text="Screenshot that shows Email received by site owners for oversharing via EEEU" lightbox="./media/data-access-governance/email-eeeu-files-folders-lists.png":::

The following image shows a report of shared links generated in the last 28 days:

:::image type="content" source="./media/site-access-review/6-detailed-sharing-links.png" alt-text="Screenshot that shows the sharing links within the last 28 days report." lightbox="./media/site-access-review/6-detailed-sharing-links.png":::

The following image shows the oversharing baseline report using permissions:
:::image type="content" source="./media/site-access-review/5-detailed-permissions-report.png" alt-text="Screenshot that shows the detailed oversharing permissions reports." lightbox="./media/site-access-review/5-detailed-permissions-report.png":::

#### Review 'Everyone except external users' site access review requests (for site owners)

Site owners can review and manage access in two main areas:

- **SharePoint groups:**
  - View which groups contain 'Everyone except external users'.
  - See when and by whom the group was added.
  - Remove 'Everyone except external users' from groups if necessary:
    1. Selecting the SharePoint group opens the group membership page that displays all members of this SharePoint group.
    2. Select **Everyone except external users** and **Actions** and choose to **remove users from group**.

        :::image type="content" source="./media/data-access-governance/manage-sharepoint-group-membership.png" alt-text="Screenshot that shows displays sharepoint group members" lightbox="./media/data-access-governance/manage-sharepoint-group-membership.png":::

- **Individual items (files/folders/lists):**
  - See items shared with 'Everyone except external users' in the last 28 days.
  - View sharing details (who shared and when).
  - Manage access and remove permissions as needed:
    1. Select **Manage access**.
    1. Under the 'Everyone except external users' group in the **Groups** tab, select the group and select **remove access**. See [Stop sharing OneDrive or SharePoint files or folders, or change permissions](https://support.microsoft.com/office/stop-sharing-onedrive-or-sharepoint-files-or-folders-or-change-permissions-0a36470f-d7fe-40a0-bd74-0ac6c1e13323) for more information.

        :::image type="content" source="./media/data-access-governance/site-owner-view-foreeeu-files.png" alt-text="Screenshot that shows view for site owner regarding items shared with eeeu" lightbox="./media/data-access-governance/site-owner-view-foreeeu-files.png":::

#### Review 'Sharing link reports' site access review requests (for site owners)

Once the site owner selects the email, they're redirected to the site access review detailed report generated for the site.

The site owner gets a view of files for whom links were generated along with the exact time of generation and who generated the links. The 'Manage access' button can be used to navigate to the link section and remove it/modify the permissions.

The following image shows an email notification about the sharing links report using permissions:
:::image type="content" source="./media/site-access-review/3-email-permissions-report.png" alt-text="Screenshot that shows the sharing links report email notification." lightbox="./media/site-access-review/3-email-permissions-report.png":::

#### Review 'Oversharing baseline using permission reports' site access review requests (for site owners)

Once the site owner selects the email, they're redirected to the site access review detailed report generated for the site.

The following image shows an email notification about oversharing baseline report using permissions:
:::image type="content" source="./media/site-access-review/2-email-permissions-report.png" alt-text="Screenshot that shows the oversharing baseline using permission reports email notification." lightbox="./media/site-access-review/2-email-permissions-report.png":::

The SharePoint admin views the unique number of permissioned users for this site in the Data access governance report and that number is also visible to site owner in the site access review email. This list shows how those users are distributed across the site content in terms of permissions and scopes.

All items created in the site, by default, inherit permissions of the site and thus the 'site' acts like a parent. However, if the inherited permissions are broken due to sharing of an item by creating links, providing direct access to individuals or groups, removing users/groups etc., a unique scope is created for that item. Now this item acts as a new 'parent' and its children inherit its permissions. The site access review page is a list of such uniquely permissioned 'parents' with the appropriate scope and name. It's not the list of all items/files/folders in the site. The item with the highest number of permissioned users is shown first. Up to 100 items are shown in descending order so that site owner can focus on items with highest 'exposure' first.

##### Understanding the site access review report for permission based reports

**Number of permissioned users:** This column represents the number of users permissioned to that scope (Site/List/Folder/File) and hence illustrates the current 'exposure' for that item, as compared to other items. However, this number is NOT a unique number of users. In case the same user has both direct and indirect permissions to this item, the user is double counted.

For example, a folder 'F' was shared to a group “A” consisting of 40 members and is directly shared with 10 individuals and 20 more individuals arrived using sharing links. The number of permissioned users is the sum of all users - 80 (40+10+20). No deduplication is done to see if the same user exists in groups or came via sharing links as well.

Also, the sum of permissioned users across all scopes might not equal the number of users in the email and/or Data access governance report and could be greater. This scenario can happen when a user has permissions across multiple items. At the site-level, such a user is counted once. However, at an item-level, that user is counted individually.

**Number of groups:** As the name suggests, this shows the number of groups having permissions to this scope/item. Usually, the exposure is caused by groups containing many users. Reducing exposure removes the permissions of groups and can edit their memberships. Select **Group number** to view the membership count of each group and identify which groups to target.

The other columns show the number of ALL existing links (Anyone, PeopleInOrg) and the presence of EEEU/Everyone. If the number of links are high, or the EEEU/Everyone column says yes, the site owner can immediately target the relevant item/scope for reducing permissions.

**Manage Access:** The 'Manage access' button allows the site owner to remove individual users, groups, delete links, or modify permissions accordingly. For a 'SharePoint site' scope, the button directs the site owner to SharePoint group management page, whereas for individual items, it uses the existing 'Manage access' experience.
With this report, a site owner gets an overview of 'exposure' of parent items in their sites, can gauge the contribution of exposure and act via 'manage access' without having to manually iterate through every permission of every item in the site.

#### Complete site access review requests (for site owners)

Once the site owner takes the necessary actions like modifying or removing permissions, the site owner should:

1. Select **Complete review**.
2. Add any relevant comments.
3. Submit the completed review.

   Comments are shared back to the IT administrator who raised the review request. The review request is then marked as completed.

#### Manage multiple site access review requests (for site owners)

A site owner can receive review requests for multiple sites, or receive multiple reviews for different scenarios for the same site. A site owner can track all requests by selecting the **Site reviews** page found in the left panel.

:::image type="content" source="./media/data-access-governance/site-review-master-page.png" alt-text="Screenshot that shows Master page to track all site review for a site" lightbox="./media/data-access-governance/site-review-master-page.png":::

For site owners handling multiple reviews:

1. Access the 'site reviews' page via:
    - The link in the review email.
    - The gear icon on the site home page:
        1. Select **Site settings**.
        1. Select **Site reviews**.
        :::image type="content" source="./media/data-access-governance/site-review-from-gear-icon.png" alt-text="Screenshot that shows path to site review page from site home page under gear icon" lightbox="./media/data-access-governance/site-review-from-gear-icon.png":::
1. View all pending site access reviews.
1. Complete reviews as necessary.

## Related topics

[Data access governance](data-access-governance-reports.md)

[Microsoft SharePoint Premium - SharePoint advanced management](advanced-management.md)
