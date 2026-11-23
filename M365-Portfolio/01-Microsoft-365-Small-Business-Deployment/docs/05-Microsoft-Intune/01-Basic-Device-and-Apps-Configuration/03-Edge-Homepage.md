# Edge Homepage & OneDrive Configuration Profile

Creates a Settings Catalog configuration profile that sets Microsoft Edge homepage/startup behaviour and OneDrive known-folder settings on Windows devices.

## Prerequisites
- Windows 10/11 devices enrolled in Intune
- Device group for assignment

## Steps

### 1 – Creating configuration profile for Edge Homepage
In Intune go to **Devices** → **Configuration** → **Create** → **New policy**.  
Platform: **Windows 10 and later**, Profile type: **Settings catalog**.

### 2 – Name the configuration profile
Example: `Windows – Edge Homepage & OneDrive`.

### 3 – Add OneDrive and Edge settings
In the Settings picker add:
- **Microsoft Edge** settings (homepage, startup pages, restore on startup, etc.)
- **OneDrive** settings (silently sign in, Known Folder Move, etc.)

### 4 – Verify Microsoft Edge settings
Common settings:
- Set homepage to your company portal or intranet URL
- Configure startup pages
- Optionally force Edge as default browser (if desired)

### 5 – Verify OneDrive settings
Useful settings:
- Silently sign in users to OneDrive
- Move known folders (Documents, Desktop, Pictures) to OneDrive
- Prevent users from redirecting known folders back to the device

This improves backup and makes files available across devices.

### 6 – Add group assignment
Assign to your Windows device group (pilot first if preferred).

### 7 – Review and Create
Review the summary and create the profile.

### 8 – Confirm completion
The configuration profile shows as created and will apply on the next device check-in.

## Notes
- Settings Catalog is the modern way to configure Edge and OneDrive; prefer it over older Administrative Templates when possible.
- Known Folder Move is one of the highest-value OneDrive settings for protecting user files.
