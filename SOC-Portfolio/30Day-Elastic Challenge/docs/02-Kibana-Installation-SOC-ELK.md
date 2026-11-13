# Kibana Installation on SOC-ELK (Elasticsearch 9.3.3)

**Complete Step-by-Step Visual Guide**  
Install, enroll, secure and verify Kibana 9.3.3

| Field                  | Value                                      |
|------------------------|--------------------------------------------|
| **Server**             | SOC-ELK (Ubuntu 22.04 on Vultr)            |
| **Elasticsearch**      | 9.3.3 already installed and running        |
| **Kibana version**     | 9.3.3 (DEB package)                        |
| **Port**               | 5601 (HTTP)                                |
| **Key features covered** | Enrollment token, verification code, encryption keys |

This guide continues from the Elasticsearch installation on the same SOC-ELK server. It covers downloading Kibana, installing it, enrolling with Elasticsearch, fixing encryption keys, and verifying the Security Alerts page.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Download Kibana DEB package](#2-download-kibana-deb-package)
3. [Copy the download link](#3-copy-the-download-link)
4. [Download Kibana 9.3.3 on the server](#4-download-kibana-933-on-the-server)
5. [Install the Kibana package](#5-install-the-kibana-package)
6. [Edit kibana.yml (optional network settings)](#6-edit-kibanayml-optional-network-settings)
7. [Enable and start the Kibana service](#7-enable-and-start-the-kibana-service)
8. [Generate an enrollment token for Kibana](#8-generate-an-enrollment-token-for-kibana)
9. [Open firewall port 5601 (Vultr + UFW)](#9-open-firewall-port-5601-vultr--ufw)
10. [Access Kibana and paste the enrollment token](#10-access-kibana-and-paste-the-enrollment-token)
11. [Generate the verification code](#11-generate-the-verification-code)
12. [Enter the verification code in the browser](#12-enter-the-verification-code-in-the-browser)
13. [Log in with the elastic user](#13-log-in-with-the-elastic-user)
14. [Security Alerts – encryption key error](#14-security-alerts--encryption-key-error)
15. [Generate encryption keys](#15-generate-encryption-keys)
16. [Add keys to the Kibana keystore & restart](#16-add-keys-to-the-kibana-keystore--restart)
17. [Verify – Security Alerts page works](#17-verify--security-alerts-page-works)
18. [Next Steps & Recommendations](#18-next-steps--recommendations)

---

## 1. Prerequisites

Before starting this guide you should already have:

- The SOC-ELK server running Ubuntu 22.04 on Vultr.
- Elasticsearch 9.3.3 installed, configured and running (see the previous Elasticsearch guide).
- SSH access as root (or a user with sudo).
- The elastic superuser password that was generated during Elasticsearch installation.
- Port 22 open in the Vultr firewall (SSH).

> **Note:** Kibana and Elasticsearch versions should match (both 9.3.3 in this guide).

---

## 2. Download Kibana DEB package

1. On your local machine open a browser and go to [https://www.elastic.co/downloads/kibana](https://www.elastic.co/downloads/kibana).
2. Under **“Download and unzip Kibana”** open the platform dropdown and select **DEB x86_64**.

---

## 3. Copy the download link

Right-click the blue **DEB x86_64** button and choose **Copy link address**.

You will paste this URL into the server’s terminal in the next step.

---

## 4. Download Kibana 9.3.3 on the server

SSH into the SOC-ELK server and run (replace the URL with the one you copied if the version differs):

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-9.3.3-amd64.deb
```

The package is approximately 359 MB.

---

## 5. Install the Kibana package

Install the downloaded package:

```bash
dpkg -i kibana-9.3.3-amd64.deb
```

The installer creates the kibana user/group and the keystore under `/etc/kibana/`.

---

## 6. Edit kibana.yml (optional network settings)

Open the configuration file if you need to change the server host or port:

```bash
nano /etc/kibana/kibana.yml
```

Common settings (uncomment and adjust if required):

```yaml
server.port: 5601
server.host: "0.0.0.0"
```

Save and exit when finished.

---

## 7. Enable and start the Kibana service

Reload systemd, enable Kibana on boot and start it:

```bash
systemctl daemon-reload
systemctl enable kibana.service
systemctl start kibana.service
systemctl status kibana.service
```

Confirm the status shows **Active: active (running)**.

---

## 8. Generate an enrollment token for Kibana

On the Elasticsearch node generate a one-time enrollment token:

```bash
cd /usr/share/elasticsearch/bin
./elasticsearch-create-enrollment-token --scope kibana
```

Copy the long token string that is printed – you will paste it into the Kibana browser UI.

---

## 9. Open firewall port 5601 (Vultr + UFW)

1. In the Vultr portal open the firewall group attached to SOC-ELK and add an inbound rule that allows TCP traffic (or specifically port 5601) from your public IP.
2. Also open the port on the local Ubuntu firewall:

```bash
ufw allow 5601
```

---

## 10. Access Kibana and paste the enrollment token

1. Open a browser and navigate to `http://<PUBLIC-IP>:5601`.
2. Paste the enrollment token generated earlier into the text box and click **Configure Elastic**.

---

## 11. Generate the verification code

On the server run:

```bash
cd /usr/share/kibana/bin
./kibana-verification-code
```

A 6-digit code is displayed (example: `194 842`). Keep this terminal open.

---

## 12. Enter the verification code in the browser

Back in the browser enter the 6-digit verification code and click **Verify**.

---

## 13. Log in with the elastic user

You are redirected to the login screen.

- **Username:** `elastic`
- **Password:** the password that was generated when you installed Elasticsearch.

Click **Log in**.

---

## 14. Security Alerts – encryption key error

After login you may see errors on the **Security → Alerts** page:

- Failed to retrieve detection engine privileges
- Failed to bootstrap prebuilt rules

Both point to a missing `xpack.encryptedSavedObjects.encryptionKey`.

This is expected on a fresh install and is fixed in the next steps.

---

## 15. Generate encryption keys

Generate the three required encryption keys:

```bash
cd /usr/share/kibana/bin
./kibana-encryption-keys generate
```

Copy the three values that are printed (`encryptedSavedObjects`, `reporting`, `security`).

---

## 16. Add keys to the Kibana keystore & restart

Store each key securely in the Kibana keystore:

```bash
./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
./kibana-keystore add xpack.reporting.encryptionKey
./kibana-keystore add xpack.security.encryptionKey

systemctl restart kibana.service
```

Paste each generated value when prompted, then restart the service.

---

## 17. Verify – Security Alerts page works

1. Refresh the browser (or log in again).
2. Navigate to **Security → Alerts**.

The previous errors should be gone and the Alerts page should load normally (even if no alerts exist yet).

---

## 18. Next Steps & Recommendations

Recommended actions after a successful Kibana installation:

- Create additional users and roles instead of using the elastic superuser for daily work.
- Install Fleet / Elastic Agent or other integrations to start ingesting data.
- Configure index patterns / data views for your SOC data sources.
- Enable TLS for Kibana (`server.ssl.*`) and terminate HTTPS at a reverse proxy or load balancer if exposed publicly.
- Restrict the Vultr firewall so that port 5601 is only reachable from trusted IPs.
- Take a snapshot of the server or enable automatic backups now that the stack is healthy.
- Continue building the rest of your SOC stack (Logstash, Beats, detection rules, dashboards, etc.).

> **Security note:** The elastic password, enrollment tokens and encryption keys are sensitive. Store them in a password manager and never commit them to source control or share them in clear text.

---

**End of Guide — Kibana Installation on SOC-ELK**

*Generated from configuration screenshots • For internal documentation / training use*
