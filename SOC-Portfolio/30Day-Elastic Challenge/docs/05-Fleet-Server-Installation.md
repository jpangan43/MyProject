# Fleet Server Installation

**Complete Step-by-Step Visual Guide**  
Add Fleet Server → Install on SOC-FLEET-SERVER → Confirm

| Field                | Value                          |
|----------------------|--------------------------------|
| **Fleet Server host**| SOC-FLEET-SERVER               |
| **Agent version**    | 9.3.3                          |
| **Fleet Server port**| 8220                           |
| **Elasticsearch**    | Already running on SOC-ELK     |
| **Method**           | Quick Start (self-signed cert for lab) |

Each of the 11 screenshots in this guide appears exactly once.

---

## Table of Contents

1. [Open Fleet in Kibana](#1-open-fleet-in-kibana)
2. [Add a Fleet Server](#2-add-a-fleet-server)
3. [Quick Start – set Fleet Server host](#3-quick-start--set-fleet-server-host)
4. [Fleet Server policy created](#4-fleet-server-policy-created)
5. [Select Linux x86_64 platform](#5-select-linux-x86_64-platform)
6. [Copy the install command](#6-copy-the-install-command)
7. [Update the Fleet Server host (optional)](#7-update-the-fleet-server-host-optional)
8. [Download and run the install command](#8-download-and-run-the-install-command)
9. [Fleet Server installed and enrolled](#9-fleet-server-installed-and-enrolled)
10. [Correct Fleet Server port in Settings (443 → 8220)](#10-correct-fleet-server-port-in-settings-443--8220)
11. [(Optional) Enroll a Windows agent against Fleet Server](#11-optional-enroll-a-windows-agent-against-fleet-server)
12. [Next Steps](#12-next-steps)

---

## 1. Open Fleet in Kibana

Log into Kibana.

Open the main menu → **Management → Fleet**.

---

## 2. Add a Fleet Server

On the Agents page you will see the prompt “Add a Fleet Server”.

Click the blue **Add Fleet Server** button.

---

## 3. Quick Start – set Fleet Server host

Keep the **Quick Start** tab selected (suitable for labs).

Confirm or set the Fleet Server host name / URL (example: SOC-FLEET-SERVER).

Click **Continue**.

---

## 4. Fleet Server policy created

Kibana automatically creates a Fleet Server policy and service token.

You will see the confirmation: **"Fleet Server policy created"**.

---

## 5. Select Linux x86_64 platform

In the install instructions open the platform selector.

Choose **Linux x86_64**.

---

## 6. Copy the install command

The full install command (including service token and Elasticsearch URL) is displayed.

Click the copy icon to copy it to the clipboard.

---

## 7. Update the Fleet Server host (optional)

SSH into the dedicated Fleet Server host (SOC-FLEET-SERVER).

It is good practice to update packages first:

```bash
apt-get update && apt-get upgrade -y
```

---

## 8. Download and run the install command

Paste and run the install command that was copied from Kibana.

The command downloads the Elastic Agent package, extracts it, and installs it with the Fleet Server flags (`--install-servers`, service token, etc.).

---

## 9. Fleet Server installed and enrolled

Wait until you see the success message:

**Done – Elastic Agent has been successfully installed.**

The Fleet Server is now running on port 8220.

---

## 10. Correct Fleet Server port in Settings (443 → 8220)

In Kibana go to **Fleet → Settings**.

Edit the Fleet Server host URL if it still shows port 443 and change it to **8220** (the port Fleet Server actually listens on).

Save the change.

---

## 11. (Optional) Enroll a Windows agent against Fleet Server

You can now enroll regular agents (Windows, Linux, etc.) against this Fleet Server.

The screenshot shows an example of installing an Elastic Agent on a Windows host using the enrollment token and pointing it at the Fleet Server URL on port 8220.

---

## 12. Next Steps

- Verify the Fleet Server appears as Healthy under **Fleet → Agents**.
- Create agent policies and enroll Linux / Windows hosts (see the Elastic Agent guides).
- Open port 8220 in the Vultr firewall (and host firewall) only from trusted networks.
- In production replace the self-signed certificate with a proper TLS certificate.
- Proceed with Sysmon, detection rules, and dashboards as needed for the lab.

> **Note:** Quick Start uses a self-signed certificate. Agents will need the `--insecure` flag (lab only) or you must distribute the CA certificate.

---

**End of Guide — Fleet Server Installation**

*Each of the 11 screenshots appears exactly once • For internal documentation / training use*
