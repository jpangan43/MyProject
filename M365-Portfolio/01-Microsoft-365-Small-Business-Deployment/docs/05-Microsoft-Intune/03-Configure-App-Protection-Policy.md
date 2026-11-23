# Configure App Protection Policy (MAM)

App protection policies protect corporate data inside managed apps on mobile devices (even if the device is not enrolled).

## Prerequisites
- Intune App Protection license (or Microsoft 365 E3/E5)
- Target user group

## Steps

### 1 – Create MAM policy for iOS/iPadOS
In Intune go to **Apps** → **App protection policies** → **Create policy** → **iOS/iPadOS**  
(Repeat the same process later for Android if needed.)

### 2 – Name the policy
Use a clear name, e.g. `MAM – iOS – All Users`.

### 3 – Select apps
Choose **All apps** or select specific public store apps (Outlook, Teams, OneDrive, Edge, etc.).  
Starting with “All apps” is simpler; you can narrow later.

### 4–5 – Configure Data Protection
Key settings:
- Prevent backup of org data to iTunes/iCloud
- Send org data to other apps: **Policy managed apps**
- Receive data from other apps: **All apps** or more restrictive
- Save copies of org data: **Block** (or allow only OneDrive/SharePoint)
- Restrict cut/copy/paste between apps

These controls keep corporate data from leaking into personal apps.

### 6 – Set Access Requirements
- PIN for access: **Yes** (minimum length 4–6)
- Biometrics allowed: optional
- Disable app after offline grace period (e.g. 30–90 days)
- Wipe data after a number of failed PIN attempts

### 7 – Conditional launch / defaults
Use the recommended default actions for jailbroken devices, outdated OS, etc.  
Typically: **Block access** or **Wipe data** for high-risk conditions.

### 8 – Assign user group
Assign to the appropriate user group (not device group).  
MAM is user-based.

### 9 – Review and create
Create the policy. Users will see the policy applied the next time they open a managed app and sign in with their work account.

## Notes
- Pair this with a Conditional Access policy that requires an approved client app or app protection policy.
- For Windows BYOD, use the separate “Enforce Windows MAM Edge” Conditional Access policy.
