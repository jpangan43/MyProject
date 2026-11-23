# Configure Disk Encryption Policy (BitLocker)

Forces BitLocker encryption on Windows devices so data at rest is protected.

## Prerequisites
- Windows 10/11 Pro, Enterprise, or Education
- TPM 1.2 or 2.0 recommended

## Steps

### 1 – Create Disk Encryption Policy
In Intune go to **Endpoint security** → **Disk encryption** → **Create Policy**.  
Platform: **Windows 10 and later**, Profile: **BitLocker**.

### 2 – Name the policy
Example: `BitLocker – Require Encryption`.

### 3 – Set configuration settings
Typical settings:
- Encrypt devices: **Require**
- Encryption method: XTS-AES 128 or 256
- Require authentication at startup (TPM only, or TPM + PIN)
- Recovery options: Store recovery key in Entra ID / Azure AD
- Hide prompt to store recovery key (if you want silent encryption)

Storing the recovery key in Entra ID is critical so users can recover if they forget a PIN.

### 4 – Assign to group
Assign to Windows device group.  
Consider a pilot group first; encryption can take time on large disks.

### 5 – Review and create
Create the policy. Devices will begin encryption after the policy applies and the user is signed in.

## Notes
- Encryption status can be monitored in Intune device compliance / encryption reports.
- Pair with a Compliance policy that requires BitLocker to be enabled.
