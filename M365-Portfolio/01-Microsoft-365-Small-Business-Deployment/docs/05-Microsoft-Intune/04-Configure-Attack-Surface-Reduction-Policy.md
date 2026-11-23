# Configure Attack Surface Reduction (ASR) Policy

ASR rules reduce the ways malware can get onto Windows devices by blocking common attack techniques.

## Prerequisites
- Windows 10/11 devices managed by Intune
- Microsoft Defender Antivirus active

## Steps

### 1 – Create ASR Policy
In Intune go to **Endpoint security** → **Attack surface reduction** → **Create Policy**.  
Platform: **Windows 10, Windows 11, and Windows Server**.

### 2 – Name the ASR Policy
Example: `ASR – Standard Protection`.

### 3 – Set configuration settings
Recommended starting mode for most rules: **Block** (or **Audit** first for testing).

Important rules to enable:
- Block executable content from email client and webmail
- Block Office applications from creating child processes
- Block Office applications from injecting code into other processes
- Block JavaScript/VBScript from launching downloaded executable content
- Block credential stealing from LSASS
- Block untrusted and unsigned processes that run from USB

Start in **Audit** mode for 1–2 weeks, review the reports, then switch to **Block**.

### 4 – Assign to Windows group
Assign to your Windows device group.  
Pilot with a small group first.

### 5 – Review and Create
Create the policy. Monitor the ASR reports in Microsoft Defender / Intune for any legitimate business apps that get blocked so you can add exclusions.

## Notes
- ASR is one of the strongest free protections available on Windows.
- Combine with Antivirus, Firewall, and BitLocker policies for defense in depth.
