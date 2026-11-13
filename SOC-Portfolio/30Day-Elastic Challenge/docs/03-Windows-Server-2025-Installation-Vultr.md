# Windows Server 2025 Installation on Vultr Cloud

**Complete Step-by-Step Visual Guide**  
Deploy a Windows Server 2025 Standard instance for the SOC lab

| Field               | Value                                      |
|---------------------|--------------------------------------------|
| **Server hostname** | MYDFIR-WIN-jasonlee                        |
| **Operating System**| Windows Server 2025 Standard x64           |
| **Plan**            | Shared CPU – vc2-1c-2gb (1 vCPU / 2 GB RAM / 55 GB SSD) |
| **Location**        | New York (NJ), United States               |
| **Cloud provider**  | Vultr                                      |
| **Purpose**         | Windows endpoint for Sysmon, Elastic Agent, and SOC lab activities |

This guide walks through deploying a fresh Windows Server 2025 instance on Vultr. The resulting server is used later for Sysmon installation, Elastic Agent enrollment, and detection testing.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Deploy a New Server](#2-deploy-a-new-server)
3. [Choose Server Type & Location](#3-choose-server-type--location)
4. [Select the Compute Plan](#4-select-the-compute-plan)
5. [Select Windows Server 2025](#5-select-windows-server-2025)
6. [Configure Hostname, Public IP & Deploy](#6-configure-hostname-public-ip--deploy)
7. [Server Ready – Overview Page](#7-server-ready--overview-page)
8. [Next Steps & Recommendations](#8-next-steps--recommendations)

---

## 1. Prerequisites

Before starting you need:

- An active Vultr account with a payment method configured.
- Access to the Vultr Customer Portal (https://my.vultr.com).
- Basic familiarity with cloud server deployment.

This Windows Server will sit alongside the existing SOC-ELK (Ubuntu) instance and will later receive Sysmon and an Elastic Agent.

---

## 2. Deploy a New Server

1. Log in to the Vultr portal.
2. In the left sidebar go to **Products → Compute** (or click the blue **Deploy +** button in the top-right).
3. From the dropdown choose **Deploy New Server**.

---

## 3. Choose Server Type & Location

1. Under **Choose Type** select **Shared CPU** (sufficient and cost-effective for lab use).
2. In the location list click **All Locations** if needed, then choose **New York (NJ), US**.

Choosing the same region as the SOC-ELK server keeps latency low for agent communication.

---

## 4. Select the Compute Plan

1. In the plan list select **vc2-1c-2gb**:
   - 1 vCPU
   - 2 GB RAM
   - 55 GB SSD
   - 2 TB bandwidth / month
2. Leave **Automatic Backups** disabled for the lab (or enable them if you prefer).
3. Click the blue **Configure** button at the bottom right.

---

## 5. Select Windows Server 2025

1. On the **Operating System** tab locate the Windows section.
2. Select **Windows Standard** and choose version **2025 x64**.

This is the full graphical (GUI) edition of Windows Server 2025, suitable for RDP access and installing desktop tools such as Sysmon.

---

## 6. Configure Hostname, Public IP & Deploy

1. Set **Server Hostname** and **Label** to `MYDFIR-WIN-jasonlee` (or any name you prefer).
2. Under **Instance Connectivity** keep **Instance(s) with Public IP** selected.
3. Ensure **Public IPv4** is enabled.
4. Review the Deploy Summary on the right side.
5. Click the blue **Deploy** button.

Vultr will provision the instance; this usually takes a few minutes.

---

## 7. Server Ready – Overview Page

Once provisioning finishes you will see the server overview page.

Key information shown:

- Public IP address (needed for RDP)
- Username: **Administrator**
- Password (click the eye / copy icon – store it securely; it is shown only once)
- OS: Windows 2025 Standard
- Specs: 1 vCPU, 2048 MB RAM, 55 GB SSD

You can now connect via Remote Desktop (port 3389) using the Administrator account and the password from the portal.

---

## 8. Next Steps & Recommendations

After the server is running, complete the following:

- Connect via RDP and finish any initial Windows setup prompts.
- Install the latest Windows updates.
- Install Sysmon with a good configuration (see the Sysmon Setup guide).
- Install and enroll an Elastic Agent into Fleet (see the Elastic Agent / Fleet guides).
- Configure the Vultr Firewall Group and Windows Firewall to allow only required ports (RDP, agent communication, etc.).
- Optionally enable Automatic Backups or take a snapshot once the baseline configuration is complete.

> **Security note:** The Administrator password is displayed only once in the Vultr portal. Copy it immediately and store it in a password manager. Do not leave RDP open to the entire internet in a production environment.

---

**End of Guide — Windows Server 2025 Installation on Vultr**

*Generated from configuration screenshots • For internal documentation / training use*
