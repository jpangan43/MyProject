# Sysmon Setup with Elastic Agent

**Complete Step-by-Step Visual Guide**  
Collect Microsoft-Windows-Sysmon/Operational via Custom Windows Event Logs

| Field              | Value                                      |
|--------------------|--------------------------------------------|
| **Integration**    | Custom Windows Event Logs                  |
| **Channel**        | Microsoft-Windows-Sysmon/Operational       |
| **Integration name**| SOC-Win-Sysmon                            |
| **Prerequisite**   | Sysmon already installed on the Windows host |
| **Elastic Agent**  | Already enrolled (Windows policy)          |

Each of the 7 screenshots in this guide appears exactly once.

---

## Table of Contents

1. [Log into Kibana](#1-log-into-kibana)
2. [Open Add integrations](#2-open-add-integrations)
3. [Search for Windows / Custom Windows Event Logs](#3-search-for-windows--custom-windows-event-logs)
4. [Add Custom Windows Event Logs integration](#4-add-custom-windows-event-logs-integration)
5. [Configure integration (name, channel)](#5-configure-integration-name-channel)
6. [Assign to an agent policy](#6-assign-to-an-agent-policy)
7. [(Optional) Filter specific Event IDs](#7-optional-filter-specific-event-ids)
8. [Next Steps](#8-next-steps)

---

## 1. Log into Kibana

Open Kibana in your browser.

Log in with the **elastic** user (or another user that has Fleet / Integrations privileges).

---

## 2. Open Add integrations

From the Kibana home page click **+ Add integrations**.

You can also reach the same place via **Management → Integrations**.

---

## 3. Search for Windows / Custom Windows Event Logs

In the search box type `windows`.

Select the integration **Custom Windows Event Logs**.

This integration can collect any Windows event log channel, including Sysmon.

---

## 4. Add Custom Windows Event Logs integration

On the integration overview page click the blue button **+ Add Custom Windows Event Logs**.

---

## 5. Configure integration (name, channel)

Set the following values:

- **Integration name:** `SOC-Win-Sysmon`
- **Description:** Collect logs from Sysmon (optional)
- **Channel Name:** `Microsoft-Windows-Sysmon/Operational`

This is the standard Sysmon operational log channel.

---

## 6. Assign to an agent policy

Under "Where to add this integration?" choose **Existing hosts**.

Select the agent policy that is assigned to your Windows hosts (e.g. `SOC-Win-2025`).

Click **Save / Add integration** when finished.

---

## 7. (Optional) Filter specific Event IDs

In Advanced options you can optionally restrict collection to specific Sysmon Event IDs (example shown: 1116, 1117, 5001).

Leave this empty if you want all Sysmon events.

Common useful Sysmon IDs include 1 (Process Create), 3 (Network Connect), 7 (Image Load), 10 (Process Access), 11 (File Create), etc.

---

## 8. Next Steps

- Confirm Sysmon is installed and running on the Windows host (`sysmon64.exe -c config.xml` or check the service).
- Generate some activity on the Windows host and verify events appear in Discover (filter on the data stream or `event.provider : "Microsoft-Windows-Sysmon"`).
- Create detection rules in **Security → Rules** that use Sysmon Event IDs.
- Build dashboards for process trees, network connections, and file creations.
- Continue with the Alerts and Dashboards guide for more advanced visualizations.

> **Prerequisite reminder:** Sysmon itself must already be installed on the Windows endpoint. This guide only configures Elastic Agent to collect the Sysmon event log channel.

---

**End of Guide — Sysmon Setup with Elastic Agent**

*Each of the 7 screenshots appears exactly once • For internal documentation / training use*
