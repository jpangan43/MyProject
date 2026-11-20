# Configure DNS

This guide covers the DNS records and Microsoft 365 security policies required for a properly secured custom domain (SPF, DKIM, DMARC, anti-phishing).

## Overview

Correct DNS configuration is essential for:

- Reliable email delivery
- Protection against spoofing and phishing
- Passing DMARC authentication checks
- Enabling DKIM signing of outbound messages

## 1. Configure DKIM

DKIM (DomainKeys Identified Mail) cryptographically signs outbound messages so receiving servers can verify they were not altered in transit.

### Steps

1. Open the Microsoft 365 Defender / Exchange admin center and navigate to **Email authentication settings** → **DKIM**.

   ![DKIM – Start](../extracted/Configure%20DNS/Configure%20DKIM/1.png)

2. Select the domain you want to enable DKIM for.

   ![DKIM – Select Domain](../extracted/Configure%20DNS/Configure%20DKIM/2.png)

3. Microsoft displays the two CNAME records that must be created in your DNS zone (`selector1._domainkey` and `selector2._domainkey`).

   ![DKIM – CNAME Records](../extracted/Configure%20DNS/Configure%20DKIM/3.png)

4. Add the CNAME records at your DNS provider.

   ![DKIM – Add CNAMEs](../extracted/Configure%20DNS/Configure%20DKIM/4.png)

5. Return to the Microsoft portal and enable DKIM signing for the domain.

   ![DKIM – Enable](../extracted/Configure%20DNS/Configure%20DKIM/5.png)

6. Confirm the status shows as **Enabled**.

   ![DKIM – Status](../extracted/Configure%20DNS/Configure%20DKIM/6.png)

7. Final verification that DKIM is active.

   ![DKIM – Complete](../extracted/Configure%20DNS/Configure%20DKIM/7.png)

### Final DKIM Configuration View

![DKIM Configuration Overview](../extracted/Configure%20DNS/01-DKIM-Configuration.png)

---

## 2. Add SPF Record (Cloudflare Example)

An SPF (Sender Policy Framework) TXT record tells receiving mail servers which hosts are authorized to send mail for your domain.

### Steps

1. In Cloudflare (or your DNS provider) create a TXT record for the root domain (`@` or the domain name itself).

2. Use a value similar to:

   ```
   v=spf1 include:spf.protection.outlook.com -all
   ```

   (Adjust includes if you have additional legitimate senders.)

   ![Add SPF in Cloudflare](../extracted/Configure%20DNS/Add%20SPF%20in%20Cloudflare/1.png)

---

## 3. Add DMARC Record

DMARC (Domain-based Message Authentication, Reporting & Conformance) builds on SPF and DKIM and tells receivers what to do with messages that fail authentication. It also provides aggregate and forensic reports.

### Steps

1. Create a TXT record for the subdomain `_dmarc`.

2. Recommended starting policy (monitor mode):

   ```
   v=DMARC1; p=none; rua=mailto:dmarc-reports@yourdomain.com; ruf=mailto:dmarc-forensics@yourdomain.com; fo=1
   ```

   Later tighten to `p=quarantine` or `p=reject` once you are confident in the results.

   ![Add DMARC](../extracted/Configure%20DNS/Add%20DMARC/1.png)

---

## 4. Anti-Phishing Policy

Configure Microsoft Defender for Office 365 anti-phishing policies to protect users.

![Anti-phishing Policy](../extracted/Configure%20DNS/02-Anti-phishing-policy.png)

Key settings typically include:

- Impersonation protection (users and domains)
- Spoof intelligence
- Mailbox intelligence
- Advanced phishing thresholds

---

## 5. Audit Log Example

After configuration, use the audit log / message trace to verify that authentication results (SPF, DKIM, DMARC) are being recorded correctly.

![Audit Log Example](../extracted/Configure%20DNS/03-Audit-log-example.png)

---

## Recommended DNS Record Summary

| Type  | Host / Name              | Value / Points to                                      | Purpose          |
|-------|--------------------------|--------------------------------------------------------|------------------|
| TXT   | `@`                      | `v=spf1 include:spf.protection.outlook.com -all`       | SPF              |
| CNAME | `selector1._domainkey`   | `selector1-<domain>._domainkey.<tenant>.onmicrosoft.com` | DKIM             |
| CNAME | `selector2._domainkey`   | `selector2-<domain>._domainkey.<tenant>.onmicrosoft.com` | DKIM             |
| TXT   | `_dmarc`                 | `v=DMARC1; p=none; rua=mailto:...`                     | DMARC            |
| MX    | `@`                      | `<tenant>.mail.protection.outlook.com`                 | Mail routing     |

> Replace placeholders with the exact values shown in your Microsoft 365 admin center.

## Related Guides

- [Configure Custom Domain](Configure-Custom-Domain.md)
- [Configure Microsoft Intune](Configure-Microsoft-Intune.md)
- [Teams](Teams.md)
