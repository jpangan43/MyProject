# Elasticsearch Installation on Vultr Cloud – SOC-ELK Server

**Complete Step-by-Step Visual Guide**  
From VPC creation to a running Elasticsearch 9.3.3 instance

| Field              | Value                              |
|--------------------|------------------------------------|
| **Server name**    | SOC-ELK                            |
| **Cloud provider** | Vultr                              |
| **OS**             | Ubuntu 22.04 LTS x64               |
| **Plan**           | 4 vCPU / 16 GB RAM / 80 GB NVMe    |
| **Elasticsearch**  | 9.3.3 (DEB package)                |
| **VPC**            | Day1-MYDFIR-SOC (172.31.0.0/24)    |

This guide walks you through creating a VPC, deploying an Ubuntu server, installing Elasticsearch, configuring the network, setting a firewall, and verifying the service.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Create VPC Network](#2-create-vpc-network)
3. [Configure VPC Name & Connectivity](#3-configure-vpc-name--connectivity)
4. [Select Location](#4-select-location)
5. [Set Custom IP Range](#5-set-custom-ip-range)
6. [Create the VPC](#6-create-the-vpc)
7. [Confirm VPC Created](#7-confirm-vpc-created)
8. [Deploy Server – Choose Type & Location](#8-deploy-server--choose-type--location)
9. [Select Server Plan](#9-select-server-plan)
10. [Choose Operating System (Ubuntu 22.04)](#10-choose-operating-system-ubuntu-2204)
11. [Set Hostname and Public IP](#11-set-hostname-and-public-ip)
12. [Attach VPC and Deploy](#12-attach-vpc-and-deploy)
13. [Server Ready – Copy IP & SSH](#13-server-ready--copy-ip--ssh)
14. [First Login as root](#14-first-login-as-root)
15. [Update the System](#15-update-the-system)
16. [Download Elasticsearch 9.3.3](#16-download-elasticsearch-933)
17. [Install the DEB Package](#17-install-the-deb-package)
18. [Note the elastic Superuser Password](#18-note-the-elastic-superuser-password)
19. [Explore Configuration Directory](#19-explore-configuration-directory)
20. [Identify Server IP Addresses](#20-identify-server-ip-addresses)
21. [Edit elasticsearch.yml (network.host)](#21-edit-elasticsearchyml-networkhost)
22–24. [Create & Assign Firewall Group](#22-24-create--assign-firewall-group)
25. [Enable and Start Elasticsearch Service](#25-enable-and-start-elasticsearch-service)
26. [Verify Elasticsearch is Running](#26-verify-elasticsearch-is-running)
27. [Final Server Overview & Next Steps](#27-final-server-overview--next-steps)

---

## 1. Prerequisites

Before you begin, ensure you have:

- A Vultr account with sufficient credit or payment method.
- Access to the Vultr Customer Portal ([my.vultr.com](https://my.vultr.com)).
- An SSH client (PowerShell, Terminal, PuTTY, etc.).
- Basic familiarity with Linux command line.

> **Note:** The screenshots show a lab named `Day1-MYDFIR-SOC`. You can use any naming convention that fits your environment.

---

## 2. Create VPC Network

1. Log in to the Vultr Customer Portal at [https://my.vultr.com](https://my.vultr.com).
2. In the left sidebar click **Products**, then expand **Network** and select **VPC Networks**.
3. Click the blue **Create VPC Network +** button.

---

## 3. Configure VPC Name & Connectivity

1. Enter a descriptive name, e.g. `Day1-MYDFIR-SOC`.
2. Choose **Instances with Public IP** (the free option). This allows the server to have a public IP while still belonging to the private VPC.

---

## 4. Select Location

Under **Location**, select the same region where you plan to deploy the server (here: **New York, US**).

Keeping the VPC and the instance in the same region is required for attachment.

---

## 5. Set Custom IP Range

1. Enable **Custom IP Range**.
2. Set **IPv4 Network Address** to `172.31.0.0` and **Network Prefix** to `24` (i.e. `172.31.0.0/24`).

This private subnet will be used by the SOC-ELK server.

---

## 6. Create the VPC

1. Review the summary (Name, Connectivity = Public IP, Location = New York).
2. Click **Create VPC Network +**.

---

## 7. Confirm VPC Created

You should now see the new VPC in the list with its UUID, location, connectivity type and subnet. Copy the UUID if you need it later; the name is usually enough for selection.

---

## 8. Deploy Server – Choose Type & Location

1. Click **Deploy +** (top right) or go to **Products → Compute**.
2. Select **Dedicated CPU**.
3. Under **Americas** choose **New York (NJ)** so it matches the VPC region.

---

## 9. Select Server Plan

1. In the **General Purpose** category select the plan `voc-g-4c-16gb-80s` (4 vCPUs, 16 GB RAM, 80 GB NVMe).
2. Leave **Automatic Backups** disabled for this lab (or enable them if desired).
3. Click **Configure**.

---

## 10. Choose Operating System (Ubuntu 22.04)

On the **Operating System** tab select **Ubuntu → 22.04 x64**.

This is a long-term support release well supported by Elasticsearch.

---

## 11. Set Hostname and Public IP

1. Set both **Hostname** and **Label** to `SOC-ELK`.
2. Keep **Instance(s) with Public IP** and enable **Public IPv4**.

---

## 12. Attach VPC and Deploy

1. Enable the **VPC Network** toggle and check the box for `Day1-MYDFIR-SOC`.
2. Review the summary (Ubuntu 22.04, 16 GB, Public IPv4, VPC attached).
3. Click **Deploy**. The instance will take a few minutes to finish provisioning.

---

## 13. Server Ready – Copy IP & SSH

Once the server shows as running, note the **public IP address** and the root password (or use SSH key if configured).

From your local machine open a terminal / PowerShell and connect:

```bash
ssh root@<PUBLIC-IP>
```

---

## 14. First Login as root

Accept the host key if prompted. You should land at the root prompt:

```text
root@SOC-ELK:~#
```

---

## 15. Update the System

Bring the system fully up to date before installing any software:

```bash
apt-get update && apt-get upgrade -y
```

Wait until the upgrade finishes (may take several minutes).

---

## 16. Download Elasticsearch 9.3.3

Download the official Debian package from Elastic's artifact repository:

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-9.3.3-amd64.deb
```

The package is approximately 635 MB.

---

## 17. Install the DEB Package

Install the downloaded package:

```bash
dpkg -i elasticsearch-9.3.3-amd64.deb
```

---

## 18. Note the elastic Superuser Password

During installation Elasticsearch generates a random password for the built-in **elastic** superuser.  
**Copy and store this password securely** – you will need it to access the cluster.

You can later reset it with:

```bash
/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```

The installer also prints the commands to enable and start the service (we will run them after configuration).

---

## 19. Explore Configuration Directory

Change into the configuration directory and list the files:

```bash
cd /etc/elasticsearch && ls
```

Key file: `elasticsearch.yml` – this is where we set network binding.

---

## 20. Identify Server IP Addresses

Run `ip a` (or `ip addr`) to see both the public interface and the private VPC address (example: `172.31.0.3`).

You will use one of these addresses for `network.host`.

```bash
ip a
```

---

## 21. Edit elasticsearch.yml (network.host)

Open the configuration file:

```bash
nano /etc/elasticsearch/elasticsearch.yml
```

Locate the **Network** section and set (replace with your actual IP or use `0.0.0.0` to listen on all interfaces):

```yaml
network.host: <SERVER-IP-OR-0.0.0.0>
http.port: 9200
```

Save and exit (`Ctrl+O`, `Enter`, `Ctrl+X` in nano).

---

## 22–24. Create & Assign Firewall Group

1. In the Vultr portal go to the server → **Settings → Firewall → Manage**.
2. Create a new Firewall Group (e.g. `MYDFIR-SOC`) and add inbound rules:
   - **SSH** (port 22) – Source: My IP (or Anywhere for lab use)
   - Optionally later: **TCP 9200** for Elasticsearch HTTP (restrict source carefully)
3. Assign the firewall group to the **SOC-ELK** instance.

---

## 25. Enable and Start Elasticsearch Service

Reload systemd, enable the service to start on boot, and start it now:

```bash
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
```

---

## 26. Verify Elasticsearch is Running

Check the service status:

```bash
systemctl status elasticsearch.service
```

You should see **Active: active (running)**. Elasticsearch is now listening on port 9200.

---

## 27. Final Server Overview & Next Steps

### Recommended next actions

- **Test connectivity:**
  ```bash
  curl -k -u elastic:<password> https://localhost:9200
  ```
  (or `http` if TLS is not yet required)

- Reset / change the elastic password if you did not save the generated one.
- Install Kibana on the same or another host and enroll it with an enrollment token.
- Configure index templates, ILM policies and any data-ingestion pipelines needed for your SOC use case.
- Restrict firewall rules so that port 9200 is only reachable from trusted sources (**never leave it open to 0.0.0.0/0 in production**).
- Consider enabling automatic backups or snapshots for the Elasticsearch data directory.

> **Security note:** The generated elastic password and any enrollment tokens are sensitive. Store them in a password manager and never commit them to source control.

---

**End of Guide — Elasticsearch Installation on Vultr (SOC-ELK)**

*Generated from configuration screenshots • For internal documentation / training use*
