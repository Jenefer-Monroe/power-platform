---
title: "Invite users with Azure Active Directory B2B collaboration  | MicrosoftDocs"
description: Invite users with Azure Active Directory B2B collaboration
ms.service: power-platform
ms.component: pa-admin
ms.topic: conceptual
ms.date: 02/04/2022
author: jimholtz
ms.subservice: admin
ms.author: jimholtz
ms.reviewer: jimholtz
ms.custom: "admin-security"
search.audienceType: 
  - admin
search.app:
  - D365CE
  - PowerApps
  - Powerplatform
  - Flow
contributors:
  - alaug
  - tapanm-msft
  - jimholtz
---
# Invite users with Azure Active Directory B2B collaboration

You can invite other users to access your environment. The [!INCLUDE[pn_Office_365](../includes/pn-office-365.md)] Global admin can do this through the [Azure portal](https://portal.azure.com). Invited users can access your environment using their own login credentials once a license and a security role are assigned to them. You don’t need to create a new user account and temporary password for these invited users in your own [!INCLUDE[pn_Office_365](../includes/pn-office-365.md)] tenant.  
  
## Requirements  
  
- To send  business-to-business (B2B) user invitations, you  must have an [!INCLUDE[pn_azure_active_directory](../includes/pn-azure-active-directory.md)] Global admin role.  
  
- To bulk- invite users, get the latest [!INCLUDE[pn_azure_active_directory](../includes/pn-azure-active-directory.md)][!INCLUDE[pn_PowerShell_short](../includes/pn-powershell-short.md)] which can be downloaded from the [PowerShell module's release page](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.98).  
  
## Incompatibilities  
 The following features are not supported for B2B invited users.  
  
1. [!INCLUDE[pn_unified_service_desk](../includes/pn-unified-service-desk.md)] client  
  
     Invited users will not be able to use the [!INCLUDE[pn_unified_service_desk](../includes/pn-unified-service-desk.md)] client to log into the host tenant’s environment.  
  
2. [!INCLUDE[pn_crm_app_for_outlook_short](../includes/pn-crm-app-for-outlook-short.md)]  
  
     Invited users will not be able to use their own tenant email addresses when performing email related transactions in the host environment. Server-side synchronization of invited users’ incoming and outgoing emails are not supported as there can be complications, especially for invited users who are already syncing their emails in their own tenant.  
  
3. Invited users cannot perform email activity using their own email address. The customer engagement apps (Dynamics 365 Sales, Dynamics 365 Customer Service, Dynamics 365 Field Service, Dynamics 365 Marketing, and Dynamics 365 Project Service Automation) only synchronizes incoming and outgoing emails from [!INCLUDE[pn_Microsoft_Exchange_Online](../includes/pn-microsoft-exchange-online.md)] that is hosted in the same [!INCLUDE[pn_Office_365](../includes/pn-office-365.md)] tenant.  
  
4. [!INCLUDE[pn_office_365_groups](../includes/pn-office-365-groups.md)]  
  
   [!INCLUDE[pn_office_365_groups](../includes/pn-office-365-groups.md)] connects a group to customer engagement apps. Data (including new conversations and documents) are stored in the [!INCLUDE[pn_Exchange](../includes/pn-exchange.md)] and/or [!INCLUDE[pn_SharePoint_short](../includes/pn-sharepoint-short.md)] system. Since invited users belong to a different [!INCLUDE[pn_Office_365](../includes/pn-office-365.md)] tenant, the invited users do not have permission to create [!INCLUDE[pn_office_365_groups](../includes/pn-office-365-groups.md)] in the invited-to [!INCLUDE[pn_Office_365](../includes/pn-office-365.md)] tenant. However, they can participate in the [!INCLUDE[pn_office_365_groups](../includes/pn-office-365-groups.md)] conversations as a guest in their [!INCLUDE[pn_Outlook_short](../includes/pn-outlook-short.md)] Inbox, but not within customer engagement apps.  
  
5. Dynamics 365 Customer Voice
   
   Invited users will not be able to use Dynamics 365 Customer Voice. You must create a new user in your tenant and then provide access to the new user.
   
6. Power Apps Maker experiences
   
   Invited users cannot sign in to https://make.powerapps.com or https://create.powerapps.com as a guest of a tenant. For the time being, users can only sign in to their home tenant in these maker experiences. 

## Invite a user  
 You can add users to through [!INCLUDE[pn_azure_active_directory](../includes/pn-azure-active-directory.md)] B2B user collaboration. Global admins and limited admins can use the [!INCLUDE[pn_azure_shortest](../includes/pn-azure-shortest.md)] portal to invite B2B collaboration users to the directory, to any security group, or to any application.  
  
 Admins can use one of the following methods to invite B2B users to their environment:  
  
1. Invite users to your environment that has a security group.  
  
   - See [Admins adding guest users to a group](/azure/active-directory/active-directory-b2b-admin-add-users).  
  
   - See [Control user access to environments: security groups and licenses](control-user-access.md) on how to use security groups for your environments.  

2. Invite users to your environment that does not have a security group.  
  
   -   See [Admins adding guest users to the directory](/azure/active-directory/active-directory-b2b-admin-add-users).  
  
3. Bulk-invite guest users using a .csv file.  
  
   -   See [PowerShell example](/azure/active-directory/b2b/code-samples).  
  
   Your invited user will receive an email invitation to get started with B2B user collaboration.  
  
   ![Email invitation sent to new user.](../admin/media/email-invitation-sent-new-user.png "Email invitation sent to new user")  
  
   When your user accepts the invitation by clicking on the **Get Started** link on the invitation email, they will be prompted to accept the invitation.  
  
   ![Accept the invitation.](../admin/media/accept-invitation-dynamics-365.png "Accept the invitation")  
  
> [!NOTE]
>  Until you add a license to the user account, the user will not have access to customer engagement apps. Follow the steps below to add a license through the [!INCLUDE[pn_azure_shortest](../includes/pn-azure-shortest.md)] portal.  
  
## Update user’s name and usage location  
 To assign a license, the invited user’s **Usage location** must be specified. Admins can update the invited user’s profile on the [!INCLUDE[pn_azure_shortest](../includes/pn-azure-shortest.md)] portal.  
  
1. Go  to **Azure Active Directory** > **Users and groups** > **All users**. If you don't see the newly created user, refresh the page.  
  
2. Click on the invited user, and then click **Profile**.  
  
   ![User Profile button in Azure Active Directory.](../admin/media/user-profile-button-azure-active-directory.png "User Profile button in Azure Active Directory")  
  
3. Update **First name**, **Last name**, and **Usage location**.  
  
   ![Update Azure Active Directory user profile.](../admin/media/update-azure-active-directory-user-profile.png "Update Azure Active Directory user profile")  
  
4. Click **Save**, and then close the Profile blade.  
  
## Assign invited users a license and security role  
 Assign your invited users a license and security role so the user can use customer engagement apps.  
  
1. Go  to **Azure Active Directory** > **Users and groups** > **All users**. If you don't see the newly created user, refresh the page.  
  
2. Click on the invited user, and then click **Licenses**.  
  
   ![Assign a license with the Azure portal.](../admin/media/assign-license-azure-portal.png "Assign a license with the Azure portal")  
  
3. Click ![New or Add button.](../admin/media/plus-2.png "New or Add button")**Assign**.  
  
4. Click **Configure required settings**.  
  
5. Select the product to license.  
  
   ![Click Assign to see the list of licenses.](../admin/media/click-assign-list-licenses.png "Click Assign to see the list of licenses")  
  
6. Click **Select**, and then click **Assign**.  
  
   Next, assign the invited users with appropriate security roles for the environment so they can access it. See [Create users](create-users.md).  
  
## Approve email or enable mailbox (not supported)  
 Since server-side synchronization is not supported, System admins cannot approve an invited email address or mailbox since emails cannot be synced from the invited user’s [!INCLUDE[pn_Microsoft_Exchange](../includes/pn-microsoft-exchange.md)].  
  
## Notify your invited users  
 To complete the user invitation, notify your invited users and provide them with the URL for the environment they are invited to (for example, https://contoso.crm.dynamics.com).  
 
 ## Power Apps support for B2B guest maker (preview)

> [!IMPORTANT]
> - This is a preview feature.
> - [!INCLUDE[cc_preview_features_definition](../includes/cc-preview-features-definition.md)] 

B2B guest users can [run Power Apps](/powerapps/maker/canvas-apps/share-app-guests). With this preview feature, B2B guests can now create [custom SharePoint forms using Power Apps](/powerapps/maker/canvas-apps/customize-list-form).

Follow these steps to allow B2B guest users to create custom SharePoint list forms using Power Apps.

> [!NOTE]
> Ensure that you perform below steps on the **resource tenant**, and not on the **home tenant**.
> - A **resource tenant** is where the SharePoint list exists, and where the user is expected to create the custom SharePoint list form using Power Apps as a guest.
> - A **home tenant** is where the user's account resides and authenticates against.

1. Use the following PowerShell cmdlet to enable guests to make Power Apps.

    ```PowerShell
    $requestBody = Get-TenantSettings 
    $requestBody.powerPlatform.powerApps.enableGuestsToMake = $True 
    Set-TenantSettings $requestBody 
    ```

1. Assign the [Environment Maker](database-security.md) security role to the B2B guest users that you want to be able to create custom SharePoint list forms using Power Apps.

    > [!TIP]
    > In addition, you can also review all other members of this security role (especially in the default environment), and remove users that aren't expected to have this privilege.

After the B2B guest users are given the required permissions to edit the SharePoint list as a guest, they can now [create](/powerapps/maker/canvas-apps/customize-list-form#open-the-form) custom SharePoint list forms using Power Apps.

### See also  
 [Azure AD B2B Collaboration is Generally Available!](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/12/azure-ad-b2b-collaboration-is-generally-available/)   
 [Azure Active Directory B2B collaboration code and PowerShell samples](/azure/active-directory/b2b/code-samples)   
 [Azure Active Directory B2B collaboration frequently-asked questions (FAQ)](/azure/active-directory/active-directory-b2b-faq)   
 [Azure Active Directory B2B Collaboration](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)   
 [Azure AD B2B: New updates make cross-business collab easy](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/)

[Share a canvas app with guest users](/powerapps/maker/canvas-apps/share-app-guests)

[!INCLUDE[footer-include](../includes/footer-banner.md)]
