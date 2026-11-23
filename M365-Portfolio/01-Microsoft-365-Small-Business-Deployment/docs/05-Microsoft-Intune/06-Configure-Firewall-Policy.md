# Configure Firewall Policy

Configures the Windows Firewall profiles (Domain, Private, Public) via Intune.

## Prerequisites
- Windows devices enrolled in Intune

## Steps

### 1 – Create Firewall Policy
In Intune go to **Endpoint security** → **Firewall** → **Create Policy**.  
Platform: **Windows 10, Windows 11, and Windows Server**.

### 2 – Name the Firewall Policy
Example: `Windows Firewall – Baseline`.

### 3 – Enable the three profiles
Set **Domain**, **Private**, and **Public** profiles to **Enabled** (True).  
Default inbound: Block, outbound: Allow is the usual secure baseline.  
Only open specific ports/apps if business applications require them.

### 4 – Assign to group
Assign to `All-Company-Windows` (or your Windows device group).

### 5 – Review and Create
Create the policy.  
Firewall settings apply relatively quickly on the next device check-in.

## Notes
- Avoid disabling the firewall “to make something work” — create explicit allow rules instead.
- Combine with ASR and Antivirus for better endpoint protection.
