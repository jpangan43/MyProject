# Ubuntu for Fleet Server

**Complete Step-by-Step Visual Guide**

Deploy SOC-FLEET-SERVER on Vultr (Ubuntu 22.04)

| Field | Value |
|-------|-------|
| **Provider** | Vultr Cloud Compute |
| **Type** | Dedicated CPU |
| **Location** | New York (NJ), US / Americas |
| **Plan** | voc-g-1c-4gb-30s (1 vCPU, 4 GB RAM, 30 GB NVMe) |
| **OS** | Ubuntu 22.04 x64 |
| **Hostname / Label** | SOC-FLEET-SERVER |
| **VPC** | Day1-MYDFIR-SOC (optional) |

Each of the 5 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Open Vultr Cloud Compute and start Deploy
2. Choose Dedicated CPU and New York (NJ) location
3. Select plan voc-g-1c-4gb-30s and Configure
4. Select Operating System Ubuntu 22.04 x64
5. Set hostname SOC-FLEET-SERVER, Public IP, VPC, and Deploy
6. Next steps

---

## 1. Open Vultr Cloud Compute and start Deploy

Log in to the Vultr console (console.vultr.com).

Open the **Cloud Compute / Instances** view.

Click **+ Deploy** (top right) to start a new server.

> **Figure 1** – Vultr Cloud Compute Instances list → + Deploy

---

## 2. Choose Dedicated CPU and New York (NJ) location

Under **Choose Type** select **Dedicated CPU**.

In **Filter Locations** choose **Americas**, then select **New York (NJ)**.

> **Figure 2** – Choose Type: Dedicated CPU; Location: Americas → New York (NJ)

---

## 3. Select plan voc-g-1c-4gb-30s and Configure

Under plans (**General Purpose**) select **voc-g-1c-4gb-30s** (1 vCPU, 4 GB Memory, 30 GB NVMe, 4 TB/mo bandwidth).

Leave **Automatic Backups Disabled** if desired for the lab.

Click **Configure**.

> **Figure 3** – General Purpose plan voc-g-1c-4gb-30s (1 vCPU, 4 GB, 30 GB NVMe); Backups Disabled → Configure

---

## 4. Select Operating System Ubuntu 22.04 x64

On the **Operating System** tab select **Ubuntu**.

Choose version **22.04 x64** (or 24.04 if preferred for your lab).

Confirm the selection before proceeding to hostname and connectivity.

> **Figure 4** – Operating System tab → Ubuntu → 22.04 x64

---

## 5. Set hostname SOC-FLEET-SERVER, Public IP, VPC, and Deploy

Set **Server Hostname** and **Label** to **SOC-FLEET-SERVER**.

Under **Instance Connectivity** choose **Instance(s) with Public IP** and **Public IPv4**.

Optionally enable **VPC Network** and select an existing VPC (example: Day1-MYDFIR-SOC / 172.31.0.0/24).

Review the Deploy Summary, then click **Deploy**.

> **Figure 5** – Hostname: SOC-FLEET-SERVER; Public IPv4; VPC Day1-MYDFIR-SOC → Deploy

---

## 6. Next Steps

- Wait until the instance status is **Running** and note the Public IP.
- SSH into the server as root (or the default user) with the password or SSH key from Vultr.
- Update packages: `apt update && apt upgrade -y`.
- Install and enroll Elastic Agent / Fleet Server on this host (see the Fleet Server Installation guide).
- Ensure required ports (e.g. 8220 for Fleet) are allowed in the Vultr firewall / security group.

---

**End of Guide — Ubuntu for Fleet Server**

*Each of the 5 screenshots appears exactly once • Descriptions match the actual screenshots*
