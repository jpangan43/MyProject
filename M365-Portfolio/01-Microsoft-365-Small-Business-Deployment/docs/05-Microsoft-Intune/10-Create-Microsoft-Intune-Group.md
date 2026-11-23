# Create Microsoft Intune Group & Automatic Enrollment

Creates the Entra ID group used for Intune assignments and enables automatic MDM enrollment.

## Steps

### 1 – Create Intune Group
In the Entra admin center go to **Groups** → **New group**.  
Type: **Security**.

### 2 – Enter the group details
- Name: e.g. `All-Company-Windows` or `Pilot-Intune-Users`
- Membership type: Assigned (or Dynamic if you prefer automatic membership based on attributes)

### 3 – Turn on Automatic Enrollment
In **Entra ID** → **Mobility (MDM and MAM)** → **Microsoft Intune**:
- Set MDM user scope to the group you created (or **All**)

### 4 – Select All – MDM user scope
When scope is set to **All** (or the selected group), devices are automatically enrolled into Intune when users sign in with their work account on a supported device.

## Notes
- Prefer a pilot group first, then expand the MDM scope.
- Automatic enrollment is the foundation for all other Intune policies (compliance, configuration, apps).
