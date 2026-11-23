# Create Enforce Windows MAM Edge for BYOD

Conditional Access policy that requires Windows BYOD users to use a managed browser (Edge) or app protection policy when accessing corporate resources.

## Prerequisites
- App protection policy already created (or approved client apps)
- Break-glass account excluded

## Steps

### 1 – Start the Conditional Access policy
In Entra ID / Intune go to **Conditional Access** → **New policy**.  
Name it clearly, e.g. `CA – Enforce Windows MAM / Edge for BYOD`.

### 2 – Condition: Client apps
Configure the client apps condition as required (browser / mobile apps and desktop clients).

### 3 – Condition: Device platform
Include **Windows**.  
You can exclude other platforms if they are covered by different policies.

### 4 – Grant access
Choose **Grant access** and require one or more of:
- Require approved client app
- Require app protection policy
- Require multifactor authentication (optional extra)

### 5 – Create the policy
Set to **Report-only** first, review sign-in logs, then switch to **On**.  
Always exclude at least one break-glass admin account.

## Notes
- This policy is especially useful for unmanaged Windows devices (BYOD).
- Test with the **What if** tool before enabling.
