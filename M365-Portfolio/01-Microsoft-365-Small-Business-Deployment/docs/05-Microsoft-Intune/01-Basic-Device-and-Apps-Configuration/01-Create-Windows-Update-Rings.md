# Create Windows Update Rings

Controls when and how Windows quality and feature updates are offered to devices via Intune.

## Prerequisites
- Windows 10/11 devices enrolled in Intune
- Device group for assignment (pilot recommended)

## Steps

### 1 – Create profile for Windows update rings
In the Intune admin center go to **Devices** → **Windows** → **Update rings for Windows 10 and later** → **Create profile**.

### 2 – Name the update rings
Use a clear name that indicates the ring purpose, for example:
- `Windows 11 – Pilot`
- `Windows 11 – Broad`

### 3 – Update ring settings
Typical settings:
- **Microsoft product updates**: Allow
- **Windows drivers**: Allow
- **Quality update deferral**: 0–7 days for pilot, 7–14 days for broad
- **Feature update deferral**: 0 days (pilot) or longer if you want to delay major upgrades
- **Automatic update behavior**: Auto install at maintenance time / restart warnings as needed
- **Active hours**: Set so restarts happen outside business hours
- **User restart checks / deadline**: Optional but useful to force lagging devices

Start with a pilot ring that receives updates first, then a broader ring that defers a few days.

### 4 – Add assignment
Assign to a device group.  
Always pilot with a small group before targeting all company devices.

### 5 – Review and create
Review the summary and create the profile.

### 6 – Confirm creation
The update ring appears in the list (e.g. “Windows 11 Update Ring Created”).

## Notes
- Update rings manage *when* updates install; feature update policies can also pin a specific Windows version.
- Monitor the **Windows updates** reports in Intune to see success/failure per device.
