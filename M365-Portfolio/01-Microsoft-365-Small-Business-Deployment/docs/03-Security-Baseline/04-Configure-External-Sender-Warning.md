# Configure External Sender Warning

Simple step-by-step guide to create a mail flow rule that prepends `[External]` to the subject of messages from external senders.

## Steps

### 1 – Create a new mail flow rule

1. Open the **Exchange admin center**
2. Go to **Mail flow** → **Rules**
3. Click **+ Add a rule** → **Create a new rule**

![Step 1](../extracted/External-Sender/Configure%20External%20sender%20warning/1.png)

---

### 2 – Set rule conditions

1. **Name:** `External Sender Warning`
2. **Apply this rule if:** The sender is external/internal → **NotInOrganization**
3. **Do the following:** Prepend the subject of the message with → `[External]`

![Step 2](../extracted/External-Sender/Configure%20External%20sender%20warning/2%20-%20Set%20rule%20conditions.png)

---

### 3 – Set rule settings

Configure rule mode, severity, and any additional options as needed, then continue.

![Step 3](../extracted/External-Sender/Configure%20External%20sender%20warning/3%20-%20Set%20rule%20settings.png)

---

### 4 – Review and finish

Review the rule summary and click **Finish** / **Save**.

![Step 4](../extracted/External-Sender/Configure%20External%20sender%20warning/4%20-%20Review%20and%20Finish.png)

---

### 5 – Confirm the rule is enabled

The **External Sender Warning** rule appears in the rules list and is enabled.

![Step 5](../extracted/External-Sender/Configure%20External%20sender%20warning/5%20-%20External%20Sender%20Warning%20Enabled.png)

---

### 6 – Related: DNS authentication (SPF, DKIM, DMARC)

Ensure SPF, DKIM, and DMARC are correctly configured so external-sender detection works reliably.

![Step 6](../extracted/External-Sender/Configure%20External%20sender%20warning/6%20-%20DNS%20%28SPF%2C%20DKIM%2C%20DMARC%29.png)

---

### 7 – Related: Mailbox auditing (Microsoft Purview)

Mailbox auditing can be reviewed in Microsoft Purview for additional monitoring.

![Step 7](../extracted/External-Sender/Configure%20External%20sender%20warning/7%20-%20Mailbox%20auditing%20located%20at%20Microsoft%20Purview.png)

---

## Notes

- The rule adds `[External]` to the subject of messages from senders outside the organization.
- This helps users quickly identify external email and reduce phishing risk.
