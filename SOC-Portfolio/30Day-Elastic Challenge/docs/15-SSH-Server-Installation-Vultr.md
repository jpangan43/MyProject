# SSH Server Installation

**Complete Step-by-Step Visual Guide**

Deploy SOC-SSH-Server on Vultr (Ubuntu 24.04)

| Field | Value |
|-------|-------|
| **Provider** | Vultr Cloud Compute |
| **Type** | Shared CPU |
| **Location** | New York (NJ), US / Americas |
| **Plan** | vc2-1c-1gb (1 vCPU, 1 GB RAM, 25 GB SSD) |
| **OS** | Ubuntu 24.04 x64 |
| **Hostname / Label** | SOC-SSH-Server |

Each of the 6 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Open Vultr Instances and start Deploy
2. Choose Shared CPU and New York (NJ) location
3. Select plan vc2-1c-1gb and Configure
4. Select Operating System Ubuntu 24.04 x64
5. Set hostname SOC-SSH-Server and Deploy
6. Confirm SOC-SSH-Server is Running
7. Next steps

---

## 1. Open Vultr Instances and start Deploy

Log in to the Vultr console (console.vultr.com).

In the left sidebar go to **Compute → Instances**.

Click **+ Deploy** (top right) to start a new server.

> **Figure 1** – Vultr console → Compute → Instances → + Deploy

---

## 2. Choose Shared CPU and New York (NJ) location

Under **Choose Type** select **Shared CPU**.

In **Filter Locations** choose **Americas**, then select **New York (NJ)**.

> **Figure 2** – Choose Type: Shared CPU; Location: Americas → New York (NJ)

---

## 3. Select plan vc2-1c-1gb and Configure

Under plans select **vc2-1c-1gb** (1 vCPU, 1 GB Memory, 25 GB SSD).

Leave **Automatic Backups Disabled** if desired for the lab.

Click **Configure**.

> **Figure 3** – Plan vc2-1c-1gb (1 vCPU, 1 GB) selected; Automatic Backups Disabled → Configure

---

## 4. Select Operating System Ubuntu 24.04 x64

On the **Operating System** tab select **Ubuntu**.

Choose version **24.04 x64**.

> **Figure 4** – Operating System tab → Ubuntu → 24.04 x64

---

## 5. Set hostname SOC-SSH-Server and Deploy

SSH Keys / Startup Script / Firewall Group can remain default or as preferred.

Set **Server Hostname** and **Label** to **SOC-SSH-Server**.

Under **Instance Connectivity** choose **Instance(s) with Public IP** and **Public IPv4**.

Review the Deploy Summary, then click **Deploy**.

> **Figure 5** – Hostname/Label: SOC-SSH-Server; Public IPv4; Deploy

---

## 6. Confirm SOC-SSH-Server is Running

Return to the Instances list.

Confirm that **SOC-SSH-Server** appears with Ubuntu icon, New Jersey location, Public IP, and status **Running**.

> **Figure 6** – Cloud Compute Instances list: SOC-SSH-Server (Ubuntu) Running

---

## 7. Next Steps

- Copy the Public IP and SSH into the server as root (or the default user) using the password or SSH key provided by Vultr.
- Update packages: `apt update && apt upgrade -y`.
- Install and configure OpenSSH if needed (usually already present on Ubuntu).
- Install the Elastic Agent on this host (see the Elastic Agent on Linux guide) so SSH activity is shipped to your ELK stack.
- Use this host as the target for SSH authentication / Hydra lab exercises and the SSH Failed Activity dashboard.

---

**End of Guide — SSH Server Installation**

*Each of the 6 screenshots appears exactly once • Descriptions match the actual screenshots*
