---
title: "Microsoft Edge management service"
ms.author: leahtu
author: dan-wesley
manager: archandr
ms.date: 06/14/2023
audience: ITPro
ms.topic: conceptual
ms.prod: microsoft-edge
ms.localizationpriority: medium
ms.collection: M365-modern-desktop
description: "Provides steps for configuring the Microsoft Edge management service."
---

# Microsoft Edge management service

The Microsoft Edge management service is an area in the Microsoft 365 admin center where admins can configure Microsoft Edge browser settings for their organization. These configurations are stored in the cloud and you can apply these settings to the browser using group assignment or group policy. Users must be logged into Microsoft Edge to retrieve these settings.

> [!NOTE]
> This experience is in public preview. We'll start rolling out this experience on June 9 and expect to finish the rollout by next week. You'll need to set up a Targeted release to opt in and view this experience in the Microsoft 365 admin center.
<!-- ====================================================================== -->
## Set up a Targeted release

There are two parts to setting up a Targeted release: identifying release preferences and picking the users for the release preference you configure.

Use the following steps as a guide to set up a Targeted release:

1. Sign into the Microsoft 365 admin center and then go to **Settings** > **Org settings**. Under the **Organization profile** tab, choose **Release preferences**. This window gives several release options: standard for everyone,  targeted for everyone, and targeted for selected users.
1. To enable a targeted release for all the users in your organization, select **Targeted release for everyone**, and then select **Save changes**.
1. To enable a targeted release for some people in your organization, select **Targeted release for selected users**, and then select **Save changes**. After you set up the release you want, the next step is to add the users for the release.
1. Choose **Select users** to add users one at a time, or **Upload users** to add them in bulk.
1. When you finish adding users, select **Save changes**.

For more information, see [Set up the Standard or Targeted release options](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide).
<!-- ====================================================================== -->
## Prerequisites

- You must have Microsoft Edge 115.0.1901.7 or greater installed.
- You must be a [Microsoft Edge Administrator](/azure/active-directory/roles/permissions-reference#edge-administrator) or a [Global Administrator](/azure/active-directory/roles/permissions-reference#global-administrator) to access the experience in Microsoft 365 Admin Center.
- You must be using one of the following supported operating systems: Windows 10+ or Windows Server 2016+. See [Microsoft Edge Supported Operating Systems](/deployedge/microsoft-edge-supported-operating-systems) for specifics.
<!-- ====================================================================== -->
## Access the preview experience

Use these steps to access the preview experience:

1. Go to the [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home#/homepage) and login.
1. In the main left navigation bar, go to **Settings** > **Microsoft Edge**.  
<!-- ====================================================================== -->
## Get started with configuration profiles

A configuration profile contains all the browser policy configurations, including extension settings.

Each configuration profile can only be assigned to one Azure Active Directory (Azure AD) group, and each group can only be assigned one configuration profile. However, the group that you select can contain other (nested) groups. If a user is a member of multiple Azure AD groups with conflicting policy settings, then the profile priority is used to determine which policy setting is applied. The highest priority is applied, with "1" being the highest priority that you can assign.

#### Create a configuration profile

Follow these steps to create a configuration profile:

1. Under the **Configuration profiles** pivot, select **Add a profile**.  
1. Under **Add a configuration profile**, enter a profile name and description and then select **Add**.  

After confirmation, you'll be able to go to the profile and configure the policies and extensions you want to use.

#### Copy a configuration profile

Follow these steps to copy a configuration profile:

1. Under the **Configuration profiles** pivot, select the profile you want to make a copy.
1. Select **Copy profile**.
1. Under **Copy configuration profile**, enter a profile name and description and then select **Add**.

After confirmation, the new profile is created with the same configurations as the profile you copied.

#### Reorder priority of configuration profile

Follow these steps to reorder the priority of a configuration profile:

1. Under the **Configuration profiles** pivot, select the profile you want to change and select  **Reorder priority**.
1. Under **Reorder profile priority**, pick a priority number from the dropdown list.
1. Select **Save** after you finish making your changes.  

#### Configure a policy for a configuration profile

Follow these steps to configure a policy for a configuration profile:

1. Under the **Configuration profiles** pivot, select the profile you want to configure a policy for.  
1. Under the **Policies** pivot, select **Select policy**.
1. Under **Configure a policy**, search for the policy you want to configure for this profile. Set the configuration settings/values for the policy you select.
1. Select **Save**.  

#### Assign a configuration profile to an Azure AD group

> [!NOTE]
> You can only assign one group to a profile. If you want to assign a different group, then you need to remove the existing group and then assign a new group to the profile.

Follow these steps to assign a configuration profile to an Azure AD group:

1. Under the **Configuration profiles** pivot, select the profile you want to assign.
1. Under the **Group assignment** pivot, select **Select group**.
1. Under **Select a security group**, select the group to assign the profile to.
1. Select **Select**. The profile will now be applied to all users in the selected group.

### Manage extensions

To manage extension settings for a profile, go **Microsoft Edge management**, select the profile you want to work with and then select the **Extensions** pivot. You can configure profile settings that apply to all extensions. Any extensions you add to be managed will appear in the profile. You can add an extension to the allow list, block list, or forced-installed list by setting the installation policy. If you configure specific settings on an individual extension, then those settings will override the profile settings.

#### Import existing extension settings to an existing configuration profile

Follow these steps to import extension settings:

1. Select the profile you want to import extension settings to and go to the **Extensions** pivot.
1. Select **Import JSON**.
1. Under **Import JSON**, browse for the JSON file that contains your extension settings and then select **Import**. Importing might overwrite any previous configurations. Note that it may take some time to complete the import if the file is large.

After confirmation, your profile will be populated with the imported settings.

#### Export extension settings to configure the ExtensionSettings policy

Follow these steps to export extension settings:

1. Select the profile you want to export extension settings from and go to the **Extensions** pivot.
1. Select **Export JSON** and the export will start downloading.

After the download is finished you can apply the JSON as a value to the [ExtensionSettings](/deployedge/microsoft-edge-policies#extensionsettings) group policy.

#### Manage settings for all extensions

Follow these steps to manage profile settings:

1. Select a profile and go to the **Extensions** pivot.
1. Select **Manage extensions** to configure any of the settings in the following table.

   | Setting | Description |
   |:-----|:-----|
   | Block all extensions | Users can't install any extensions (unless the extension is on the allow list). |
   | Allowed types of apps and extensions| Specify what types of app or extensions users are allowed to install. |
   | Install sources| Specify which URLs are allowed to install extensions. For URL pattern examples, see the [Defining match patterns](/microsoft-edge/extensions-chromium/developer-guide/match-patterns). |
   | External extensions | Allow or block installation of external extensions. |
   | Message for users when extension is blocked | Set a custom message that displays if users try to install a blocked extension. |
   | Blocked hosts | Prevent extensions from interacting with or modifying websites that you specify. The host pattern format is similar to [match patterns](/microsoft-edge/extensions-chromium/developer-guide/match-patterns) except you can't define the path. |
   | Allowed hosts | Allow extensions to interact with or modify websites, even if they're defined in blocked hosts. The host pattern format is similar to [match patterns](/microsoft-edge/extensions-chromium/developer-guide/match-patterns) except you can't define the path. |
   | Block extensions that require these permissions | Prevent users from installing/running extensions that need the permissions you select. |

1. When you're finished configuring extension settings, select **Save**.

#### Add an extension

Follow these steps to add an extension:

1. Select a profile and go to the **Extensions** pivot.
1. Select **Select extension**.
1. Under **Select an extension**, select an extension from the **Microsoft Edge Add-ons** store or specify an external extension ID.
1. Select **Select**.

#### Manage an extension

After selecting an extension, you can configure settings for a specific extension. These settings will only apply to the extension that you select and will override any profile settings.

##### Manage extension policy

Decide if an extension is allowed, blocked, or forced by setting its installation policy. Follow these steps to configure this setting:

1. Select an extension.
1. Select **Manage installation policy** and choose one of the following options from the dropdown list:

   - Allow: Users can install the extension. This is the default setting.
   - Block: Users can't install the extension. You could remove the extension if users previously installed it. Also, you can write a message that displays when users try to install the extension.
   - Force: The extension is automatically installed. Users can't remove it. You can optionally specify an update URL for the initial extension installation and use it for subsequent updates.
   - Normal: The extension is automatically installed. Users can disable it. You can optionally specify an update URL for the initial extension installation and use it for subsequent updates.

1. Select **Save**.

##### Manage hosts

Control what websites extensions can access. Prevent extensions from altering web pages by specifying which URLs should block extensions from making changes or reading data from. Allow extensions to interact with or modify websites, even if they're defined in blocked hosts. The host pattern format is similar to [match patterns](/microsoft-edge/extensions-chromium/developer-guide/match-patterns) except you can't define the path. Follow these steps to configure this setting:

1. Select an extension.
1. Select **Manage hosts**. In the **Hosts** window, specify blocked and allowed host URLs.
1. Select **Save**.

##### Manage permissions

Prevent users from installing and using the extension if it requires certain permissions that your organization doesn't allow. Follow these steps to configure this setting:

1. Select an extension.
1. Select **Manage permissions**. You can choose to use the default permissions that were defined in the profile settings or change these permissions. Use the **Permissions** window to allow all permissions, or customize permissions by choosing certain permissions that aren't allowed.
1. Select **Save**.

##### Edit minimum version

Specify the minimum version required for the extension. The extension will be disabled if it's a version older than what's specified, even if its installation policy is forced. The format of the version string is the same as the one used in the extension manifest. Follow these steps to configure this setting:

1. Select an extension.
1. Select **Edit minimum version**. In the **Minimum version required** window, enter the minimum version in the textbox.
1. Select **Save**.

##### Manage toolbar state

Choose how an extension is displayed in the toolbar. Follow these steps to configure this setting:

1. Select an extension.
1. Under **Toolbar state**, choose one of the following options:

   - Hidden: This is the default setting.
   - Shown: Show the extension on installation. Users can hide it from the toolbar.
   - Force shown: Always show extension on the toolbar. Users won't be able to hide it from the toolbar.

1. Select **Save**.

#### Manage sidebar apps

To manage sidebar apps for a profile, go to the profile and navigate to the **Extensions** pivot. You can allow, block, or force enable specific sidebar apps.

Use the following steps to manage sidebar apps:

1. Select **Select extension**.
1. Under **Select an extension**, navigate to the **Sidebar apps** pivot and select an app.
1. Select **Select**.

After selecting a sidebar app, you can configure its installation policy to Allow, Block, or Force.

### View extension requests

> [!NOTE]
> This feature is rolling out starting late June. Please check back again later if you don't see it.

If you blocked all extensions for your organization, you can see the extensions that your users are attempting to install. To view these extensions, go to a configuration profile and go to the "Requests" pivot. You can add an extension to the allow list, block list, or forced-installed list by setting the installation policy. To allow requests, use the [EdgeAdminCenterExtensionsFeedbackEnabled] policy to enable reporting.

To set the installation policy on a requested extension, use these steps:

1. Select an extension.
1. Select **Manage installation policy** and choose an option from the dropdown list:

   - Allow: Users can install the extension. This is the default setting.
   - Block: Users can't install the extension. You could remove the extension if users previously installed it. Also, you can write a message that displays when users try to install the extension.
   - Force: The extension is automatically installed. Users can't remove it. You can optionally specify an update URL for the initial extension installation and use it for subsequent updates.
   - Normal: The extension is automatically installed. Users can disable it. You can optionally specify an update URL for the initial extension installation and use it for subsequent updates.

1. Select **Save**.

<!-- ====================================================================== -->
## Configure Microsoft Edge to use a configuration profile

After configuring a profile, the next step is to assign the profile.  

> [!NOTE]
> Any policies you apply with Microsoft Edge Management Service will be overridden if they conflict with an existing Group Policy Object (GPO) or Mobile Device Management (MDM) policy that's set on the device.

### Enable the Microsoft Edge Management Service

Use the following steps as a guide to enable the Microsoft Edge Management Service.

1. Enable the Microsoft Edge Management Service by setting the [EdgeAdminCenterEnabled] policy to 1 and the [EdgeAdminCenterUseOCPSEndpoint] policy to 1. You can configure these settings in the registry under the key `SOFTWARE\Policies\Microsoft\Edge` in either `HKLM` or `HKCU`. If these keys aren't there you can create them. Use the following command line as a guide (use your profile ID):

   ```
   reg add HKLM\Software\Policies\Microsoft\Edge /v EdgeAdminCenterEnabled /t REG_DWORD /d 1
   reg add HKLM\Software\Policies\Microsoft\Edge /v EdgeAdminCenterUseOCPSEndpoint /t REG_DWORD /d 1
   ```

1. If Microsoft Edge is open, restart it.

If  MIcrosoft Edge is logged in as a user with an assigned policy, Microsoft Edge will download and apply the policy. For more information, see [Assign a configuration profile to an Azure AD group](#assign-a-configuration-profile-to-an-azure-ad-group) group.

### Set an enrollment token

If you don't want to assign the profile using group assignment in the Microsoft 365 Admin Center, then you can assign it through group policy. Each profile has a unique profile ID which is the value you can use for the [EdgeAdminCenterEnrollmentToken] policy to assign the profile. After assignment, the users will receive the profile and the settings will be applied when they're signed into the Edge browser. These policies will be applied in addition to any from group assignment in the Microsoft 365 Admin Center.

Use these steps as a guide for setting an enrollment token:

1. Repeat the previous steps to enable Microsoft Edge Management Service.
1. Log in to the Microsoft 365 Admin Center. Go to **Settings** > **Microsoft Edge**. Under the **Configuration profiles** pivot, go to the profile you want to assign.
1. Copy the token ID.
1. Set the [EdgeAdminCenterEnrollmentToken] policy value to the token ID. You can configure these settings in the registry under the key `SOFTWARE\Policies\Microsoft\Edge` in either `HKLM` or `HKCU`. If these keys aren't there you can create them. Use the following command line as a guide (use your token ID):

    ```
    reg add HKLM\Software\Policies\Microsoft\Edge /v EdgeAdminCenterEnrollmentToken /t REG_SZ /d 1bba4530-7d23-4512-acda-89248f8e3d47 
    ```

1. If Microsoft Edge is open, restart it.

#### Control policy source precedence

As stated previously, if policy is set in MDM or GPM, that value will override any value provided by Microsoft Edge Managment Service. If you want the Microsoft Edge Management Service policy to override MDM/GPM policy you can set the override in the  **CloudPolicyOverridesPlatformPolicy** policy. This is a private policy and must be set via the registry.

> [!IMPORTANT]
> This policy is highly experimental and will probably change in both name and functionality at any time before General Availability. Don't take any dependencies on it and only use it for testing.

Set the value of [CloudPolicyOverridesPlatformPolicy] under the key `SOFTWARE\Policies\Microsoft\Edge` in either `HKLM` or `HKCU`. If the key isn't there you can create it. In the following command line example, remember to use your token ID and restart Microsoft Edge if it's open.

```
reg add HKLM\Software\Policies\Microsoft\Edge /v CloudPolicyOverridesPlatformPolicy /t REG_ DWORD /d 1 
```

#### Control user/device policy precedence

Microsoft Edge policy has the concept of the audience that the policy is meant to apply to, this can be either "User" or "Device". In Microsoft Edge Management Service the policy applied via Group Assignment is applied as User Policy, while policy pulled down via [EdgeAdminCenterEnrollmentToken] is applied as Device Policy.

If there's a conflict with policy that User and Device are both trying to set, Device Policy takes precedence over User Policy. If you want to give User Policy precendence you can change precedence in [CloudUserPolicyOverridesCloudMachinePolicy] policy.

> [!IMPORTANT]
> This policy is highly experimental and will probably change in both name and functionality at any time before General Availability. Don't take any dependencies on it and only use it for testing.

Set the value of [CloudPolicyOverridesPlatformPolicy] under the key `SOFTWARE\Policies\Microsoft\Edge` in either `HKLM` or `HKCU`. If the key isn't there you can create it. In the following command line example, remember to use your token ID and restart Microsoft Edge if it's open.

```
reg add HKLM\Software\Policies\Microsoft\Edge /v CloudUserPolicyOverridesCloudMachinePolicy /t REG_ DWORD /d 1 
```
<!-- ====================================================================== -->
## Feedback and support

This experience is supported by Microsoft Support. You can reach out to Microsoft Support to report issues or give feedback. You can also leave feedback in our [TechCommunity forum](https://techcommunity.microsoft.com/t5/enterprise/bd-p/EdgeInsiderEnterprise).

## See also

- [Microsoft Edge Enterprise landing page](https://aka.ms/EdgeEnterprise)