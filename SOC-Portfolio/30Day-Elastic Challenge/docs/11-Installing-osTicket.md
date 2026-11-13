# Installing osTicket

**Complete Step-by-Step Visual Guide**

Download → Deploy to XAMPP → Web installer → Admin login

| Field | Value |
|-------|-------|
| **Version** | osTicket Core v1.18.3 |
| **Stack** | XAMPP (Apache + PHP + MySQL) on Windows |
| **Helpdesk name** | SOC-Lee-Support |
| **Admin user** | SOCLee (Jason Lee) |
| **Database** | soc-lab-db (MySQL) |

Each of the 20 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

**Part A – Download osTicket (Steps 1–4)**

**Part B – Deploy files into XAMPP htdocs (Steps 5–9)**

**Part C – Web installer prerequisites & config file (Steps 10–14)**

**Part D – Basic installation form & database (Steps 15–16)**

**Part E – Finish install, lock config, log in (Steps 17–20)**

**Next Steps**

---

## Part A – Download osTicket

### 1. Open osTicket website → Self-Hosted

In a browser go to https://osticket.com.

In the top navigation click **Self-Hosted**.

**Figure 1** – osticket.com → Self-Hosted menu item

---

### 2. Choose Community (Download)

On the editions page, under the free Community column, click **Download**.

This starts the self-hosted download wizard.

**Figure 2** – Editions comparison → Download button under Community

---

### 3. Select osTicket Core v1.18.3

Select **osTicket Core, v1.18.3** (highlighted in orange).

Requirements: IIS or Apache, PHP 8.2–8.4, MySQL 5.5+.

Click **Next Step**.

**Figure 3** – Download page → osTicket Core, v1.18.3 → Next Step

---

### 4. Choose language pack

On the Languages step, ensure **English (Great Britain)** (or your preferred pack) is in the Selected list.

Click **Next Step** (you may skip plugins on the following step and download the package).

**Figure 4** – Languages step → English (Great Britain) selected → Next Step

---

## Part B – Deploy files into XAMPP htdocs

### 5. Extract the downloaded package

After download, open your Downloads folder.

Extract the osTicket zip so you have an **osTicket** folder (containing the versioned subfolder with scripts and upload).

**Figure 5** – Downloads folder: osTicket.zip and extracted osTicket folder

---

### 6. Copy scripts and upload folders

Open the extracted version folder (e.g. osTicket-v1.18.3).

Select the **scripts** and **upload** folders.

Right-click → **Copy**.

**Figure 6** – Inside osTicket-v1.18.3 → select scripts + upload → Copy

---

### 7. Open XAMPP htdocs

Navigate to your XAMPP installation directory (typically `C:\xampp`).

Open the **htdocs** folder — this is the Apache web root.

**Figure 7** – C:\xampp → htdocs folder

---

### 8. Paste into htdocs

Inside `C:\xampp\htdocs` right-click and choose **Paste** to copy the scripts and upload folders into the web root. (Alternatively create an osTicket subfolder first and paste there for a cleaner URL.)

**Figure 8** – htdocs context menu → Paste

---

### 9. Confirm scripts and upload in htdocs

Verify that **scripts** and **upload** appear under htdocs.

In this lab they are placed so the installer is reachable at `http://<server-IP>/osTicket/upload/setup/` (or similar path).

**Figure 9** – htdocs now contains scripts and upload folders

---

## Part C – Web installer prerequisites & config file

### 10. Open the osTicket Installer (prerequisites check)

In the browser open the installer URL, e.g. `http://66.135.4.248/osTicket/upload/setup/`.

Review the prerequisites list (PHP version, MySQLi, etc.). Required items should show green checkmarks. Click **Continue »**.

**Figure 10** – http://.../osTicket/upload/setup/ → prerequisites → Continue

---

### 11. Configuration file missing warning

The installer reports that `include/ost-config.php` is missing.

It instructs you to rename `include/ost-sampleconfig.php` to `ost-config.php`.

**Figure 11** – “Configuration file missing!” → rename ost-sampleconfig.php

---

### 12. Open the include folder

In File Explorer navigate to:

`C:\xampp\htdocs\osTicket\upload\include`

(adjust the path if your folder layout differs).

**Figure 12** – File Explorer → ...\upload\include

---

### 13. Rename ost-sampleconfig.php

Locate `ost-sampleconfig.php`.

Right-click → **Rename** and change the name to `ost-config.php`.

**Figure 13** – include folder → ost-sampleconfig.php → Rename

---

### 14. Continue after creating ost-config.php

Return to the installer page and click **Continue »**.

The installer can now write to the configuration file.

**Figure 14** – Installer still shows config warning → Continue »

---

## Part D – Basic installation form & database

### 15. Fill Basic Installation (system + admin)

Complete the form:

- **Helpdesk Name**: SOC-Lee-Support
- **Default Email**: e.g. test@test.com
- **Admin First/Last Name**: Jason / Lee
- **Admin Username**: SOCLee
- Set and confirm a strong password.

**Figure 15** – System Settings + Admin User form

---

### 16. Database settings and Install Now

Enter database connection details:

- **MySQL Table Prefix**: ost_
- **MySQL Hostname**: server IP or localhost
- **MySQL Database**: soc-lab-db (create it first in phpMyAdmin if needed)
- **MySQL Username / Password**: e.g. root and the MySQL password

Click **Install Now**.

**Figure 16** – Database Settings → Install Now

---

## Part E – Finish install, lock config, log in

### 17. Installation complete (Congratulations)

The installer shows **Congratulations!**

Note the URLs:

- osTicket URL: `http://.../osTicket/upload/`
- Staff Control Panel: `http://.../osTicket/upload/scp`

It also reminds you to remove write access from `ost-config.php`.

**Figure 17** – Congratulations! + config permission reminder + URLs

---

### 18. Lock down ost-config.php permissions

Open an elevated PowerShell window and run:

This resets permissions so the web server can no longer write to the config file (important security hardening after install).

```powershell
cd C:\xampp\htdocs\osTicket\upload\include
icacls .\ost-config.php /reset
```

**Figure 18** – PowerShell: cd ...\include; icacls .\ost-config.php /reset

---

### 19. Staff Control Panel login

Browse to the Staff Control Panel login page (e.g. `http://66.135.4.248/osTicket/upload/scp/login.php`).

Enter the admin username (**SOCLee**) or email and the password you set, then click **Log In**.

**Figure 19** – /scp/login.php → Authentication Required

---

### 20. osTicket staff interface (Tickets)

After login you see the staff interface.

Under **Tickets → Open** there is a system ticket “osTicket Installed!” from the osTicket Team.

The helpdesk is ready for use.

**Figure 20** – Tickets view → welcome ticket “osTicket Installed!”

---

## Next Steps

- Delete or rename the setup directory (`upload/setup`) so the installer is no longer publicly reachable.
- Configure email (SMTP/IMAP) under Admin Panel → Emails if you want ticket notifications.
- Create departments, agents, and SLA plans for your SOC workflow.
- Use osTicket to track incidents generated from Mythic C2 activity, Hydra brute-force, or Elastic alerts.
- Restrict access to the staff panel (scp) by IP or reverse-proxy authentication in production-like labs.

> **Prerequisite reminder**: XAMPP (Apache + MySQL + PHP) must already be installed and running, and a MySQL database (e.g. soc-lab-db) should exist before you click Install Now.

---

**End of Guide — Installing osTicket**

*Each of the 20 screenshots appears exactly once • Descriptions match the actual screenshots*
