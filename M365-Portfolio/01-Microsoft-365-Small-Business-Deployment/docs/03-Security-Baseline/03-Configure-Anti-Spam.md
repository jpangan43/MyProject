# Configure Anti-Spam

Simple step-by-step guide to review the default Anti-spam policies in Microsoft Defender.

## Steps

### 1 – Open Policies & rules

1. Go to **Microsoft Defender** portal
2. Select **Email & collaboration** → **Policies & rules**
3. Click **Threat policies**

![Step 1](../extracted/Anti-Spam/Configure%20Anti-Spam/1.png)

---

### 2 – Open Anti-spam

On the Threat policies page, under **Policies**, select **Anti-spam**.

![Step 2](../extracted/Anti-Spam/Configure%20Anti-Spam/2.png)

---

### 3 – Review Anti-spam inbound policy (Default)

Select **Anti-spam inbound policy (Default)**. Key settings:

- Spam / High confidence spam → Move to Junk Email folder
- Phishing → Move to Junk Email folder
- High confidence phishing → Quarantine message
- Spam safety tips → On
- Quarantine policy → AdminOnlyAccessPolicy

![Step 3 - Inbound](../extracted/Anti-Spam/Configure%20Anti-Spam/3%20-%20Default%20Anti-spam%20Inbound%20Policy.png)

---

### 4 – Review Anti-spam outbound policy (Default)

Select **Anti-spam outbound policy (Default)**. Key settings:

- Message limits (external / internal / daily)
- Restriction when limit is reached
- Automatic forwarding rules
- Optional notifications for suspicious outbound mail

![Step 4 - Outbound](../extracted/Anti-Spam/Configure%20Anti-Spam/3%20-%20Default%20Anti-spam%20Outbound%20Policy.png)

![Step 4b](../extracted/Anti-Spam/Configure%20Anti-Spam/4%20-%20Default%20Anti-spam%20Outbound%20Policy.png)

---

## Notes

- Default inbound and outbound policies are always on.
- Create custom policies only when you need different actions for specific users or groups.
