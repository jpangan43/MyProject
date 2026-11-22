# Create User Group

Simple step-by-step guide to create a security group in Microsoft Entra ID.

## Steps

### 1 – Open Groups and start a new group

1. Go to **Groups**
2. Select **All groups**
3. Click **New group**

![Step 1](../extracted/Create-User-Group/Create%20User%20Group/1.png)

---

### 2 – Configure the group

1. **Group type:** Security
2. **Group name:** e.g. `SG-Employees`
3. Turn **on** “Microsoft Entra roles can be assigned to the group” (optional)
4. Click **Owners** → select an owner (e.g. Finance Manager) → **Select**
5. Click **Create**

![Step 2](../extracted/Create-User-Group/Create%20User%20Group/2.png)

---

### 3 – Confirm the group is created

The new security groups appear in the **All groups** list (e.g. SG-Employees, SG-Finance, SG-HR, SG-IT, SG-Management, etc.).

![Step 3](../extracted/Create-User-Group/Create%20User%20Group/3.png)

---

## Notes

- Use the **Security** group type for Conditional Access, Intune, and role assignments.
- Naming convention used: `SG-<Department>` or `SG-<Purpose>`.
