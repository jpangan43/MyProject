# Configure Microsoft Intune

Comprehensive step-by-step guide derived from the screenshot collection for configuring Microsoft Intune (Endpoint Manager) for Windows and mobile device management.

## Table of Contents

1. [Create Microsoft Intune Group & Automatic Enrollment](#1-create-microsoft-intune-group--automatic-enrollment)
2. [Create Baseline Compliance Policy](#2-create-baseline-compliance-policy)
3. [Device Compliance Message Notification](#3-device-compliance-message-notification)
4. [Basic Device and Apps Configuration](#4-basic-device-and-apps-configuration)
   - Windows Update Rings
   - Deploy Microsoft 365 Apps
   - Edge Homepage / OneDrive configuration
5. [Endpoint Security Policies](#5-endpoint-security-policies)
   - Antivirus
   - Disk Encryption (BitLocker)
   - Firewall
   - Attack Surface Reduction (ASR)
6. [App Protection Policy (MAM)](#6-app-protection-policy-mam)
7. [Conditional Access – Enforce Windows MAM / Edge for BYOD](#7-conditional-access--enforce-windows-mam--edge-for-byod)
8. [Reference Screenshots](#8-reference-screenshots)

---

## 1. Create Microsoft Intune Group & Automatic Enrollment

### Steps

1. Create a new Microsoft Entra ID security group that will be used for Intune assignments (e.g., `All-Company-Windows` or `Pilot-Intune-Users`).

   ![Create Intune Group](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Microsoft%20Intune%20Group/1%20-%20Create%20Intune%20Group.png)

2. Enter the group name, description, and membership type.

   ![Enter group details](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Microsoft%20Intune%20Group/2%20-%20Enter%20the%20group%20details.png)

3. Enable **Automatic Enrollment** (MDM user scope).

   ![Turn on Automatic Enrollment](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Microsoft%20Intune%20Group/3%20-%20Turn%20on%20Automatic%20Enrollment.png)

4. Set the MDM user scope to **All** (or selected groups) so devices are automatically enrolled when users sign in with their work account.

   ![Select All – MDM user scope](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Microsoft%20Intune%20Group/4%20-%20Select%20All%20-%20MDM%20user%20scope.png)

---

## 2. Create Baseline Compliance Policy

Compliance policies define the rules devices must meet to be considered compliant (and therefore granted access via Conditional Access).

### Steps

1. Create a new compliance policy for Windows 10/11.

   ![Create Compliance Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/1%20-%20Create%20Compliance%20Policy.png)

2. Name the policy (e.g., `Windows 11 Baseline Compliance`).

   ![Name the policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/2%20-%20Name%20the%20policy.png)

3. Configure **Device Health** settings (BitLocker, Secure Boot, etc.).

   ![Device Health](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/3%20-%20Set%20the%20compliance%20settings%20%28Device%20Health%29.png)

4. Configure **System Security** settings (password requirements, encryption, firewall, etc.).

   ![System Security](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/4%20-%20Set%20the%20compliance%20settings%20%28System%20Security%29.png)

5. Require antivirus / Microsoft Defender Antivirus to be enabled and up to date.

   ![Antivirus and Defender](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/5%20-%20Set%20the%20Antivirus%20and%20Defender.png)

6. Define **Actions for noncompliance** (mark device noncompliant, send email, remote lock, retire, etc.).

   ![Actions for noncompliance](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/6%20-%20Set%20the%20Actions%20for%20noncompliance.png)

7. Assign the policy to the pilot / target group (e.g., `Pilot-Intune-Users`).

   ![Add the Pilot-Intune-Users group](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/7%20-%20Add%20the%20Pilot-Intune-Users%20group.png)

8. Review and create the policy.

   ![Proceed on creating](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/8%20-%20Proceed%20on%20creating%20the%20compliance%20policy.png)

9. Confirmation that the Windows Compliance Policy has been created.

   ![Windows Compliance Policy Created](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Baseline%20Compliance%20Policy/9%20-%20Windows%20Compliance%20Policy%20Created.png)

---

## 3. Device Compliance Message Notification

Create a notification message template that is sent when a device becomes non-compliant.

### Steps

1. Create a new Notification Message Template.

   ![Create Notification Message Template](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/1%20-%20Create%20Notification%20Message%20Template.png)

2. Name the notification alert.

   ![Name the notification alert](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/2%20-%20Name%20the%20notification%20alert.png)

3. Verify the details.

   ![Verify the details](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/3%20-%20Verify%20the%20details.png)

4. Create the subject and message body that users will receive.

   ![Create the subject and message](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/4%20-%20Create%20the%20subject%20and%20message.png)

5. Link the notification to the non-compliance action.

   ![Create the noncompliance notification](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/5%20-%20Create%20the%20noncompliance%20notification.png)

6. Confirmation that the Non-compliant Device Alert has been created.

   ![Non-compliant Device Alert Created](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Device%20Compliance%20Message%20Notification/6%20-%20Non-compliant%20Device%20Alert%20Created.png)

---

## 4. Basic Device and Apps Configuration

### 4.1 Create Windows Update Rings

1. Create a profile for Windows update rings.

   ![Create profile](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/1%20-%20Create%20profile%20for%20Windows%20update%20rings.png)

2. Name the update ring (e.g., `Windows 11 – Broad / Pilot`).

   ![Name the update rings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/2%20-%20Name%20the%20update%20rings.png)

3. Configure update ring settings (quality/feature update deferral, automatic update behavior, active hours, etc.).

   ![Update ring settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/3%20-%20Update%20ring%20settings.png)

4. Add assignment to the target group.

   ![Add assignment](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/4%20-%20Add%20assignment.png)

5. Review and create.

   ![Review and create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/5%20-%20Review%20and%20create.png)

6. Confirmation – Windows 11 Update Ring created.

   ![Windows 11 Update Ring Created](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Create%20Windows%20Update%20Rings/6%20-%20Windows%2011%20Update%20Ring%20Created.png)

### 4.2 Deploy Microsoft 365 Apps

1. Create a Microsoft 365 Apps deployment.

   ![Create Microsoft 365 Apps](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/1%20-%20Create%20Microsoft%20365%20Apps.png)

2. Enter app suite information (architecture, update channel, etc.).

   ![Enter app suite information](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/2%20-%20Enter%20ap%20suite%20information.png)

3. Configure the app suite (which apps to include/exclude).

   ![Configure app suite](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/3%20-%20Configure%20app%20suite.png)

4. Add group assignment.

   ![Add group assignment](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/4%20-%20Add%20group%20assignment.png)

5. Review and create.

   ![Review and create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/5%20-%20Review%20and%20create.png)

6. Confirmation – Microsoft 365 Apps deployment completed.

   ![Microsoft 365 Apps Completed](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Deploy%20Microsoft%20365%20Apps/6%20-%20Microsoft%20365%20Apps%20Completed.png)

### 4.3 Edge Homepage & OneDrive Configuration Profile

1. Create a configuration profile for Edge Homepage / Windows settings.

   ![Creating configuration profile](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/1%20-%20Creating%20configuration%20profile%20for%20Edge%20Homepage.png)

2. Name the configuration profile.

   ![Name the configuration profile](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/2%20-%20Name%20the%20configuration%20profile.png)

3. Add OneDrive and Microsoft Edge settings in the Configuration Settings catalog.

   ![Add OneDrive and Edge](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/3%20-%20Add%20OneDrive%20and%20Edge%20in%20the%20Configuration%20Settings.png)

4. Verify Microsoft Edge settings (homepage, startup pages, etc.).

   ![Verify Microsoft Edge settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/4%20-%20Verify%20Microsoft%20Edge%20settings.png)

5. Verify OneDrive settings (Known Folder Move, silent account configuration, etc.).

   ![Verify OneDrive settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/5%20-%20Verify%20OneDrive%20settings.png)

6. Add group assignment.

   ![Add group assignment](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/6%20-%20Add%20group%20assignment.png)

7. Review and create.

   ![Review and Create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/7%20-%20Review%20and%20Create.png)

8. Confirmation – Windows 11 configuration completed.

   ![Windows 11 configuration completed](../extracted/intune_temp/Configure%20Microsoft%20Intune/Basic%20Device%20and%20Apps%20Configuration/Edge%20Homepage/8%20-%20Windows%2011%20configuration%20completed.png)

---

## 5. Endpoint Security Policies

### 5.1 Configure Antivirus Policy

1. Create a policy profile for Antivirus (Microsoft Defender Antivirus).

   ![Create policy profile for Antivirus](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Antivirus%20Policy/1%20-%20Create%20policy%20profile%20for%20Antivirus.png)

2. Name the policy.

   ![Name the policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Antivirus%20Policy/2%20-%20Name%20the%20policy.png)

3. Set configuration settings (real-time protection, cloud-delivered protection, scan schedules, etc.).

   ![Set configuration settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Antivirus%20Policy/3%20-%20Set%20configuration%20settings.png)

4. Choose group assignment.

   ![Choose group assignment](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Antivirus%20Policy/4%20-%20Choose%20group%20assignment.png)

5. Review and create.

   ![Review and create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Antivirus%20Policy/5%20-%20Review%20and%20create.png)

### 5.2 Configure Disk Encryption Policy (BitLocker)

1. Create a Disk Encryption policy.

   ![Create Disk Encryption Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Disk%20Encryption%20Policy/1%20-%20Create%20Disk%20Encryption%20Policy.png)

2. Name the policy.

   ![Name the policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Disk%20Encryption%20Policy/2%20-%20Name%20the%20policy.png)

3. Set configuration settings (encryption method, require encryption, recovery key options, etc.).

   ![Set configuration settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Disk%20Encryption%20Policy/3%20-%20Set%20configuration%20settings.png)

4. Assign to the appropriate Windows group.

   ![Assign group user](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Disk%20Encryption%20Policy/4%20-%20Assign%20group%20user.png)

5. Review and create.

   ![Review and create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Disk%20Encryption%20Policy/5%20-%20Review%20and%20create.png)

### 5.3 Configure Firewall Policy

1. Create a Firewall policy.

   ![Create Firewall Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Firewall%20Policy/1%20-%20Create%20Firewall%20Policy.png)

2. Name the Firewall Policy.

   ![Name the Firewall Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Firewall%20Policy/2%20-%20Name%20the%20Firewall%20Policy.png)

3. Enable the three profiles (Domain, Private, Public) to the desired default (typically Enabled / True).

   ![Enable the 3 profiles](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Firewall%20Policy/3%20-%20Enable%20the%203%20profile%20to%20True%20default.png)

4. Assign to `All-Company-Windows` (or equivalent group).

   ![Assign to All-Company-Windows](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Firewall%20Policy/4%20-%20Assign%20to%20All-Company-Windows.png)

5. Review and Create.

   ![Review and Create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Firewall%20Policy/5%20-%20Review%20and%20Create.png)

### 5.4 Configure Attack Surface Reduction (ASR) Policy

1. Create an ASR policy.

   ![Create ASR Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Attack%20Surface%20Reduction%20Policy/1%20-%20Create%20ASR%20Policy.png)

2. Name the ASR Policy.

   ![Name the ASR Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Attack%20Surface%20Reduction%20Policy/2%20-%20Name%20the%20ASR%20Policy.png)

3. Set configuration settings (block executable content from email, block Office child processes, etc.).

   ![Set configuration settings](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Attack%20Surface%20Reduction%20Policy/3%20-%20Set%20configuration%20settings.png)

4. Assign to the Windows group.

   ![Assign to Windows group](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Attack%20Surface%20Reduction%20Policy/4%20-%20Assign%20to%20Windows%20group.png)

5. Review and Create.

   ![Review and Create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20Attack%20Surface%20Reduction%20Policy/5%20-%20Review%20and%20Create.png)

**Endpoint Security overview**

![Endpoint Security Policies](../extracted/intune_temp/Configure%20Microsoft%20Intune/Endpoint%20Security%20Policies.png)

---

## 6. App Protection Policy (MAM)

App protection policies protect corporate data inside managed apps on both enrolled and unenrolled (BYOD) devices.

### Steps (iOS/iPadOS example)

1. Create a MAM policy for iOS/iPadOS.

   ![Create MAM Policy for iOS-iPadOS](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/1%20-%20Create%20MAM%20Policy%20for%20iOS-iPadOS.png)

2. Name the policy.

   ![Name the policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/2%20-%20Name%20the%20policy.png)

3. Select the apps the policy targets (All Apps or selected public/store apps).

   ![Select All Apps for Target Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/3%20-%20Select%20All%20Apps%20for%20Target%20Policy.png)

4–5. Configure **Data Protection** settings (backup, sharing, cut/copy/paste, save-as restrictions, etc.).

   ![Configure Data Protection 1](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/4%20-%20Configure%20Data%20Protection.png)

   ![Configure Data Protection 2](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/5%20-%20Configure%20Data%20Protection.png)

6. Set **Access Requirements** (PIN, biometric, etc.).

   ![Set Access Requirements](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/6%20-%20Set%20Access%20Requirements.png)

7. Configure conditional launch / default actions.

   ![Set to Default](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/7%20-%20Set%20to%20Default.png)

8. Select the proper user group for assignment.

   ![Select the proper user group](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/8%20-%20Select%20the%20proper%20user%20group.png)

9. Review and Create.

   ![Review and Create](../extracted/intune_temp/Configure%20Microsoft%20Intune/Configure%20App%20Protection%20Policy/9%20-%20Review%20and%20Create.png)

---

## 7. Conditional Access – Enforce Windows MAM / Edge for BYOD

Create a Conditional Access policy that requires the use of a managed browser (Edge) or App Protection Policy for Windows BYOD scenarios.

### Steps

1. Start creating the Conditional Access policy “Enforce Windows MAM Edge for BYOD”.

   ![Enforce Windows MAM Edge for BYOD](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD/1%20-%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD.png)

2. Set the condition for client apps.

   ![Set the condition for client app](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD/2%20-%20Set%20the%20condition%20for%20client%20app.png)

3. Set the condition for device platforms (Windows).

   ![Set the condition for device platform](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD/3%20-%20Set%20the%20condition%20for%20device%20platfo.png)

4. Configure the grant controls (Require app protection policy / Require approved client app).

   ![Set grant access](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD/4%20-%20Set%20grant%20access.png)

5. Assign users to be **included**.

   ![Assign users to be included](../extracted/intune_temp/Configure%20Microsoft%20Intune/10%20-%20Assign%20users%20to%20be%20included.png)

6. Assign users to be **excluded** (break-glass / admin accounts).

   ![Assign users to be excluded](../extracted/intune_temp/Configure%20Microsoft%20Intune/10%20-%20Assign%20users%20to%20be%20excluded.png)

7. Final policy creation view.

   ![Create new CA policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD/9%20-%20Create%20new%20CA%20policy.png)

**Policy overview**

![Create Enforce Windows MAM Edge for BYOD policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/Create%20Enforce%20Windows%20MAM%20Edge%20for%20BYOD%20policy.png)

**List of Conditional Access Policies**

![List of Conditional Access Policy](../extracted/intune_temp/Configure%20Microsoft%20Intune/List%20of%20Conditional%20Access%20Policy.png)

---

## 8. Reference Screenshots

- Devices blade overview  
  ![Devices blade](../extracted/intune_temp/Configure%20Microsoft%20Intune/Devices%20blade.png)

- Endpoint Security Policies overview  
  ![Endpoint Security Policies](../extracted/intune_temp/Configure%20Microsoft%20Intune/Endpoint%20Security%20Policies.png)

### Blocked Words (for Naming Policies)

A sample `BlockedWords.csv` is included in the package. It contains common terms that should be blocked in group / Team names (Test, Temp, Confidential, Password, etc.).

---

## Related Guides

- [Configure Custom Domain](Configure-Custom-Domain.md)
- [Configure DNS](Configure-DNS.md)
- [Teams](Teams.md)
