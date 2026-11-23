# Create Baseline Compliance Policy

Compliance policies define the rules a device must meet to be considered compliant. Conditional Access can then require a compliant device.

## Prerequisites
- Intune licensed users/devices
- Device group for assignment (e.g. Pilot-Intune-Users)

## Steps

### 1 – Create Compliance Policy
In Intune go to **Devices** → **Compliance policies** → **Create policy**.  
Platform: **Windows 10 and later**.

### 2 – Name the policy
Example: `Windows 11 – Baseline Compliance`.

### 3 – Device Health settings
Require:
- BitLocker
- Secure Boot
- Code integrity

### 4 – System Security settings
Typical requirements:
- Password/PIN required
- Minimum password length
- Device encryption
- Firewall enabled
- Antivirus enabled and up to date
- Antispyware enabled

### 5 – Antivirus and Defender
Require Microsoft Defender Antivirus to be enabled and signatures up to date.  
This ties into the Antivirus policy you configured separately.

### 6 – Actions for noncompliance
Common configuration:
- Mark device noncompliant immediately (or after a grace period)
- Send email to user
- Optionally retire or remote lock after a longer period

### 7 – Assign the group
Add the pilot group first (`Pilot-Intune-Users`), then expand later.

### 8–9 – Review and create
Create the policy and confirm it appears as created.  
Devices will evaluate compliance on the next check-in.

## Notes
- Always start with a pilot group.
- Use the **Device compliance** reports to see which devices are noncompliant and why.
- Pair with Conditional Access “Require compliant device”.
