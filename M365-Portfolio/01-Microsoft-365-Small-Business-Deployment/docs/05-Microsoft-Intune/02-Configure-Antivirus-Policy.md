# Configure Antivirus Policy

Endpoint security policy in Microsoft Intune that configures Microsoft Defender Antivirus on Windows devices.

## Prerequisites
- Intune Administrator or Endpoint Security Manager role
- A device group to assign (e.g. All-Company-Windows)

## Steps

### 1 – Create the policy profile
In the Microsoft Intune admin center go to **Endpoint security** → **Antivirus** → **Create Policy**.  
Choose platform **Windows 10 and later** and profile type **Microsoft Defender Antivirus**.

### 2 – Name the policy
Give a clear name such as `Windows Defender Antivirus – Baseline` and an optional description.  
Good naming makes it easier to find later when you have many policies.

### 3 – Set configuration settings
Typical recommended settings:
- Real-time protection: **Enabled**
- Cloud-delivered protection: **Enabled**
- Automatic sample submission: **Send safe samples automatically**
- Scan archive files / removable drives as needed
- PUA (Potentially Unwanted App) protection: **Enabled**

Leave advanced options at Microsoft defaults unless you have a specific requirement.

### 4 – Assign to a group
Assign to your Windows device group (e.g. `All-Company-Windows` or a pilot group first).  
Use a pilot group before rolling out to everyone.

### 5 – Review and create
Review the summary and create the policy.  
Devices will receive the settings on the next Intune check-in (usually within a few hours, or force a sync from the Company Portal).

## Notes
- This policy works together with the **Compliance policy** that requires antivirus to be on and up to date.
- For stricter control, also configure **Attack Surface Reduction** rules.
