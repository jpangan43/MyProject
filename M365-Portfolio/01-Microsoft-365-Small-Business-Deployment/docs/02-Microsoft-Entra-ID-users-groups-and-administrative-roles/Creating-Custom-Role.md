# Creating Custom Role

Simple step-by-step guide to create a custom role in Microsoft Entra ID (example: Admin-Breakglass).

## Steps

### 1 – Open Roles & admins and start a new custom role

1. Go to **Roles & admins**
2. Click **+ New custom role**

![Step 1](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/1.png)

---

### 2 – Basics

1. **Name:** e.g. `Admin-Breakglass`
2. **Description:** Emergency Global admin account that can manage all aspects of Microsoft Entra ID and Microsoft services that use Microsoft Entra identities.
3. **Baseline permissions:** Start from scratch
4. Click **Next**

![Step 2](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/2.png)

---

### 3 – Permissions

Select the permissions required for the role, then click **Next**.

![Step 3](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/3.png)

---

### 4 – Review + create

Review the role name, description, and selected permissions, then click **Create**.

![Step 4](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/4.png)

---

### 5 – Confirm the custom role is created

The new custom role (`Admin-Breakglass`) appears in the **All roles** list with type **Custom**.

![Step 5](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/5.png)

![Break-glass Account](../extracted/Creating-Custom-Role/Creating%20Custom%20Role/Break-glass%20Account.png)

---

## Notes

- Custom roles are useful for least-privilege break-glass / emergency access scenarios.
- After creation, assign the role to a dedicated break-glass account and exclude that account from Conditional Access policies that could lock it out.
