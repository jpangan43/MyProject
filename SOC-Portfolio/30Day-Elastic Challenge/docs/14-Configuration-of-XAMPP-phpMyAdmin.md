# Configuration of XAMPP – phpMyAdmin

**Complete Step-by-Step Visual Guide**

properties.ini · config.inc.php · Firewall · root@IP privileges

| Field | Value |
|-------|-------|
| **Stack** | XAMPP on Windows (Apache + MySQL + phpMyAdmin) |
| **Goal** | Allow remote access to phpMyAdmin / MySQL by host IP |
| **Key files** | C:\xampp\xampp-control.ini (properties) · config.inc.php |
| **Firewall** | Inbound TCP 80, 443 |
| **MySQL user** | root@<server-IP> with password |

Each of the 17 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Open xampp properties (configuration) file
2. Set apache_domainname to the server IP
3. Open the phpMyAdmin folder
4. Copy config.inc.php
5. Paste a backup / working copy of config.inc.php
6. Edit config.inc.php – set $cfg['Servers'][$i]['host']
7. Open Windows Defender Firewall with Advanced Security
8. Create new Inbound Rule → Port
9. Specify TCP ports 80, 443
10. Allow the connection
11. Apply to Domain / Private / Public
12. Name the rule and Finish
13. Start Apache & MySQL in XAMPP Control Panel
14. phpMyAdmin → User accounts → root@localhost
15. Edit privileges → Login Information
16. Change Host name to the server IP
17. Set password and Go
18. Next steps

---

## 1. Open xampp properties (configuration) file

Open File Explorer and go to `C:\xampp`.

Locate the file named **properties** (Configuration settings) and open it with Notepad.

**Figure 1** – C:\xampp → properties (Configuration settings) selected

---

## 2. Set `apache_domainname` to the server IP

In the `[Apache]` section find `apache_domainname`.

Set it to the machine’s IP address (example shows a value ending in 248).

Save the file.

**Figure 2** – properties file: `apache_domainname` set to the host IP (...248)

---

## 3. Open the phpMyAdmin folder

Still under `C:\xampp`, open the **phpMyAdmin** folder.

**Figure 3** – C:\xampp → phpMyAdmin folder selected

---

## 4. Copy config.inc.php

In the phpMyAdmin folder locate `config.inc.php`.

Right-click it and choose **Copy** (create a backup before editing).

**Figure 4** – Right-click config.inc.php → Copy

---

## 5. Paste a backup / working copy of config.inc.php

Right-click in an empty area of the same folder and choose **Paste** so you have a backup copy (or ensure config.inc.php is present and editable).

**Figure 5** – Right-click in folder → Paste

---

## 6. Edit config.inc.php – set host

Open `config.inc.php` in Notepad.

Locate the Servers configuration block and set:

```php
$cfg['Servers'][$i]['host'] = '<your-server-IP>';
```

(example shows a value ending in ...18).

Also note `auth_type`, `user`, `password`, `AllowNoPassword` as needed for your lab.

Save the file.

**Figure 6** – config.inc.php in Notepad: $cfg['Servers'][$i]['host'] set to the IP

---

## 7. Open Windows Defender Firewall with Advanced Security

Open Windows Settings / Search and launch **Windows Defender Firewall with Advanced Security**.

**Figure 7** – Search → Windows Defender Firewall with Advanced Security

---

## 8. Create new Inbound Rule → Port

Select **Inbound Rules** on the left.

Click **New Rule...** on the right.

Choose **Port** and click **Next**.

**Figure 8** – Inbound Rules → New Rule... → Rule Type: Port → Next

---

## 9. Specify TCP ports 80, 443

Select **TCP**.

Choose **Specific local ports** and enter `80, 443`.

Click **Next**.

**Figure 9** – Protocol and Ports: TCP, Specific local ports: 80, 443 → Next

---

## 10. Allow the connection

Select **Allow the connection** and click **Next**.

**Figure 10** – Action: Allow the connection → Next

---

## 11. Apply to Domain / Private / Public

Leave Domain, Private, and Public checked (or restrict as appropriate for the lab).

Click **Next**.

**Figure 11** – Profile: Domain, Private, Public checked → Next

---

## 12. Name the rule and Finish

Name the rule e.g. **Inbound 80, 443**.

Click **Finish**.

**Figure 12** – Name: Inbound 80, 443 → Finish

---

## 13. Start Apache & MySQL in XAMPP Control Panel

Open the **XAMPP Control Panel**.

Start **Apache** and **MySQL** (both should show green / running).

Click **Admin** next to Apache to open the default page / phpMyAdmin.

**Figure 13** – XAMPP Control Panel: Apache and MySQL running; Admin button for Apache

---

## 14. phpMyAdmin → User accounts → root@localhost

In phpMyAdmin go to the **User accounts** tab.

Locate the **root** account with Host name **localhost**.

**Figure 14** – phpMyAdmin User accounts overview; root@localhost selected

---

## 15. Edit privileges → Login Information

Click **Edit privileges** for root@localhost.

Open the **Login Information** section.

**Figure 15** – Edit privileges for root@localhost → Login Information tab

---

## 16. Change Host name to the server IP

Change **Host name** from localhost to the server’s IP (example: 66.135.4.248). This allows root to connect from that host address.

**Figure 16** – Host name set to 66.135.4.248 (example IP)

---

## 17. Set password and Go

Set a strong **Password** (and re-type it).

Choose to keep the old account (or as preferred).

Click **Go** to apply the changes.

**Figure 17** – Host name = IP, Password set, keep old account → Go

---

## 18. Next Steps

- Verify you can reach phpMyAdmin via `http://<server-IP>/phpmyadmin` from another lab host.
- Update any application config (e.g. osTicket) to use the new root password / host if required.
- Restrict firewall rules to trusted lab subnets rather than Public if possible.
- Do not expose phpMyAdmin to the public internet without additional hardening (VPN, IP allow-list, strong auth).

> **Security note**: Allowing root@IP and opening ports 80/443 increases exposure. Use only in isolated lab environments.

---

**End of Guide — Configuration of XAMPP – phpMyAdmin**

*Each of the 17 screenshots appears exactly once • Descriptions match the actual screenshots*
