# Deploy Microsoft 365 Apps

Deploys the Microsoft 365 Apps suite (Word, Excel, PowerPoint, Outlook, Teams, etc.) to Windows devices through Intune.

## Prerequisites
- Intune and Microsoft 365 Apps licenses
- Device or user group for assignment

## Steps

### 1 – Create Microsoft 365 Apps
In Intune go to **Apps** → **Windows** → **Add** → **Microsoft 365 Apps**.

### 2 – Enter app suite information
Select the architecture (64-bit recommended) and update channel:
- **Current Channel** – latest features
- **Monthly Enterprise Channel** – more predictable monthly updates
- **Semi-Annual Enterprise Channel** – fewer updates, more stability

Most organisations use Monthly Enterprise or Current Channel.

### 3 – Configure app suite
Choose which apps to include or exclude (e.g. exclude Access or Publisher if not needed).  
You can also set the default file format (Office Open XML) and shared computer activation if required.

### 4 – Add group assignment
Assign as **Required** to a device or user group so the apps install automatically.  
Use a pilot group first.

### 5 – Review and create
Review the configuration and create the app deployment.

### 6 – Confirm completion
The Microsoft 365 Apps deployment appears in the apps list and will install on targeted devices at the next check-in.

## Notes
- Installation can take 15–30+ minutes depending on network and device.
- Users need a Microsoft 365 Apps license to activate and use the apps.
- You can create multiple deployments (e.g. one for Current Channel pilot, one for Monthly Enterprise production).
