# Configure Teams Governance

Step-by-step guide for Teams creation control, naming policy, expiration, and external access.

## Steps

### 1 – Security groups for allowed creators
Create security groups that will be allowed to create Teams.

### 2 – Team Creators group
Create the **Team Creators** group (used to restrict who can create Teams).

### 3 – Upload Blocked Words list
Upload a blocked words list (CSV) for the naming policy.

### 4 – Create Group Naming Policy
Configure the Microsoft 365 Groups naming policy (prefix/suffix + blocked words).

### 5 – Configure Inactive Team Policy
Set the group/Team expiration (inactive Team) policy.

### 6 – Create Teams Policy
Create or configure a Teams policy as needed.

### 7 – Set Guest Access
Configure guest access settings for Teams.

### 8 – Set External Access
Configure external access (federation) settings.

### 9 – Set External Collaboration Settings
Configure external collaboration settings in Entra ID / Microsoft 365.

### 10 – Create Simple Microsoft Form
Create a request form (e.g. for Team creation requests).

### 11 – Create Power Automate Flow
Create a Power Automate flow to process the form.

### 12 – Name the flow and Create
Name and create the flow.

### 13 – Set the Parameters
Configure the flow parameters (approvals, group creation, etc.).

---

## Summary

| Area | Action |
|------|--------|
| Who can create Teams | Security group + Teams creation restricted |
| Naming | Group naming policy + blocked words |
| Lifecycle | Inactive / expiration policy |
| Guests & external | Guest access, external access, collaboration settings |
| Request process | Microsoft Form + Power Automate |
