# Installing Mythic Agent (Apollo)

**Complete Step-by-Step Visual Guide**

Install the Apollo payload type into Mythic via mythic-cli

| Field | Value |
|-------|-------|
| **Agent / Payload type** | Apollo |
| **Repository** | https://github.com/MythicAgents/Apollo.git |
| **Supported OS** | Windows (.NET 4.0 compatible training agent) |
| **Mythic host** | SOC-Mythic |
| **Prerequisite** | Mythic C2 server already installed and running |

Each of the 3 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

1. Install Apollo agent via mythic-cli
2. Confirm successful installation
3. Verify Apollo is Online in Installed Services
4. Next steps

---

## 1. Install Apollo agent via mythic-cli

SSH into the Mythic server (SOC-Mythic) as root.

Change into the Mythic directory:

Run mythic-cli to install the Apollo agent from GitHub: mythic-cli clones the repository, parses config.json, processes the Apollo payload type, adds the service to docker-compose, and begins pulling the container image.

```bash
cd Mythic
./mythic-cli install github https://github.com/MythicAgents/Apollo.git
```

**Figure 1** – cd Mythic; ./mythic-cli install github https://github.com/MythicAgents/Apollo.git

---

## 2. Confirm successful installation

Wait for the install to finish. You should see:

- Image `ghcr.io/mythicagents/apollo:...` **Pulled**
- Container **apollo** → **Started**
- Messages: Successfully installed service / c2 / Payload documentation / Wrapper documentation
- Final line: **Successfully installed service!**

All other Mythic containers remain Healthy / Running.

**Figure 2** – Apollo image pulled, container Started, “Successfully installed service!”

---

## 3. Verify Apollo is Online in Installed Services

Open the Mythic web UI and go to **Installed Services** in the left sidebar.

Under the **AGENTS** tab you will see the **apollo** service listed.

Metadata shows:

- Author: @djhohnstein, @its_a_feature_
- Supported Operating Systems: Windows
- Version: 2.4.13
- Description: A fully featured .NET 4.0 compatible training agent

Confirm that the **Status** column shows **Online** (green).

**Figure 3** – Mythic UI → Installed Services → apollo Agent → Status Online

---

## 4. Next Steps

- Install a C2 profile (e.g. HTTP) if you have not already done so.
- Create a payload in the Mythic UI (Create Payload → select Windows + apollo).
- Configure the payload (output type WinExe, C2 profile, callback host/port, etc.) and build it.
- Deliver the payload to a lab Windows target and confirm a callback appears under Active Callbacks.
- Observe the resulting process/network activity in Sysmon and Elastic for detection practice.

> **Lab note**: Apollo is a real offensive agent. Use it only in isolated lab environments you own or have explicit written permission to test. Do not deploy against systems without authorization.

---

**End of Guide — Installing Mythic Agent (Apollo)**

*Each of the 3 screenshots appears exactly once • Descriptions match the actual screenshots*
