# Configure Custom Domain

This guide documents the steps to add and verify a custom domain in Microsoft 365 / Entra ID (Azure AD), based on the provided screenshot sequence.

## Overview

Adding a custom domain allows your organization to use branded email addresses (e.g., `user@contoso.com`) and simplifies identity management across Microsoft 365 services.

## Prerequisites

- Global Administrator or Domain Name Administrator role in Microsoft 365 / Entra ID
- Access to the DNS provider for the domain (to create verification records)
- Domain ownership of the domain you want to add

## Step-by-Step Configuration

### Step 1 – Navigate to Custom Domain Settings
Open the Microsoft 365 admin center or Microsoft Entra admin center and go to the **Custom domain names** / **Domains** blade.

![Step 1](../extracted/Configure%20Custom%20Domain/1.png)

### Step 2 – Start Adding a Domain
Select **Add domain** (or equivalent action) to begin the domain registration process.

![Step 2](../extracted/Configure%20Custom%20Domain/2.png)

### Step 3 – Enter the Domain Name
Type the fully qualified domain name you want to add (e.g., `contoso.com`) and continue.

![Step 3](../extracted/Configure%20Custom%20Domain/3.png)

### Step 4 – Choose Verification Method
Select how you want to verify domain ownership. The most common method is adding a TXT record at your DNS provider.

![Step 4](../extracted/Configure%20Custom%20Domain/4.png)

### Step 5 – Obtain the Verification Record
Microsoft displays the TXT (or other) record values that must be created in your DNS zone.

![Step 5](../extracted/Configure%20Custom%20Domain/5.png)

### Step 6 – Add the Record at the DNS Provider
Log in to your DNS provider (Cloudflare, GoDaddy, Route 53, etc.) and create the exact TXT record shown by Microsoft.

![Step 6](../extracted/Configure%20Custom%20Domain/6.png)

### Step 7 – Verify the Domain
Return to the Microsoft admin center and click **Verify**. Microsoft will check for the presence of the verification record.

![Step 7](../extracted/Configure%20Custom%20Domain/7.png)

### Step 8 – Domain Verification Result
Confirm that the domain status changes to **Verified**.

![Step 8](../extracted/Configure%20Custom%20Domain/8.png)

### Step 9 – Configure Domain Services (Optional)
After verification you can choose which Microsoft 365 services (Exchange, Teams, etc.) the domain will be used for and set it as the default domain if desired.

![Step 9](../extracted/Configure%20Custom%20Domain/9.png)

### Step 10 – Review Domain List
The newly added domain now appears in the domains list with a verified status.

![Step 10](../extracted/Configure%20Custom%20Domain/10.png)

### Step 11 – Final Confirmation / DNS Records
Review any additional DNS records Microsoft recommends (MX, CNAME, TXT for SPF, etc.) so that mail flow and other services work correctly with the custom domain.

![Step 11](../extracted/Configure%20Custom%20Domain/11.png)

## Post-Configuration Tasks

1. Update MX records so email is delivered to Microsoft 365.
2. Add the recommended SPF, DKIM, and DMARC records (see the companion **Configure DNS** guide).
3. Set the new domain as the default if required.
4. Update user principal names (UPNs) or create new users with the custom domain.

## Related Guides

- [Configure DNS](Configure-DNS.md) – SPF, DKIM, DMARC and anti-phishing configuration
- [Configure Microsoft Intune](Configure-Microsoft-Intune.md)
- [Teams](Teams.md)
