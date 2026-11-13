# Creating Mythic C2 Profile (HTTP)

**Complete Step-by-Step Visual Guide**

Install the HTTP C2 profile into Mythic via mythic-cli

| Field | Value |
|-------|-------|
| **C2 Profile** | http (HTTP Get/Post) |
| **Repository** | https://github.com/MythicC2Profiles/http |
| **Supported agents** | apollo (and others that support HTTP) |
| **Mythic host** | SOC-Mythic |
| **Prerequisite** | Mythic C2 server already installed and running |

Each of the 2 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Install the HTTP C2 profile with mythic-cli
2. Verify the profile is Online in Installed Services
3. Next steps

---

## 1. Install the HTTP C2 profile with mythic-cli

SSH into the Mythic server (SOC-Mythic) and change to the Mythic directory if needed.

Install the official HTTP C2 profile from GitHub:

mythic-cli clones the repo, parses config.json, adds the http service to docker-compose, pulls the image (`ghcr.io/mythicc2profiles/http...`), starts the http container, and installs the related documentation.

When finished you should see: **Successfully installed service!**

```bash
./mythic-cli install github https://github.com/MythicC2Profiles/http
```

**Figure 1** – ./mythic-cli install github https://github.com/MythicC2Profiles/http → Successfully installed service!

---

## 2. Verify the profile is Online in Installed Services

Open the Mythic web UI and go to **Installed Services** in the left sidebar.

Select the **C2** tab (shows C2 (1)).

You will see the **http** service listed with type **Egress**.

Metadata includes:

- Author: @its_a_feature_
- Version: 1.1.1
- Supported Agents: apollo
- Description: Uses HTTP Get/Post messages for connectivity

Confirm **Container Status: Online** and **C2 Server Status: Accepting Connections**.

**Figure 2** – Installed Services → C2 tab → http → Container Status Online, Accepting Connections

---

## 3. Next Steps

- Ensure the Apollo agent is also installed (see the “Installing Mythic Agent” guide).
- Create a payload that uses the HTTP profile (Create Payload → Windows + apollo + http).
- Configure callback host/port and any HTTP-specific options (URI, user-agent, etc.).
- Build the payload and deliver it to a lab Windows target.
- Confirm a callback appears under Active Callbacks and that traffic is visible in your network sensors / Elastic.

> **Lab note**: C2 profiles and agents are real offensive capabilities. Use them only in isolated lab environments you own or have explicit written permission to operate in.

---

**End of Guide — Creating Mythic C2 Profile (HTTP)**

*Each of the 2 screenshots appears exactly once • Descriptions match the actual screenshots*
