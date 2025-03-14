---
title: Insider risk management settings
description: Learn about insider risk management settings in Microsoft Purview
keywords: Microsoft 365, Microsoft Purview, insider risk, risk management, compliance
ms.localizationpriority: medium
ms.service: O365-seccomp
ms.topic: article
f1.keywords:
- NOCSH
ms.author: robmazz
author: robmazz
manager: laurawi
audience: itpro
ms.collection:
- highpri 
- tier1
- purview-compliance
- m365solution-insiderrisk
- m365initiative-compliance
- highpri
ms.custom: admindeeplinkCOMPLIANCE
---

# Get started with insider risk management settings

> [!IMPORTANT]
> Microsoft Purview Insider Risk Management correlates various signals to identify potential malicious or inadvertent insider risks, such as IP theft, data leakage and security violations. Insider risk management enables customers to create policies to manage security and compliance. Built with privacy by design, users are pseudonymized by default, and role-based access controls and audit logs are in place to help ensure user-level privacy.

Insider risk management settings apply to all insider risk management policies, regardless of the template you choose when creating a policy. Settings are configured using the **Insider risk settings** control located at the top of all insider risk management pages. These settings control policy components for the following areas:

- [Privacy](#privacy)
- [Indicators](#indicators)
- [Policy timeframes](#policy-timeframes)
- [Intelligent detections](#intelligent-detections)
- [Export alerts](#export-alerts)
- [Priority user groups](#priority-user-groups)
- [Priority physical assets (preview)](#priority-physical-assets-preview)
- [Power Automate flows (preview)](#power-automate-flows-preview)
- [Microsoft Teams (preview)](#microsoft-teams-preview)
- [Analytics](#analytics)
- [Admin notifications](#admin-notifications)

Before you get started and create insider risk management policies, it's important to understand these settings and choose setting levels best for the compliance needs for your organization.

[!INCLUDE [purview-preview](../includes/purview-preview.md)]

## Privacy

Protecting the privacy of users that have policy matches is important and can help promote objectivity in data investigation and analysis reviews for insider risk alerts. For users with an insider risk policy match, you can choose one of the following settings:

- **Show anonymized versions of usernames**: Names of users are anonymized to prevent admins, data investigators, and reviewers from seeing who is associated with policy alerts. For example, a user 'Grace Taylor' would appear with a randomized pseudonym such as 'AnonIS8-988' in all areas of the insider risk management experience. Choosing this setting anonymizes all users with current and past policy matches and applies to all policies. User profile information in the insider risk alert and case details won't be available when this option is chosen. However, usernames are displayed when adding new users to existing policies or when assigning users to new policies. If you choose to turn off this setting, usernames will be displayed for all users that have current or past policy matches.

    > [!IMPORTANT]
    > To maintain referential integrity for users who have insider risk alerts or cases in Microsoft 365 or other systems, anonymization of usernames isn't preserved for exported alerts. Exported alerts will display usernames for each alert.

- **Do not show anonymized versions of usernames**: Usernames are displayed for all current and past policy matches for alerts and cases. User profile information (the name, title, alias, and organization or department) is displayed for the user for all insider risk management alerts and cases.

![Insider risk management privacy settings.](../media/insider-risk-settings-privacy.png)

## Indicators

Insider risk policy templates define the type of risk activities that you want to detect and investigate. Each policy template is based on specific indicators that correspond to specific triggers and risk activities. All global indicators are disabled by default, and you must select one or more indicators to configure an insider risk management policy.

Signals are collected and alerts are triggered by policies when users perform activities related to indicators. Insider risk management uses different types of events and indicators to collect signals and create alerts:

- **Triggering events**: Events that determine if a user is active in an insider risk management policy. If a user is added to an insider risk management policy doesn't have a triggering event, the user isn't evaluated by the policy as a potential risk. For example, User A is added to a policy created from the *Data theft by departing users* policy template and the policy and Microsoft 365 HR connector are properly configured. Until User A has a termination date reported by the HR connector, User A isn't evaluated by this insider risk management policy for potential risk. Another example of a triggering event is if a user has a *High* severity DLP policy alert when using *Data leaks* policies.
- **Global settings indicators**: Indicators enabled in global settings for insider risk management define both the indicators available for configuration in policies and the types of events signals collected by insider risk management. For example, if a user copies data to personal cloud storage services or portable storage devices and these indicators are selected only in global settings, the user's potentially risky activity will be available for review in the Activity explorer. However, if this user wasn't defined in an insider risk management policy, the user isn't evaluated by the policy as a potential risk and therefore won't be assigned a risk score or generate an alert.
- **Policy indicators**: Indicators included in insider risk management policies are used to determine a risk score for an in-scope user. Policy indicators are enabled from indicators defined in global settings and are only activated after a triggering event occurs for a user.  Some examples of policy indicators are when a user copies data to personal cloud storage services or portable storage devices, if a user account is removed from Azure Active Directory, or if a user shares internal files and folders with unauthorized external parties.

Certain policy indicators and sequences may also be used for customizing triggering events for specific policy templates. When configured in the policy wizard for the *General data leaks* or *Data leaks by priority users* templates, these indicators or sequences allow you more flexibility and customization for your policies and when users are in-scope for a policy. Also, you can define risk management activity thresholds for these triggering indicators for more fine-grained control in a policy.

Policy indicators are segmented into the following areas. You can choose the indicators to activate and customize indicator event limits for each indicator level when creating an insider risk policy:

- **Office indicators**: These include policy indicators for SharePoint sites, Microsoft Teams, and email messaging.
- **Device indicators**: These include policy indicators for activity such as sharing files over the network or with devices. Indicators include activities involving all file types, excluding executable (.exe) and dynamic link library (.dll) file activity. If you select *Device indicators*, activity is processed for devices with Windows 10 Build 1809 or higher and macOS (three latest released versions) devices. For both Windows and macOS devices, you must first onboard devices to the compliance portal. Device indicators also include browser signal detection to help your organization detect and act on exfiltration signals for non-executable files viewed, copied, shared, or printed in Microsoft Edge and Google Chrome. For more information on configuring Windows devices for integration with insider risk, see the following [Enable device indicators and onboard Windows devices](insider-risk-management-settings.md#OnboardDevices) section in this article. For more information on configuring macOS devices for integration with insider risk, see the following Enable device indicators and onboard macOS devices section in this article. For more information about browser signal detection, see [Learn about and configure insider risk management browser signal detection](insider-risk-management-browser-support.md).
- **Microsoft Defender for Endpoint indicators (preview)**: These include indicators from Microsoft Defender for Endpoint related to unapproved or malicious software installation or bypassing security controls. To receive alerts in insider risk management, you must have an active Defender for Endpoint license and insider risk integration enabled. For more information on configuring Defender for Endpoint for insider risk management integration, see [Configure advanced features in Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/advanced-features\#share-endpoint-alerts-with-microsoft-compliance-center).
- **Risky browsing indicators (preview)**: These include policy indicators for user browsing activity related to websites that are considered malicious or risky and pose potential insider risk that may lead to a security or compliance incident. Risky browsing activity refers to users who visit potentially risky websites, such as those associated with malware, pornography, violence, and other unallowed activities. To include these risk management activities in policy alerts, select one or more indicators in this section. To learn about configuring browser exfiltration signals, see [Insider risk management browser signal detection](insider-risk-management-browser-support.md).
- **Physical access indicators (preview)**: These include policy indicators for physical access to sensitive assets. For example, attempted access to a restricted area in your physical badging system logs can be shared with insider risk management policies. To receive these types of alerts in insider risk management, you must have priority physical assets enabled in insider risk management and the [Physical badging data connector](import-physical-badging-data.md) configured. To learn about configuring physical access, see the [Priority physical access section](#priority-physical-assets-preview) in this article.
- **Microsoft Defender for Cloud Apps indicators (preview)**: These include policy indicators from shared alerts from Defender for Cloud Apps. Automatically enabled anomaly detection in Defender for Cloud Apps immediately starts detecting and collating results, targeting numerous behavioral anomalies across your users and the machines and devices connected to your network. To include these risk management activities in policy alerts, select one or more indicators in this section. To learn more about Defender for Cloud Apps analytics and anomaly detection, see [Get behavioral analytics and anomaly detection](/cloud-app-security/anomaly-detection-policy).
- **Health record access indicators**: These include policy indicators for patient medical record access. For example, attempted access to patient medical records in your electronic medical records (EMR) system logs can be shared with insider risk management healthcare policies. To receive these types of alerts in insider risk management, you must have a healthcare-specific data connector and the HR data connector configured.
- **Risk score boosters**: These include raising the risk score for potentially risky activity that is above what is typical or for users with previous cases resolved as a policy violation. Enabling risk score boosters increase risk scores and the likelihood of alerts for these types of activities. For risk management activity that is above what is typical, scores are boosted if the detected potentially risky activity deviates from activities that are considered compliant. For users with previous cases resolved as a policy violation, scores are boosted if a user had more than one case previously resolved as a confirmed policy violation. Risk score boosters can only be selected if one or more indicators are selected.

In some cases, you may want to limit the insider risk policy indicators that are applied to insider risk policies in your organization. You can turn off the policy indicators for specific areas by disabling them from all insider risk policies in global settings. Triggering events can only be modified for policies created from the *Data leaks* or *Data leaks by priority users* templates. Policies created from all other templates don't have customizable triggering indicators or events.

To define the insider risk policy indicators that are enabled in all insider risk policies, navigate to **Insider risk settings** > **Indicators** and select one or more policy indicators. The indicators selected on the **Indicators** settings page can't be individually configured when creating or editing an insider risk policy in the policy wizard.

> [!NOTE]
> It may take several hours for new manually-added users to appear in the **Users dashboard**. Activities for the previous 90 days for these users may take up to 24 hours to display. To view activities for manually added users, select the user on the **Users dashboard** and open the **User activity** tab on the details pane.

### Enable device indicators and onboard Windows devices
<a name="OnboardDevices"> </a>

To enable the detection of risk activities on Windows devices and include policy indicators for these activities, your Windows devices must meet the following requirements and you must complete the following onboarding steps.

#### Step 1: Prepare your endpoints

Make sure that the Windows 10 devices that you plan on reporting in insider risk management meet these requirements.

1. Must be running Windows 10 x64 build 1809 or later and must have installed the [Windows 10 update (OS Build 17763.1075)](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818) from February 20, 2020.
2. The user account used to log into the Windows 10 device must be an active Azure Active Directory (AAD) account. The Windows 10 device may be [AAD](/azure/active-directory/devices/concept-azure-ad-join), hybrid AAD, or Active Directory joined, or AAD registered.
3. Install the Microsoft Edge browser on the endpoint device to detect actions for the cloud upload activity. See, [Download the new Microsoft Edge based on Chromium](https://support.microsoft.com/help/4501095/download-the-new-microsoft-edge-based-on-chromium).

#### Step 2: Onboarding devices
<a name="OnboardStep2"> </a>

You must enable device checking and onboard your endpoints before you can detect insider risk management activities on a device. Both actions are taken in the Microsoft Purview compliance portal.

When you want to enable devices that haven't been onboarded yet, you need to download the appropriate script and deploy it as outlined below.

If you already have devices onboarded into [Microsoft Defender for Endpoint](/windows/security/threat-protection/), they'll already appear in the managed devices list. Follow [Step 3: If you have devices onboarded into Microsoft Defender for Endpoint](insider-risk-management-settings.md#OnboardStep3) in the next section.

In this deployment scenario, you'll enable devices that haven't been onboarded yet, and you just want to detect insider risk activities on Windows devices.

1. Open the [Microsoft Purview compliance portal](https://compliance.microsoft.com).
2. Open the compliance portal settings page and choose **Onboard devices**.

   > [!NOTE]
   > While it usually takes about 60 seconds for device onboarding to be enabled, please allow up to 30 minutes before engaging with Microsoft support.

3. Choose **Device management** to open the **Devices** list. The list will be empty until you onboard devices.
4. Choose **Onboarding** to begin the onboarding process.
5. Choose the way you want to deploy to these more devices from the **Deployment method** list and then **download package**.
6. Follow the appropriate procedures in [Onboarding tools and methods for Windows machines](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints). This link takes you to a landing page where you can access Microsoft Defender for Endpoint procedures that match the deployment package you selected in step 5:
    - Onboard Windows machines using Group Policy
    - Onboard Windows machines using Microsoft Endpoint Configuration Manager
    - Onboard Windows machines using Mobile Device Management tools
    - Onboard Windows machines using a local script
    - Onboard non-persistent virtual desktop infrastructure (VDI) machines.

Once done and endpoint is onboarded, it should be visible in the devices list and the endpoint will start reporting audit activity logs to insider risk management.

> [!NOTE]
> This experience is under license enforcement. Without the required license, data will not be visible or accessible.

#### Step 3: If you have devices onboarded into Microsoft Defender for Endpoint
<a name="OnboardStep3"> </a>

If Microsoft Defender for Endpoint is already deployed and there are endpoints reporting in, all these endpoints will appear in the managed devices list. You can continue to onboard new devices into insider risk management to expand coverage by using the [Step 2: Onboarding devices](insider-risk-management-settings.md#OnboardStep2) section.

1. Open the [Microsoft Purview compliance portal](https://compliance.microsoft.com).
2. Open the compliance portal settings page and choose **Enable device monitoring**.
3. Choose **Device management** to open the **Devices** list. You should see the list of devices that are already reporting into Microsoft Defender for Endpoint.
4. Choose **Onboarding** if you need to onboard more devices.
5. Choose the way you want to deploy to these more devices from the **Deployment method** list and then **Download package**.
6. Follow the appropriate procedures in [Onboarding tools and methods for Windows machines](/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints). This link takes you to a landing page where you can access Microsoft Defender for Endpoint procedures that match the deployment package you selected in step 5:
    - Onboard Windows machines using Group Policy
    - Onboard Windows machines using Microsoft Endpoint Configuration Manager
    - Onboard Windows machines using Mobile Device Management tools
    - Onboard Windows machines using a local script
    - Onboard non-persistent virtual desktop infrastructure (VDI) machines.

Once done and endpoint is onboarded, it should be visible under the **Devices** table and the endpoint will start reporting audit activity logs to insider risk management.

> [!NOTE]
> This experience is under license enforcement. Without the required license, data will not be visible or accessible.

### Enable device indicators and onboard macOS devices

macOS devices (Catalina 10.15 or later) can be onboarded into Microsoft 365 to support insider risk management policies using either Intune or JAMF Pro. For more information and configuration guidance, see [Onboard macOS devices into Microsoft 365 overview (preview)](device-onboarding-macos-overview.md).

### Indicator level settings (preview)

When creating a policy using the policy wizard, you can configure how the daily number of risk events should influence the risk score for insider risk alerts. These indicator settings help you control how the number of occurrences of risk events in your organization should affect the risk score, and so the associated alert severity, for these events. If you prefer, you can also choose to keep the default event threshold levels recommended by Microsoft for all enabled indicators.

For example, you decide to enable SharePoint indicators in the insider risk policy settings and to **set custom thresholds** for SharePoint events when configuring indicators for a new insider risk *Data leaks* policy. While in the insider risk policy wizard, you configure three different daily event levels for each SharePoint indicator to influence the risk score for alerts associated with these events.

![Insider risk management custom indicator settings](../media/insider-risk-custom-indicators.png)

For the first daily event level, you set the threshold at *10 or more events per day* for a lower impact to the risk score for the events, *20 or more events per day* for a medium impact to the risk score for the events, and *30 or more events per day* a higher impact to the risk score for the events. These settings effectively mean:

- If there are 1-9 SharePoint events that take place after triggering event, risk scores are minimally impacted and would tend not to generate an alert.
- If there are 10-19  SharePoint events that take place after a triggering event, the risk score is inherently lower and alert severity levels would tend to be at a low level.
- If there are 20-29 SharePoint events that take place after a triggering, the risk score is inherently higher and alert severity levels would tend to be at a medium level.
- If there are 30 or more SharePoint events that take place after a triggering, the risk score is inherently higher and alert severity levels would tend to be at a high level.

Another option for policy thresholds is to assign the policy triggering event to risk management activity that is above the typical daily amount of users. Instead of being defined by specific threshold settings, each threshold is dynamically customized for anomalous activities detected for in-scope policy users. If threshold activity for anomalous activities is supported for an individual indicator, you can select **Activity is above user's usual activity for the day** in the policy wizard for that indicator. If this option isn't listed, anomalous activity triggering isn't available for the indicator. If the **Activity is above user's usual activity for the day** option is listed for an indicator, but not selectable, you need to enable this option in **Insider risk settings** > **Policy indicators**.

## Policy timeframes

Policy timeframes allow you to define past and future review periods that are triggered after policy matches based on events and activities for the insider risk management policy templates. Depending on the policy template you choose, the following policy timeframes are available:

- **Activation window**: Available for all policy templates, the *Activation window* is the defined number of days that the window activates **after** a triggering event. The window activates for 1 to 30 days after a triggering event occurs for any user assigned to the policy. For example, you've configured an insider risk management policy and set the *Activation window* to 30 days. Several months have passed since you configured the policy, and a triggering event occurs for one of the users included in the policy. The triggering event activates the *Activation window* and the policy is active for that user for 30 days after the triggering event occurred.
- **Past activity detection**: Available for all policy templates, the *Past activity detection* is the defined number of days that the window activates **before** a triggering event. The window activates for 0 to 90 days before a triggering event occurs for any user assigned to the policy. For example, you've configured an insider risk management policy and set the *Past activity detection* to 90 days. Several months have passed since you configured the policy, and a triggering event occurs for one of the users included in the policy. The triggering event activates the *Past activity detection* and the policy gathers historic activities for that user for 90 days prior to the triggering event.

![Insider risk management timeframe settings.](../media/insider-risk-settings-timeframes.png)

## Intelligent detections

Intelligent detection settings help refine how the detections of risky activities are processed for alerts. In certain circumstances, you may need to define file types to ignore, or you want to enforce a detection level for daily events to boost risk scores for users. Use these settings to control file type exclusions, boosting risk score for potentially risky activity, and file volume limits.

### File activity detection

To exclude specific file types from all insider risk management policy matching, enter file type extensions separated by commas. For example, to exclude certain types of music files from policy matches you may enter *aac,mp3,wav,wma* in the **File type exclusions** field. Files with these extensions will be ignored by all insider risk management policies.

### Alert volume

Potentially risky activities detected by insider risk policies are assigned a specific risk score, which in turn determines the alert severity (low, medium, high). By default, we'll generate a certain amount of low, medium, and high severity alerts, but you can increase or decrease the volume to suit your needs. To adjust the volume of alerts for all insider risk management policies, choose one of the following settings:

- **Fewer alerts**: You'll see all high severity alerts, fewer medium severity alerts, and no low severity ones. This setting level means you might miss some true positives.
- **Default volume**: You'll see all high severity alerts and a balanced amount of medium and low severity alerts.
- **More alerts**: You'll see all medium and high severity alerts and most low severity alerts. This setting level might result in more false positives.

### Microsoft Defender for Endpoint alert statuses

[Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) is an enterprise endpoint security platform designed to help enterprise networks prevent, detect, investigate, and respond to advanced threats. To have better visibility of security violations in your organization, you can import and filter Defender for Endpoint alerts for activities used in policies created from insider risk management security violation policy templates.

Depending on the types of signals you're interested in, you can choose to import alerts to insider risk management based on the Defender for Endpoint alert triage status. You can define one or more of the following alert triage statuses in the global settings to import:

- Unknown
- New
- In progress
- Resolved

Alerts from Defender for Endpoint are imported daily. Depending on the triage status you choose, you may see multiple user activities for the same alert as the triage status changes in Defender for Endpoint.

For example, if you select *New*, *In progress*, and *Resolved* for this setting, when a Microsoft Defender for Endpoint alert is generated and the status is *New*, an initial alert activity is imported for the user in insider risk. When the Defender for Endpoint triage status changes to *In progress*, a second activity for this alert is imported for the user in insider risk. When the final Defender for Endpoint triage status of *Resolved* is set, a third activity for this alert is imported for the user in insider risk. This functionality allows investigators to follow the progression of the Defender for Endpoint alerts and choose the level of visibility that their investigation requires.

> [!IMPORTANT]
> You'll need to have Microsoft Defender for Endpoint configured in your organization and enable Defender for Endpoint for insider risk management integration in the Defender Security Center to import security violation alerts. For more information on configuring Defender for Endpoint for insider risk management integration, see [Configure advanced features in Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/advanced-features\#share-endpoint-alerts-with-microsoft-compliance-center).

### Domains

Domain settings help you define risk levels for risk management activities to specific domains. These activities include sharing files, sending email messages, downloading, or uploading content. By specifying domains in these settings, you can increase or decrease the risk scoring for risk management activity that takes place with these domains.

Use Add domain to define a domain for each of the domain settings. Additionally, you can use wildcards to help match variations of root domains or subdomains. For example, to specify sales.wingtiptoys.com and support.wingtiptoys.com, you use the wildcard entry '*.wingtiptoys.com' to match these subdomains (and any other subdomain at the same level). To specify multi-level subdomains for a root domain, you must select the **Include Multi-Level Subdomains** checkbox.

For each of the following domain settings, you can enter up to 500 domains:

- **Unallowed domains:** By specifying unallowed domains, risk management activity that takes place with these domains will have *higher* risk scores. Some examples are activities involving sharing content with someone (such as sending email to someone with a gmail.com address) and when users download content to a device from one of these unallowed domains.
- **Allowed domains:** Certain risk management activity related to allowed domains will be ignored by your policies and won't generate alerts. These activities include:

    - Email sent to external domains
    - Files, folders, sites shared with external domains
    - Files uploaded to external domains (using Microsoft Edge browser)

    By specifying allowed domains in settings, the risk management  activity with these domains is treated similarly to how internal organizational activity is treated. For example, domains added here map to activities may involve sharing content with someone outside your organization (such as sending email to someone with a gmail.com address).

- **Third party domains:** If your organization uses third-party domains for business purposes (such as cloud storage), include them here so you can receive alerts for potentially risky activity related to the device indicator *Use a browser to download content from a third-party site*.
 
### Sensitive info types exclusion (preview)

[Sensitive info types](sensitive-information-type-learn-about.md) excluded in settings map to indicators and triggers involving file-related activities for Endpoint, SharePoint, Teams, OneDrive, and Exchange. These excluded types will be treated as non-sensitive info types. For those files that contain any sensitive info types identified here, they will be risk scored but not shown as activities involving content related to sensitive info types. For a complete list, see [Sensitive information type entity definitions](sensitive-information-type-entity-definitions.md).

You can select the sensitive info types to be excluded from the list of all available (out-of-box and custom) types available in the tenant. You can choose up to 500 sensitive info types to be excluded.

> [!NOTE]
> The exclusion list of sensitive info types takes precedence over the [priority content](insider-risk-management-policies.md#prioritize-content-in-policies) list.

To exclude sensitive info types, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**. 
2. In the **Sensitive info types** section, select **Add sensitive info types to exclude**.
3. On the **Add or edit sensitive info type** pane, select the types that you want to exclude.
4. Select **Add** accept the changes or **Cancel** to discard the changes. 

To delete a sensitive info type exclusion, select the exclusion and **Delete**.

### Trainable classifier exclusion (preview)

[Trainable classifiers](classifier-get-started-with.md) excluded in settings map to indicators and triggers involving file-related activities for SharePoint, Teams, OneDrive, and Exchange. For those files that contain any trainable classifiers identified here, they will be risk scored but not shown as activities involving content related to trainable classifiers. To learn more, see [Trainable classifiers definitions](classifier-tc-definitions.md#trainable-classifiers-definitions) for a complete list of all pre-trained classifiers.

You can select the trainable classifiers to be excluded from the list of all available (out-of-box and custom) types available in the tenant. Insider risk management excludes some trainable classifiers by default, including Threat, Profanity, Targeted harassment, Offensive language, and Discrimination. You can choose up to 500 trainable classifiers to be excluded.

> [!NOTE]
> Optionally, you can choose trainable classifiers to be included in the [priority content](insider-risk-management-policies.md#prioritize-content-in-policies) list.

To exclude trainable classifiers, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**. 
2. In the **Trainable classifiers** section, select **Add trainable classifiers to exclude**.
3. On the **Add or edit trainable classifiers** pane, select the classifiers that you want to exclude.
4. Select **Add** accept the changes or **Cancel** to discard the changes. 

To delete a trainable classifiers exclusion, select the exclusion and **Delete**.

### File path exclusions

By defining file paths to exclude, user activities that map to specific indicators and that occur in these file path locations won't generate policy alerts. Some examples are copying or moving files to a system folder or network share path. You can enter up to 500 file paths for exclusion.

To add file paths to exclude, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**. 
2. In the **File path exclusion** section, select **Add file paths to exclude**.
3. On the **Add a file path** pane, enter an exact network share or device path to exclude from risk scoring. You can also use * and *([0-9]) to denote specific folders and sub-folders to be excluded.
4. Select **Add file paths** to exclude to configure the file path exclusions or **Close** to discard the changes. 

To delete a file path exclusion, select the file path exclusion and select **Delete**.

### Default file path exclusions

By default, several file paths are automatically excluded from generating policy alerts. Activities in these file paths are typically benign and could potentially increase the volume of non-actionable alerts. If needed, you can cancel the selection for these default file path exclusions to enable risk scoring for activities in these locations.

The default file path exclusions are:

- \Users\\\*\AppData
- \Users\\\*\AppData\Local
- \Users\\\*\AppData\Local\Roaming
- \Users\\\*\AppData\Local\Local\Temp

The wildcards in these paths denote that all folder levels between the \Users and \AppData are included in the exclusion. For example, activities in *C:\Users\Test1\AppData\Local* and *C:\Users\Test2\AppData\Local*, *C:\Users\Test3\AppData\Local* (and so on) would all be included and not scored for risk as part of the *\Users\\\*\AppData\Local* exclusion selection.

### Site exclusions

Configure site URL exclusions to prevent potential risky activities that occur in SharePoint (and SharePoint sites associated with Team channel sites) from generating policy alerts. You might want to consider excluding sites and channels that contain non-sensitive files and data that can be shared with stakeholders or the public. You can enter up to 500 site URL paths to exclude.

To add site URL paths to exclude, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**.
2. In the **Site URL exclusion** section, select **Add or edit SharePoint sites**.
3. On the **Add or edit SharePoint sites** pane, enter or search for the SharePoint site to exclude from risk scoring. You'll only see SharePoint sites that you have permission to access.
4. Select **Add** to configure the site URL exclusions or **Cancel** to discard the changes.

To edit site URL paths to exclude, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**.
2. In the **Site URL exclusion** section, select **Add or edit SharePoint sites**.
3. On the **Add or edit SharePoint sites** pane, enter or search for the SharePoint site to exclude from risk scoring. You'll only see SharePoint sites that you have permission to access.
4. Select **Edit** to configure the site URL exclusions or **Cancel** to discard the changes.

To delete a Site URL exclusion, select the site URL exclusion and select **Delete**.

### Keyword exclusion

Configure exclusions for keywords that appear in file names, file paths, or email message subject lines. This allows flexibility for organizations that need to reduce potential alert frequency due to flagging of benign terms specified for your organization. Such activities related to files or email subjects containing the keyword will be ignored by your insider risk management policies and won't generate alerts. You can enter up to 500 keywords to exclude. 

Use the **Exclude only if it does not contain** field to define specific groupings of terms to ignore for exclusion, For example, if you want to exclude the keyword 'training,' but not exclude 'compliance training,' you would enter 'compliance' (or 'compliance training') in the **Exclude only if it does not contain** field and 'training' in the **But does contain** field.

If you just want to exclude specific standalone terms, enter the terms in the **But does contain field** only.

To add standalone keywords to exclude, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**.
2. In the **Keyword exclusion** section, enter the standalone keywords in the **But does contain** field.
3. Select **Save** to configure the keyword exclusions.

To delete a standalone keyword to exclude, complete the following steps:

1. In the compliance portal, navigate to **Insider risk management** > **Settings** > **Intelligent detections**. 
2. In the **Keyword exclusion** section, select the *X* for the specific standalone keyword in the **But does contain** field. Repeat as needed to remove multiple keywords.
3. Select **Save** to delete the keyword exclusions.

## Export alerts

Insider risk management alert information is exportable to security information and event management (SIEM) and security orchestration automated response (SOAR) solutions by using the [Office 365 Management Activity API schema](/office/office-365-management-api/office-365-management-activity-api-schema#security-and-compliance-alerts-schema). You can use the Office 365 Management Activity APIs to export alert information to other applications your organization may use to manage or aggregate insider risk information. Alert information is exported and available every 60 minutes via the Office 365 Management Activity APIs.

If your organization uses Microsoft Sentinel, you can also use the out-of-the-box insider risk management data connector to import insider risk alert information to Sentinel. For more information, see [Insider Risk Management (IRM) (Preview)](/azure/sentinel/data-connectors-reference#microsoft-365-insider-risk-management-irm-preview) in the Microsoft Sentinel article.

> [!IMPORTANT]
> To maintain referential integrity for users who have insider risk alerts or cases in Microsoft 365 or other systems, anonymization of usernames isn't preserved for exported alerts. Exported alerts will display usernames for each alert.

To use the APIs to review insider risk alert information:

1. Enable Office 365 Management Activity API support in **Insider risk management** > **Settings** > **Export alerts**. By default, this setting is disabled for your Microsoft 365 organization.
2. Filter the common Office 365 audit activities by *SecurityComplianceAlerts*.
3. Filter *SecurityComplianceAlerts* by the *InsiderRiskManagement* category.

![Insider risk management export alert settings.](../media/insider-risk-settings-export.png)

Alert information contains information from the Security and Compliance Alerts schema and the [Office 365 Management Activity API](/office/office-365-management-api/office-365-management-activity-api-schema.md#security-and-compliance-alerts-schema) common schema.

The following fields and values are exported for insider risk management alerts for the Security and Compliance Alerts schema:

| **Alert parameter** | **Description** |
|:------------------|:----------------|
| AlertType | Type of the alert is *Custom*.  |
| AlertId | The GUID of the alert. Insider risk management alerts are mutable. As alert status changes, a new log with the same AlertID is generated. This AlertID can be used to correlate updates for an alert. |
| Category | The category of the alert is *InsiderRiskManagement*. This category can be used to distinguish from these alerts from other security and compliance alerts. |
| Comments | Default comments for the alert. Values are *New Alert* (logged when an alert is created) and *Alert Updated* (logged when there's an update to an alert). Use the AlertID to correlate updates for an alert. |
| Data | The data for the alert, includes the unique user ID, user principal name, and date and time (UTC) when user was triggered into a policy. |
| Name | Policy name for insider risk management policy that generated the alert. |
| PolicyId | The GUID of the insider risk management policy that triggered the alert. |
| Severity | The severity of the alert. Values are *High*, *Medium*, or *Low*. |
| Source | The source of the alert. The value is *Office 365 Security & Compliance*. |
| Status | The status of the alert. Values are *Active* (*Needs Review* in insider risk), *Investigating* (*Confirmed* in insider risk), *Resolved* (*Resolved* in insider risk), *Dismissed* (*Dismissed* in insider risk). |
| Version | The version of the Security and Compliance Alerts schema. |

The following fields and values are exported for insider risk management alerts for the [Office 365 Management Activity API common schema](/office/office-365-management-api/office-365-management-activity-api-schema#common-schema).

- UserId
- Id
- RecordType
- CreationTime
- Operation
- OrganizationId
- UserType
- UserKey

## Priority user groups

Users in your organization may have different levels of risk depending on their position, level of access to sensitive information, or risk history. Prioritizing the examination and scoring of the activities of these users can help alert you to potential risks that may have higher consequences for your organization. Priority user groups in insider risk management help define the users in your organization that need closer inspection and more sensitive risk scoring. Coupled with the *Security policy violations by priority users* and *Data leaks by priority users* policy templates, users added to a priority user group have an increased likelihood of insider risk alerts and alerts with higher severity levels.

![Insider risk management priority user group settings](../media/insider-risk-settings-priority-users.png)

Instead of being open to review by all analysts and investigators, priority users groups may also need to restrict review activities to specific users or insider risk role groups. You can choose to assign individual users and role groups to review users, alerts, cases, and reports for each priority user group. Priority user groups can have review permissions assigned to the built-in *Insider Risk Management*, *Insider Risk Management Analysts*, and *Insider Risk Management Investigators* role groups, one or more of these role groups, or to a custom selection of users.

For example, you need to protect against data leaks for a highly confidential project where users have access to sensitive information. You choose to create *Confidential Project* *Users* priority user group for users in your organization that work on this project. Also, this priority user group shouldn't have users, alerts, cases, and reports associated with group visible to all the default insider risk management admins, analysts, and investigators. In **Settings**, you create the *Confidential Project Users* priority users group and assign two users as reviewer that can view data related to the groups. Use the policy wizard and the *Data leaks by priority users* policy template to create a new policy and assign the *Confidential Project Users* priority users group to the policy. Activities examined by the policy for members of the *Confidential Project Users* priority user group are more sensitive to risk and activities by these users will be more likely to generate an alert and have alerts with higher severity levels.

### Create a priority user group

To create a new priority user group, use the setting controls in the **Insider risk management** solution in the Microsoft Purview compliance portal. To create a priority user group, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group.

Complete the following steps to create a priority user group:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings**.
2. Select the **Priority user groups** page.
3. On the **Priority user groups** page, select **Create priority user group** to start the group creation wizard.
4. On the **Name and describe** page, complete the following fields:
    - **Name (required)**: Enter a friendly name for the priority user group. You can't change the name of the priority user group after you complete the wizard.
    - **Description (optional)**: Enter a description for the priority user group.
5. Select **Next** to continue.
6. On the **Choose members** page, select **Choose members** to search and select which mail-enabled user accounts are included in the group or select the **Select all** checkbox to add all users in your organization to the group. Select **Add** to continue or **Cancel** to close without adding any users to the group.
7. Select **Next** to continue.
8. On the **Choose who can view this group** page, you must define who can review users, alerts, cases, and reports for the priority user group. At least one user or insider risk management role group must be assigned. Select **Choose users and role groups** and select the users or insider risk management role groups you want to assign to the priority user group. Select **Add** to assign the selected users or role groups to the group.
9. Select Next to continue.
10. On the **Review** page, review the settings you've chosen for the priority user group. Select the **Edit** links to change any of the group values or select **Submit** to create and activate the priority user group.
11. On the confirmation page, select **Done** to exit the wizard.

### Update a priority user group

To update an existing priority user group, you'll use setting controls in the **Insider risk management** solution in the Microsoft Purview compliance portal. To update a priority user group, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group.

Complete the following steps to edit a priority user group:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings**.
2. Select the **Priority user groups** page.
3. Select the priority user group you want to edit and select **Edit group**.
4. On the **Name and describe** page, update the Description field if needed. You can't update the name of the priority user group. Select **Next** to continue.
5. On the **Choose members** page, add new members to the group using the **Choose members** control. To remove a user from the group, select the 'X' next to the user you wish to remove. Select **Next** to continue.
6. On the **Choose who can view this group** page, add or remove users or role groups that can review users, alerts, cases, and reports for the priority user group.
7. Select **Next** to continue.
8. On the **Review** page, review the update settings you've chosen for the priority user group. Select the **Edit** links to change any of the group values or select **Submit** to update the priority user group.
9. On the confirmation page, select **Done** to exit the wizard.

### Delete a priority user group

To delete an existing priority user group, use setting controls in the **Insider risk management** solution in the Microsoft Purview compliance portal. To delete a priority user group, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group.

> [!IMPORTANT]
> Deleting a priority user group will remove it from any active policy to which it is assigned. If you delete a priority user group that is assigned to an active policy, the policy will not contain any in-scope users and will effectively be idle and will not create alerts.

Complete the following steps to delete a priority user group:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings**.
2. Select the **Priority user groups** page.
3. Select the priority user group you want to edit and select **Delete** from the dashboard menu.
4. On the **Delete** dialog, select **Yes** to delete the priority user group or select **Cancel** to return to the dashboard.

## Priority physical assets (preview)

Identifying access to priority physical assets and correlating access activity to user events is an important component of your compliance infrastructure. These physical assets represent priority locations in your organization, such as company buildings, data centers, or server rooms. Insider risk activities may be associated with users working unusual hours, attempting to access these unauthorized sensitive or secure areas, and requests for access to high-level areas without legitimate needs.

With priority physical assets enabled and the [Physical badging data connector](import-physical-badging-data.md) configured, insider risk management integrates signals from your physical control and access systems with other user risk activities. By examining patterns of behavior across physical access systems and correlating these activities with other insider risk events, insider risk management can help compliance investigators and analysts make more informed response decisions for alerts. Access to priority physical assets is scored and identified in insights differently from access to non-priority assets.

For example, your organization has a badging system for users that governs and approves physical access to normal working and sensitive project areas. You have several users working on a sensitive project and these users will return to other areas of your organization when the project is completed. As the sensitive project nears completion, you want to make sure that the project work remains confidential and that access to the project areas is tightly controlled.

You choose to enable the Physical badging data connector in Microsoft 365 to import access information from your physical badging system and specify priority physical assets in insider risk management. By importing information from your badging system and correlating physical access information with other risk activities identified in insider risk management, you notice that one of the users on the project is accessing the project offices after normal working hours and is also exporting large amounts of data to a personal cloud storage service from their normal work area. This physical access activity associated with the online activity may point to possible data theft and compliance investigators and analysts can take appropriate actions as dictated by the circumstances for this user.

![Insider risk management priority physical assets.](../media/insider-risk-settings-priority-assets.png)

### Configure priority physical assets

To configure priority physical assets, you'll configure the Physical badging connector and use setting controls in the **Insider risk management** solution in the Microsoft Purview compliance portal. To configure priority physical assets, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin role group*.

Complete the following steps to configure priority physical assets:

1. Follow the configuration steps for insider risk management in the [Getting started with insider risk management](insider-risk-management-configure.md) article. In Step 3, make sure you configure the Physical badging connector.

    > [!IMPORTANT]
    > For insider risk management policies to use and correlate signal data related to departing and terminated users with event data from your physical control and access platforms, you must also configure the Microsoft 365 HR connector. If you enable the Physical badging connector without enabling the Microsoft 365 HR connector, insider risk management policies will only process events for physical access activities for users in your organization.

2. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Priority physical assets**.
3. On the **Priority physical assets** page, you can either manually add the physical asset IDs you want to detect asset events imported by the Physical badging connector or import a .csv file of all physical assets IDs imported by the Physical badging connector:
    a) To manually add physical assets IDs, choose **Add priority physical assets**, enter a physical asset ID, then select **Add**. Enter other physical asset IDs and then select **Add priority physical assets** to save all the assets entered.
    b) To add a list of physical asset IDs from a .csv file, choose **Import priority physical assets**. From the file explorer dialog, select the CSV file you wish to import, then select **Open**. The physical asset IDs from the CSV files are added to the list.
4. Navigate to the **Policy indicators** page in **Settings**.
5. On the **Policy indicators** page, navigate to the **Physical access indicators** section and select the checkbox for **Physical access after termination or failed access to sensitive asset**.
6. Select **Save** to configure and exit.

### Delete a priority physical asset

To delete an existing priority physical asset, you'll use setting controls in the Insider risk management solution in the Microsoft Purview compliance portal. To delete a priority physical asset, you must be a member of the Insider Risk Management or Insider Risk Management Admin role group.

> [!IMPORTANT]
> Deleting a priority physical asset removes it from examination by any active policy to which it was previously included. Alerts generated by activities associated with the priority physical asset aren't deleted.

Complete the following steps to delete a priority physical asset:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Priority physical assets**.
2. On the **Priority physical assets** page, select the asset you want to delete.
3. Select **Delete** on the action menu to delete the asset.

## Power Automate flows (preview)

[Microsoft Power Automate](/power-automate/getting-started) is a workflow service that automates actions across applications and services. By using flows from templates or created manually, you can automate common tasks associated with these applications and services. When you enable Power Automate flows for insider risk management, you can automate important tasks for cases and users. You can configure Power Automate flows to retrieve user, alert, and case information and share this information with stakeholders and other applications, as well as automate actions in insider risk management, such as posting to case notes. Power Automate flows are applicable for cases and any user in scope for a policy.

Customers with Microsoft 365 subscriptions that include insider risk management don't need additional Power Automate licenses to use the recommended insider risk management Power Automate templates. These templates can be customized to support your organization and cover core insider risk management scenarios. If you choose to use premium Power Automate features in these templates, create a custom template using the Microsoft Purview connector, or use Power Automate templates for other compliance areas in Microsoft 365, you may need more Power Automate licenses.

The following Power Automate templates are provided to customers to support process automation for insider risk management users and cases:

- **Notify users when they're added to an insider risk policy**: This template is for organizations that have internal policies, privacy, or regulatory requirements that users must be notified when they're subject to insider risk management policies. When this flow is configured and selected for a user in the **Users** page, users and their managers are sent an email message when the user is added to an insider risk management policy. This template also supports updating a SharePoint list hosted on a SharePoint site to help track notification message details like date/time and the message recipient. If you've chosen to anonymize users in **Privacy settings**, flows created from this template won't function as intended so that user privacy is maintained. Power Automate flows using this template are available on the **Users dashboard**.
- **Request information from HR or business about a user in an insider risk case**: When acting on a case, insider risk analysts and investigators may need to consult with HR or other stakeholders to understand the context of the case activities. When this flow is configured and selected for a case, analysts and investigators send an email message to HR and business stakeholders configured for this flow. Each recipient is sent a message with pre-configured or customizable response options. When recipients select a response option, the response is recorded as a case note and includes recipient and date/time information. If you've chosen to anonymize users in **Privacy settings**, flows created from this template won't function as intended so that user privacy is maintained. Power Automate flows using this template are available on the **Cases dashboard**.
- **Notify manager when a user has an insider risk alert**: Some organizations may need to have immediate management notification when a user has an insider risk management alert. When this flow is configured and selected, the manager for the case user is sent an email message with the following information about all case alerts:
    - Applicable policy for the alert
    - Date/Time of the alert
    - Severity level of the alert

    The flow automatically updates the case notes that the message was sent and that the flow was activated. If you've chosen to anonymize users in **Privacy settings**, flows created from this template won't function as intended so that user privacy is maintained. Power Automate flows using this template are available on the **Cases dashboard**.
- **Create record for insider risk case in ServiceNow**: This template is for organizations that want to use their ServiceNow solution to track insider risk management cases.  When in a case, insider risk analysts and investigators can create a record for the case in ServiceNow. You can customize this template to populate selected fields in ServiceNow based on your organization's requirements. Power Automate flows using this template are available on the **Cases dashboard**. For more information on available ServiceNow fields, see the [ServiceNow Connector reference](/connectors/service-now/) article.

### Create a Power Automate flow from insider risk management template

To create a Power Automate flow from a recommended  insider risk management template, you'll use the settings controls in the **Insider risk management** solution in the Microsoft Purview compliance portal or the **Manage Power Automate flows** option from the **Automate** control when working directly in the **Cases** or **Users dashboards**.

To create a Power Automate flow in the settings area, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group. To create a Power Automate flow with the **Manage Power Automate flows** option, you must be a member of at least one insider risk management role group.

Complete the following steps to create a Power Automate flow from a recommended insider risk management template:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Power Automate flows**. You can also access from the **Cases** or **Users dashboards** pages by choosing **Automate** > **Manage Power Automate flows**.
2. On the **Power Automate flows** page, select a recommended template from the **Insider risk management templates you may like** section on the page.
3. The flow lists the embedded connections needed for the flow and will note if the connection statuses are available. If needed, update any connections that aren't displayed as available. Select **Continue**.
4. By default, the recommended flows are pre-configured with the recommended insider risk management and Microsoft 365 service data fields required to complete the assigned task for the flow. If needed, customize the flow components by using the **Show advanced options** control and configuring the available properties for the flow component.
5. If needed, add any other steps to the flow by selecting the **New step** button. In most cases, this shouldn't be needed for the recommended default templates.
6. Select **Save draft** to save the flow for further configuration or select **Save** to complete the configuration for the flow.
7. Select **Close** to return to the **Power Automate flow** page. The new template will be listed as a flow on the **My flows** tabs and is automatically available from the **Automate** dropdown control when working with insider risk management cases for the user creating the flow.

> [!IMPORTANT]
> If other users in your organization need access to the flow, the flow must be shared.

### Create a custom Power Automate flow for insider risk management

Some processes and workflows for your organization may be outside of the recommended insider risk management flow templates and you may have the need to create custom Power Automate flows for insider risk management areas. Power Automate flows are flexible and support extensive customization, but there are steps that need to be taken to integrate with insider risk management features.

Complete the following steps to create a custom Power Automate template for insider risk management:

1. **Check your Power Automate flow license**: To create customized Power Automate flows that use insider risk management triggers, you'll need a Power Automate license. The recommended insider risk management flow templates don't require extra licensing and are included as part of your insider risk management license.
2. **Create an automated flow**: Create a flow that performs one or more tasks after it's triggered by an insider risk management event. For details on how to create an automated flow, see [Create a flow in Power Automate](/power-automate/get-started-logic-flow).
3. **Select the Microsoft Purview connector**: Search for and select the Microsoft Purview connector. This connector enables insider risk management triggers and actions. For more information on connectors, see the [Connector reference overview](/connectors/connector-reference/) article.
4. **Choose insider risk management triggers for your flow**: Insider risk management has two triggers available for custom Power Automate flows:
    - **For a selected insider risk management case**: Flows with this trigger can be selected from the insider risk management Cases dashboard page.
    - **For a selected insider risk management user**: Flows with this trigger can be selected from the insider risk management Users dashboard page.
5. Choose insider risk management actions for your flow: You can choose from several actions for insider risk management to include in your custom flow:
    - Get insider risk management alert
    - Get insider risk management case
    - Get insider risk management user
    - Get insider risk management alerts for a case
    - Add insider risk management case note

### Share a Power Automate flow

By default, Power Automate flows created by a user are only available to that user. For other insider risk management users to have access and use a flow, the flow must be shared by the flow creator. To share a flow, you'll use the settings controls in the **Insider risk management solution** in the Microsoft Purview compliance portal or the **Manage Power Automate flows** option from the Automate control when working directly in the **Cases** or **Users dashboard** pages. Once you've shared a flow, everyone who it has been shared with can access the flow in the **Automate** control dropdown in the **Case** and **User dashboards**.

To share a Power Automate flow in the settings area, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group. To share a Power Automate flow with the **Manage Power Automate flows** option, you must be a member of at least one insider risk management role group.

Complete the following steps to share a Power Automate flow:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Power Automate flows**. You can also access from the **Cases** or **Users dashboards** pages by choosing **Automate** > **Manage Power Automate flows**.
2. On the **Power Automate flows** page, select the **My flows** or **Team flows** tab.
3. Select the flow to share, then select **Share** from the flow options menu.
4. On the flow sharing page, enter the name of the user or group you want to add as an owner for the flow.
5. On the **Connection Used** dialog, select **OK** to acknowledge that the added user or group will have full access to the flow.

### Edit a Power Automate flow

To edit a flow, you'll use the settings controls in the **Insider risk management** solution in the Microsoft Purview compliance portal or the **Manage Power Automate flows** option from the **Automate** control when working directly in the **Cases** or **Users dashboards**.

To edit a Power Automate flow in the settings area, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group. To edit a Power Automate flow with the **Manage Power Automate flows** option, you must be a member of at least one insider risk management role group.

Complete the following steps to edit a Power Automate flow:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Power Automate flows**. You can also access from the **Cases** or **Users dashboards** pages by choosing **Automate** > **Manage Power Automate flows**.
2. On the **Power Automate flows** page, select a flow to edit and select **Edit** from the flow control menu.
3. Select the **ellipsis** > **Settings** to change a flow component setting or **ellipsis** > **Delete** to delete a flow component.
4. Select **Save** and then **Close** to complete editing the flow.

### Delete a Power Automate flow

To delete a flow, you'll use the settings controls in the **Insider risk management** solution in the Microsoft Purview compliance portal or the **Manage Power Automate flows** option from the **Automate** control when working directly in the **Cases** or **Users dashboards**. When a flow is deleted, it's removed as an option for all users.

To delete a Power Automate flow in the settings area, you must be a member of the *Insider Risk Management* or *Insider Risk Management Admin* role group. To delete a Power Automate flow with the **Manage Power Automate flows** option, you must be a member of at least one insider risk management role group.

Complete the following steps to delete a Power Automate flow:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** and select **Insider risk settings** > **Power Automate flows**. You can also access from the **Cases** or **Users dashboards** pages by choosing **Automate** > **Manage Power Automate flows**.
2. On the **Power Automate flows** page, select a flow to delete and select **Delete** from the flow control menu.
3. On the deletion confirmation dialog, select **Delete** to remove the flow or select **Cancel** to exit the deletion action.

## Microsoft Teams (preview)

Compliance analysts and investigators can easily use Microsoft Teams for collaboration on insider risk management cases. They can coordinate and communicate with other stakeholders in Microsoft Teams to:

- Coordinate and review response activities for cases in private Teams channels
- Securely share and store files and evidence related to individual cases
- Track and review response activities by analysts and investigators

After Microsoft Teams is enabled for insider risk management, a dedicated Microsoft Teams team is created every time an alert is confirmed and a case is created. By default, the team automatically includes all members of the *Insider Risk Management*, *Insider Risk Management Analysts*, and *Insider Risk Management Investigators* role groups (up to 100 initial users). Additional organization contributors may be added to the team after it's created and as appropriate. For existing cases created before enabling Microsoft Teams, analysts and investigators can choose to create a new Microsoft Teams team when working in a case if needed.  Once you resolve the associated case in insider risk management, the team is automatically archived (moved to hidden and read-only).

For more information on how to use teams and channels in Microsoft Teams, see [Overview of teams and channels in Microsoft Teams](/MicrosoftTeams/teams-channels-overview).

Enabling Microsoft Teams support for cases is quick and easy to configure. To enable Microsoft Teams for insider risk management, complete the following steps:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** > **Insider risk settings**.
2. Select the **Microsoft Teams** page.
3. Enable Microsoft Teams integration for insider risk management.
4. Select **Save** to configure and exit.

![Insider risk management Microsoft Teams.](../media/insider-risk-settings-teams.png)

### Create a Microsoft Teams team for existing cases

If you enable Microsoft Teams support for insider risk management after you have existing cases, you'll need to manually create a team for each case as needed. After enabling Microsoft Teams support in insider risk management settings, new cases will automatically create a new Microsoft Teams team.

Users need permission to create Microsoft 365 groups in your organization to create a Microsoft Teams team from a case. For more information about managing permissions for Microsoft 365 Groups, see [Manage who can create Microsoft 365 Groups](../solutions/manage-creation-of-groups.md).

To create a team for a case, you'll use the Create Microsoft Team control when working directly in an existing case. Complete the following steps to create a new team:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** > **Cases** and select an existing case.
2. On the case action menu, select **Create Microsoft Team**.
3. In the **Team name** field, enter a name for the new Microsoft Teams team.
4. Select **Create Microsoft team** and then select **Close**.

Depending on the number of users assigned to insider risk management role groups, it may take 15 minutes for all investigators and analysts to be added to the Microsoft Teams team for a case.

## Analytics

Insider risk analytics enables you to conduct an evaluation of potential insider risks in your organization without configuring any insider risk policies. This evaluation can help your organization identify potential areas of higher user risk and help determine the type and scope of insider risk management policies you may consider configuring. Analytics scans offer the following advantages for your organization:

- Easy to configure: To get started with analytics scans, you can select Run scan when prompted by the analytics recommendation or go to **Insider risk settings** > **Analytics** and enable analytics.
- Privacy by design: Scan results and insights are returned as aggregated and anonymized user activity, individual user names aren't identifiable by reviewers.
- Understand potential risks through consolidated insights: Scan results can help you quickly identify potential risk areas for your users and which policy would be best to help mitigate these risks.

Check out the [Insider Risk Management Analytics video](https://www.youtube.com/watch?v=5c0P5MCXNXk) to help understand how analytics can help accelerate the identification of potential insider risks and help you to quickly take action.

Analytics scans for risk management activity from several sources to help identify insights into potential areas of risk. Depending on your current configuration, analytics looks for qualifying risk activities in the following areas:

- **Microsoft 365 audit logs**: Included in all scans, this is the primary source for identifying most of the potentially risky activities.
- **Exchange Online**: Included in all scans, Exchange Online activity helps identify activities where data in attachments are emailed to external contacts or services.
- **Azure Active Directory**: Included in all scans, Azure Active Directory history helps identify risky activities associated with users with deleted user accounts.
- **Microsoft 365 HR data connector**: If configured, HR connector events help identify risky activities associated with users that have resignation or upcoming termination dates.

Analytics insights from scans are based on the same risk management activity signals used by insider risk management policies and report results based on both single and sequence user activities. However, the risk scoring for analytics is based on up to 10 days of activity while insider risk policies use daily activity for insights. When you first enable and run analytics in your organization, you'll see the scan results for one day. If you leave analytics enabled, you'll see the results of each daily scan added to the insight reports for a maximum range of the previous 10 days of activity.

### Enable analytics and start your scan

To enable insider risk analytics, you must be a member of the *Insider Risk Management*, *Insider Risk Management Admin*, or *Microsoft 365 Global admin* role group.
Complete the following steps to enable insider risk analytics:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management**.
2. Select **Run scan** on the **Scan for insider risks in your organization** card on the insider risk management **Overview** tab. This turns on analytics scanning for your organization. You can also turn on scanning in your organization by navigating to **Insider risk settings** > **Analytics** and enabling **Scan your tenant's user activity to identify potential insider risks**.
3. On the **Analytics details** pane, select **Run scan** to start the scan for your organization. Analytics scan results may take up to 48 hours before insights are available as reports for review.

![Insider risk management analytics settings](../media/insider-risk-settings-analytics-enable.png)

### Viewing analytics insights and creating new policies

After the first analytics scan is complete for your organization, members of the *Insider Risk Management Admin* role group will automatically receive an email notification and can view the initial insights and recommendations for potentially risky activities by your users. Daily scans continue unless you turn off analytics for your organization. Email notifications to admins are provided for each of the three in-scope categories for analytics (data leaks, theft, and exfiltration) after the first instance of potentially risky activity in your organization. Email notifications aren't sent to admins for follow-up risk management activity detection resulting from the daily scans. If analytics in **Insider risk management** > **Settings** > **Analytics** are disabled and then re-enabled in your organization, automatic email notifications are reset and emails are sent to members of the *Insider Risk Management Admin* role group for new scanning insights.

To view potential risks for your organization, go to the **Overview** tab and select **View results** on the **Insider risk analytics** card. If the scan for your organization isn't complete, you'll see a message that the scan is still active.

![Insider risk management analytics report ready card](../media/insider-risk-analytics-ready-card.png)

For completed analyses, you'll see the potential risks discovered in your organization and insights and recommendations to address these risks. Identified risks and specific insights are included in reports grouped by area, the total number of users with identified risks, the percentage of these users with potentially risky activities, and a recommended insider risk policy to help mitigate these risks. The reports include:

- **Data leaks insights**: For all users that may include accidental oversharing of information outside your organization or data leaks by users with malicious intent.
- **Data theft insights**: For departing users or users with deleted Azure Active Directory accounts that may include risky sharing of information outside your organization or data theft by users with malicious intent.
- **Top exfiltration insights**: For all users that may include sharing data outside of your organization.

![Insider risk management analytics overview report.](../media/insider-risk-analytics-overview.png)

To display more information for an insight, select **View details** to display the details pane for the insight. The details pane includes the complete insight results, an insider risk policy recommendation, and the **Create policy** button to quickly help you create the recommended policy. Selecting Create policy takes you to the policy wizard and automatically selects the recommended policy template related to the insight. For example, if the analytics insight is for *Data leak* activity, the *Data leaks* policy template will be pre-selected in the policy wizard for you.

![Insider risk management analytics details report.](../media/insider-risk-analytics-details.png)

### Turn off analytics

To turn off insider risk analytics, you must be a member of the *Insider Risk Management*, *Insider Risk Management Admin*, or Microsoft 365 *Global admin* role group. After you disable analytics, analytics insight reports will remain static and not be updated for new risks.

Complete the following steps to turn off insider risk analytics:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management**.
2. Select **Insider risk settings** > **Analytics** page.
3. On the **Analytics** page, turn off **Scan your tenant's user activity to identify potential insider risks**.

## Admin notifications

Admin notifications automatically send an email notification to selectable insider risk management role groups. You can enable notifications and assign which role groups will receive the notifications for the following scenarios:

- Send a notification email when the first alert is generated for a new policy. Policies are checked every 24 hours for first-time alerts and notifications aren't sent on subsequent alerts for the policy.
- Send a daily email when new high severity alerts are generated. Policies are checked every 24 hours for high severity alerts.
- Send a weekly email summarizing policies that have unresolved warnings

If you've enabled insider risk management analytics for your organization, members of the *Insider Risk Management Admin* role group automatically receive an email notification for initial analytics insights for data leaks, theft, and exfiltration activities.

If you prefer to disable admin and analytics notifications, complete the following steps:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** > **Insider risk settings**.
2. Select the **Admin notifications** page.
3. Clear the check box for the following options as applicable:
    - **Send a notification email when the first alert is generated for a new policy**
    - **Send an email notification when a new insight is available in Analytics**
    - **Send an email notification when Analytics is turned off**

4. Select **Save** to configure and exit.

## Inline alert customization (preview)

Inline alert customization allows you to quickly tune an insider risk management policy directly from the **Alert dashboard** while reviewing the alert. Alerts are generated when a risk management activity meets the thresholds configured in the related policy. To reduce the number of alerts you get from this type of activity, you can change the thresholds or remove the risk management activity from the policy altogether.

You can enable inline alert customization to allow users assigned to the *Insider Risk Management Analysts* and *Insider Risk Management Investigators* role groups to edit policy thresholds and to disable specific indicators. If inline alert customization isn't enabled, only users assigned to the *Insider Risk Management Admin* or *Insider Risk Management* role groups can edit these policy conditions. Inline alert customization is supported for alerts regardless of the current alert status, allowing analysts and investigators to update policies for *Dismissed* and *Resolved* alerts if needed.

Complete the following steps to enable inline alert customization:

1. In the [Microsoft Purview compliance portal](https://compliance.microsoft.com), go to **Insider risk management** > **Insider risk settings**.
2. Select the **Inline alert customization (preview)** page.
3. Enable inline alert customization for insider risk management.
4. Select **Save** to configure and exit.

> [!NOTE]
> Enabling inline alert customization will take approximately one hour before being available in new and existing policy alerts.

When enabled, analysts and investigators can select **Reduce alerts for this activity** for an alert on the **Alert dashboard** and can view details about the risk management activity and indicators associated with the alert. Additionally, the current policy thresholds are displayed for the number of events used to create low, medium, and high severity alerts. If **Reduce alerts for this activity** is selected and a previous policy edit has been made that changes the threshold or has removed the associated indicator, you'll see a notification message detailing previous changes to the policy.

Analysts and investigators can choose from the following options on the **Reduce alerts for this activity** pane to quickly edit the policy that created the alert:

- **Reduce alerts using Microsoft's recommended thresholds**: We'll automatically increase the thresholds in the policy for you. You'll be able to review the new recommended threshold settings before changing the policy.
- **Reduce alerts by choosing your own thresholds**: You can manually increase the thresholds for this type of activity for the current and future alerts. You'll be able to review the current threshold settings and configure the new threshold settings before changing the policy.
- **Stop getting alerts for this activity**: This removes this indicator from the policy and this risk management activity will no longer be detected by the policy. This applies to all indicators, regardless of if the indicator is threshold-based.

After choosing an option, analysts and investigators can choose two options to update the policy:

- **Save and dismiss alert**: Saves the changes to the policy and updates the alert status to *Resolved*.
- **Save only**: Saves the changes to the policy, but the alert status remains the same.
