# Elastic Agent Installation on Linux SSH Server

**Complete Step-by-Step Visual Guide**  
Create policy → Add agent → Install & enroll on SOC-SSH-Server

| Field             | Value                          |
|-------------------|--------------------------------|
| **Target host**   | SOC-SSH-Server (Linux)         |
| **Agent version** | 9.3.3                          |
| **Policy name**   | SOC-Linux-SSH-Server           |
| **Fleet Server**  | Already running (port 8220)    |
| **Platform**      | Linux x86_64                   |

Each screenshot in this guide appears only once. Follow the numbered steps in order.

---

## Table of Contents

1. [Open Fleet in Kibana](#1-open-fleet-in-kibana)
2. [Go to Agent policies](#2-go-to-agent-policies)
3. [Create agent policy (SOC-Linux-SSH-Server)](#3-create-agent-policy-soc-linux-ssh-server)
4. [Confirm new policy appears](#4-confirm-new-policy-appears)
5. [Open Agents tab and click Add agent](#5-open-agents-tab-and-click-add-agent)
6. [Select the Linux policy](#6-select-the-linux-policy)
7. [Choose Enroll in Fleet](#7-choose-enroll-in-fleet)
8. [Select Linux x86_64 platform](#8-select-linux-x86_64-platform)
9. [Copy the install command](#9-copy-the-install-command)
10. [Run the install command on the Linux host](#10-run-the-install-command-on-the-linux-host)
11. [Confirm successful installation & enrollment](#11-confirm-successful-installation--enrollment)
12. [Enrollment and data confirmed in Kibana](#12-enrollment-and-data-confirmed-in-kibana)
13. [Verify agent is Healthy in Fleet](#13-verify-agent-is-healthy-in-fleet)
14. [Next Steps](#14-next-steps)

---

## 1. Open Fleet in Kibana

Log into Kibana with the elastic user.

Open the main menu (hamburger icon) → **Management → Fleet**.

---

## 2. Go to Agent policies

Click the **Agent policies** tab.

Existing policies (SOC-Win-2025, Fleet Server Policy) are listed.

Click the blue **+ Create agent policy** button.

---

## 3. Create agent policy (SOC-Linux-SSH-Server)

Enter the policy name: `SOC-Linux-SSH-Server`.

Leave **"Collect system logs and metrics"** checked (recommended).

Click **Create agent policy**.

---

## 4. Confirm new policy appears

The new policy **SOC-Linux-SSH-Server** (rev. 1) now appears in the Agent policies list.

---

## 5. Open Agents tab and click Add agent

Switch to the **Agents** tab.

Click the blue **Add agent** button on the right.

---

## 6. Select the Linux policy

In the "What type of host..." dropdown select **SOC-Linux-SSH-Server**.

---

## 7. Choose Enroll in Fleet

Under “Enroll in Fleet?” keep the default option **Enroll in Fleet (recommended)** selected.

This allows central management and automatic updates via Fleet.

---

## 8. Select Linux x86_64 platform

In the Install Elastic Agent section open the platform dropdown.

Select **Linux x86_64**.

---

## 9. Copy the install command

Kibana shows a ready-to-run command that includes the Fleet Server URL and enrollment token.

Click the copy icon to copy the full command to the clipboard.

---

## 10. Run the install command on the Linux host

SSH into the Linux host (SOC-SSH-Server) as root.

Paste and run the command. The example uses the `--insecure` flag because the Fleet Server is using a self-signed certificate.

The command downloads the agent, extracts it, and starts the installation + enrollment.

```bash
curl -L -O https://artifacts.elastic.co/downloads/beats/elastic-agent/...tar.gz
tar xzvf elastic-agent-...-linux-x86_64.tar.gz
cd elastic-agent-...
sudo ./elastic-agent install --url=https://...:8220 --enrollment-token=... --insecure
```

---

## 11. Confirm successful installation & enrollment

The installer confirms that the service started and the agent enrolled successfully.

Look for the message: **Done – Elastic Agent has been successfully installed.**

---

## 12. Enrollment and data confirmed in Kibana

Back in the Kibana Add agent wizard you should see two green check marks:

- Agent enrollment confirmed
- Incoming data confirmed

---

## 13. Verify agent is Healthy in Fleet

Go to **Fleet → Agents**.

Confirm the new host **SOC-SSH-Server** is listed with status **Healthy** and is assigned to the **SOC-Linux-SSH-Server** policy.

---

## 14. Next Steps

- Verify data is arriving in Discover / Dashboards (filter by `agent.name : "SOC-SSH-Server"`).
- Add more integrations to the SOC-Linux-SSH-Server policy if needed (Auditd, custom logs, etc.).
- Repeat the process for additional Linux hosts using the same policy.
- Continue with Windows agents, Sysmon, or detection-rule creation as required by your lab.

> **Note:** The `--insecure` flag disables TLS certificate verification and should only be used in lab environments. In production, configure proper certificates for the Fleet Server.

---

**End of Guide — Elastic Agent on Linux SSH Server**

*Each of the 13 screenshots appears exactly once • For internal documentation / training use*
