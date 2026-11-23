# Create Device Compliance Message Notification

Creates the email/notification template that users receive when their device becomes noncompliant.

## Steps

### 1 – Create Notification Message Template
In Intune go to **Devices** → **Compliance policies** → **Notifications** → **Create notification**.

### 2 – Name the notification alert
Example: `Non-compliant Device Alert`.

### 3 – Verify the details
Confirm locale and basic settings.

### 4 – Create the subject and message
Write a clear subject and body, for example:
- Subject: `Your device is not compliant with company policy`
- Body: Explain that the device does not meet security requirements and provide steps or a link to the Company Portal / help desk.

### 5 – Link to noncompliance action
In the Compliance policy’s **Actions for noncompliance**, select this notification template so it is sent when a device is marked noncompliant.

### 6 – Confirm creation
The notification template appears in the list and is ready to use.

## Notes
- Keep the message short and actionable.
- You can create different templates for different locales or severity levels.
