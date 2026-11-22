# Conditional Access Configuration

This guide follows the exact numbered sequence shown in the screenshots for creating and validating Conditional Access policies in Microsoft Entra ID.

## Overview

Conditional Access policies enforce access requirements (such as MFA, compliant device, or block) when specific conditions are met. The screenshots demonstrate creating the first policy (**CA001 – Require MFA for Administrators**) and then validating the full policy set with the **What if** tool, a blocked sign-in example, and sign-in logs.

**Policies created in this series:**

| Policy | Name |
|--------|------|
| CA001 | Require MFA for Administrators |
| CA002 | Require MFA for All Users |
| CA003 | Block Legacy Authentication |
| CA004 | Require Compliant Device |
| CA005 | Block Unsupported Platforms |

---

## Step-by-Step Configuration

### 1 – Open Conditional Access and start a new policy

In the **Microsoft Entra admin center**:

1. Go to **Conditional Access**
2. Select **Policies**
3. Click **+ New policy**

![Step 1](../extracted/Conditional-Access/Conditional%20Access%20Configuration/1.png)

---

### 2 – Name the policy and include Directory roles

1. **Name:** `CA001 - Require MFA for Administrators`
2. Under **Users** → **Include**:
   - Select **Directory roles**
   - Choose the administrative roles that should require MFA (5 roles selected in the example)

![Step 2](../extracted/Conditional-Access/Conditional%20Access%20Configuration/2.png)

---

### 3 – Exclude break-glass account

1. Switch to the **Exclude** tab
2. Select **Users and groups**
3. Add the break-glass / emergency admin account (e.g. `Breakglass-Admin`) so it is never locked out by this policy

![Step 3](../extracted/Conditional-Access/Conditional%20Access%20Configuration/3.png)

---

### 4 – Target resources = All resources

1. Open **Target resources**
2. On the **Include** tab select **All resources (formerly 'All cloud apps')**

> Warning: This affects the Azure / Entra portal itself. Ensure at least one break-glass account is excluded before enabling the policy.

![Step 4](../extracted/Conditional-Access/Conditional%20Access%20Configuration/4.png)

---

### 5 – Grant control = Require multifactor authentication

1. Open **Grant**
2. Select **Grant access**
3. Check **Require multifactor authentication**
4. Click **Select**

![Step 5](../extracted/Conditional-Access/Conditional%20Access%20Configuration/5.png)

---

### 6 – Set policy to Report-only and create

1. Set **Enable policy** to **Report-only** (recommended for initial testing)
2. Choose to exclude the current user if prompted
3. Click **Create**

![Step 6](../extracted/Conditional-Access/Conditional%20Access%20Configuration/6.png)

---

### 7 – Review the policy list

After creation (and after creating the remaining policies CA002–CA005 using the same pattern), the **Policies** blade shows all five user-created policies in **Report-only** state.

![Step 7](../extracted/Conditional-Access/Conditional%20Access%20Configuration/7.png)

---

### 8 – Test with the What if tool

1. Open **What if**
2. Select a user (e.g. **CEO**)
3. Select a target cloud app (e.g. **M365 Admin Services**)
4. Optionally set device platform, client app, IP, etc.

![Step 8](../extracted/Conditional-Access/Conditional%20Access%20Configuration/8.png)

---

### 9 – Review policies that will apply

Click **What if**. Under **Policies that will apply** you can see which Conditional Access policies match the simulated sign-in (CA001, CA002, CA003, CA005 in the example).

![Step 9](../extracted/Conditional-Access/Conditional%20Access%20Configuration/9.png)

---

### 10 – Review policies that will not apply

Switch to the **Policies that will not apply** tab to see policies that do not match the current conditions (e.g. CA004 – Require Compliant Device does not apply because the simulated user/group filter does not match).

![Step 10](../extracted/Conditional-Access/Conditional%20Access%20Configuration/10.png)

---

### 11 – Blocked access example

When a policy is later switched from Report-only to **On** and the user fails the required controls, the sign-in is blocked with the message:

> **You cannot access this right now**  
> Your sign-in was successful but does not meet the criteria to access this resource.

![Step 11](../extracted/Conditional-Access/Conditional%20Access%20Configuration/11%20Blocked%20Access.png)

---

### 12 – Verify in Sign-in logs

In **Conditional Access → Sign-in logs** (or the user’s sign-in activity):

1. Open a sign-in event
2. Go to the **Conditional access** tab
3. Review each policy’s **Result** (Failure / Not applied / Success)

This confirms which policies evaluated and whether access was granted or blocked.

![Step 12](../extracted/Conditional-Access/Conditional%20Access%20Configuration/12%20Sign-in%20logs.png)

---

## Recommended Rollout Order

1. Create all policies in **Report-only** mode.
2. Use **What if** and **Sign-in logs** to validate impact.
3. Exclude at least one break-glass account from every policy.
4. Disable Security Defaults (if still enabled) before turning policies to **On**.
5. Enable policies one at a time, starting with the least disruptive (e.g. Block Legacy Authentication), and monitor for several days.

## Related Guides

- [Configure Custom Domain](Configure-Custom-Domain.md)
- [Configure DNS](Configure-DNS.md)
- [Configure DKIM](Configure-DKIM.md)
- [Configure Microsoft Intune](Configure-Microsoft-Intune.md)
- [Teams](Teams.md)
