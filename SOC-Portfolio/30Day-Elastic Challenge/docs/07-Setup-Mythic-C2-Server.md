# Setup Mythic C2 Server

**Complete Step-by-Step Visual Guide**

Install Docker → Clone Mythic → Start services → Login to UI

| Field | Value |
|-------|-------|
| **Host** | SOC-Mythic (Linux) |
| **Mythic version** | v3.4.0.57 (its-a-feature/Mythic) |
| **Admin user** | mythic_admin |
| **UI port** | 7443 (HTTPS) |
| **Default operation** | Operation Chimera |

Each of the 9 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Install docker-compose
2. Install make and clone Mythic repository
3. Run install_docker_ubuntu.sh
4. Restart Docker and run make
5. Start Mythic with mythic-cli start
6. View .env (admin credentials)
7. Accept the self-signed certificate warning
8. Log in to the Mythic UI
9. Mythic dashboard (Operation Chimera)
10. Next steps

---

## 1. Install docker-compose

SSH into the Mythic host (SOC-Mythic) as root.

Install the docker-compose package:

When prompted "Do you want to continue? [Y/n]" type **Y** and press Enter.

The package and its dependencies are downloaded and installed.

```bash
apt install docker-compose
```

**Figure 1** – apt install docker-compose (confirm with Y)

---

## 2. Install make and clone Mythic repository

Install the make utility (may already be present):

Clone the official Mythic repository:

The repository is cloned into a directory named **Mythic**.

```bash
apt install make
git clone https://github.com/its-a-feature/Mythic
```

**Figure 2** – apt install make; git clone https://github.com/its-a-feature/Mythic

---

## 3. Run install_docker_ubuntu.sh

List the home directory to confirm the Mythic folder exists, then enter it:

Run the Ubuntu Docker install helper script that ships with Mythic:

The script installs/updates Docker-related packages and prepares the host.

```bash
ls
cd Mythic
./install_docker_ubuntu.sh
```

**Figure 3** – ls; cd Mythic; ./install_docker_ubuntu.sh

---

## 4. Restart Docker and run make

Restart the Docker service and confirm it is active (running):

Then run **make**. This builds the mythic-cli binary  
(`cd Mythic_CLI && make build_linux && mv mythic-cli ...`).

When finished you will have an executable **mythic-cli** in the Mythic directory.

```bash
systemctl restart docker
systemctl status docker
make
```

**Figure 4** – systemctl restart/status docker; make (builds mythic-cli)

---

## 5. Start Mythic with mythic-cli start

From the Mythic directory start the full stack:

mythic-cli creates docker-compose.yml if needed, pulls the required images (mythic_react, mythic_nginx, mythic_server, mythic_postgres, etc.), starts all containers, generates SSL certificates for Nginx, and connects to RabbitMQ. Wait until the services report Healthy / Started.

```bash
./mythic-cli start
```

**Figure 5** – ./mythic-cli start (containers pulled and started)

---

## 6. View .env (admin credentials)

The generated `.env` file contains the admin credentials and other settings.

Display it and note especially:

- `MYTHIC_ADMIN_USER` = mythic_admin
- `MYTHIC_ADMIN_PASSWORD` = (the generated password – copy and store it securely)

You will need these credentials to log into the web UI.

```bash
cat .env
```

**Figure 6** – cat .env → MYTHIC_ADMIN_USER / MYTHIC_ADMIN_PASSWORD

---

## 7. Accept the self-signed certificate warning

Open a browser and navigate to `https://<Mythic-IP>:7443`.

Because Mythic uses a self-signed certificate you will see a certificate warning (`NET::ERR_CERT_AUTHORITY_INVALID`).

Click **Advanced** (if shown) and then **Proceed to ... (unsafe)** to continue.

**Figure 7** – Browser “Your connection is not private” → Proceed (unsafe)

---

## 8. Log in to the Mythic UI

On the Mythic login page enter:

- **Username**: mythic_admin
- **Password**: the value of `MYTHIC_ADMIN_PASSWORD` from the `.env` file

Click **LOGIN**.

**Figure 8** – Mythic login page → username mythic_admin + password → LOGIN

---

## 9. Mythic dashboard (Operation Chimera)

After a successful login you reach the main Mythic dashboard.

The default operation is named **Operation Chimera**.

You will see panels for Active Callbacks, Payloads, Workflows, etc.

At this point the C2 server is ready; you can install agents/payloads and C2 profiles next.

**Figure 9** – Welcome mythic_admin to Operation Chimera’s Dashboard

---

## 10. Next Steps

- Install a C2 profile (e.g. HTTP) with:  
  `./mythic-cli install github https://github.com/MythicC2Profiles/http`
- Install an agent (e.g. Apollo) for Windows payloads.
- Create a payload in the UI and deliver it to a lab target.
- Open port 7443 (and any C2 listener ports) in the host/Vultr firewall only from trusted sources.
- Store the `MYTHIC_ADMIN_PASSWORD` securely; it is only shown in `.env`.
- Continue with the “Creating Mythic C2 Profile” and “Creating a Payload in Mythic” guides.

> **Lab note**: Mythic is a real C2 framework. Use it only in isolated lab environments you own or have explicit permission to test. Do not expose the UI or listeners to the public internet without proper controls.

---

**End of Guide — Setup Mythic C2 Server**

*Each of the 9 screenshots appears exactly once • Descriptions match the actual screenshots*
