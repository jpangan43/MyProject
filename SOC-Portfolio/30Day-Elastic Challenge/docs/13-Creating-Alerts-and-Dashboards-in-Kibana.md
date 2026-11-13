# Creating Alerts and Dashboards in Kibana

**Complete Step-by-Step Visual Guide**

Discover SSH failures → Save session → Create threshold rule → Build network map dashboard

| Field | Value |
|-------|-------|
| **Focus** | SSH failed (and successful) authentication on SOC-SSH-Server |
| **Data view** | Security solution default |
| **Key field** | system.auth.ssh.event (Failed / Accepted) |
| **Alert** | Search threshold rule from Discover |
| **Dashboard** | Choropleth world map of source countries |

Each of the 27 screenshots appears exactly once. Descriptions match the actual screenshots.

---

## Table of Contents

**Part A – Discover & Filter SSH Failures (Steps 1–9)**

**Part B – Save Discover Session & Create Alert Rule (Steps 10–15)**

**Part C – Create Choropleth Network Map (Steps 16–21)**

**Part D – Save Map to Dashboard & Duplicate for Successes (Steps 22–27)**

**Next Steps**

---

## Part A – Discover & Filter SSH Failures

### 1. Open Discover

Log into Kibana.

Open the main menu (hamburger icon) → expand **Analytics** → click **Discover**.

**Figure 1** – Main menu → Analytics → Discover

---

### 2. Filter by agent.name and set time range

In the left field list click **agent.name**.

In the popup you will see the top values (SOC-FLEET-SERVER, MYDFIR-WIN-jasonlee, SOC-SSH-Server).

Click the **+** icon next to the host you want to investigate (e.g. SOC-SSH-Server).

Set the time picker (top right) to **Today**.

**Figure 2** – agent.name field → add filter for a host; time range = Today

---

### 3. Locate system.auth.ssh.event

With the agent filter applied, find the field **system.auth.ssh.event** in the sidebar.

Click it. The top values show Failed (majority) and other values.

Click the **+** next to Failed to add it as a filter.

**Figure 3** – system.auth.ssh.event field with top values Failed / message

---

### 4. Search “failed” and review documents

You can also type `failed` in the Discover search bar.

The Documents tab now lists matching events (example: 158 documents).

The column **system.auth.ssh.event** shows the value Failed.

**Figure 4** – Search bar = “failed”; Documents tab showing Failed events

---

### 5. Add user.name as a column

In the left field list hover over **user.name**.

Click the **+** icon (“Add field as column”) so the username appears in the document table.

**Figure 5** – Add field as column → user.name

---

### 6. Add source.ip as a column

Likewise, hover over **source.ip** and click the **+** icon to add the source IP address as a column.

**Figure 6** – Add field as column → source.ip

---

### 7. Add source.geo.country_name as a column

Hover over **source.geo.country_name** and click the **+** icon to display the country of the source IP in the table.

**Figure 7** – Add field as column → source.geo.country_name

---

### 8. Review the filtered document list

The table now shows timestamp, system.auth.ssh.event = Failed, user.name, source.ip and source.geo.country_name. Example rows show user “solv” from Romania (80.94.92.166).

**Figure 8** – Document rows showing Failed, username (solv), source IP and country

---

### 9. Click Save in Discover

With the useful columns and filters in place, click the blue **Save** button in the top-right corner of Discover.

**Figure 9** – Discover toolbar → Save button

---

## Part B – Save Discover Session & Create Alert Rule

### 10. Save the Discover session

In the “Save Discover session” dialog enter the title **SSH Failed Activity**.

Click **Save**.

The open tab is now saved and can be reopened later.

**Figure 10** – Save Discover session → Title = SSH Failed Activity

---

### 11. Open Alerts → Create search threshold rule

Still in Discover, click the **Alerts** button in the toolbar.

From the dropdown choose **Create search threshold rule**.

This creates a rule based on the current Discover query and filters.

**Figure 11** – Alerts dropdown → Create search threshold rule

---

### 12. Define the rule query and threshold

The rule form is pre-filled with the data view (Security solution default) and your filters (agent.name: SOC-SSH-Server, system.auth.ssh.event: Failed).

Set the threshold, for example: **WHEN count() OVER all documents IS ABOVE 5 FOR THE LAST 5 minutes**.

Click **Next**.

**Figure 12** – Create rule → query, filters, WHEN count() IS ABOVE 5 FOR THE LAST 5 minutes

---

### 13. Actions step (optional)

On the Actions step you can attach a connector (email, Slack, webhook, etc.).

For a lab you can leave actions empty. Click **Next**.

**Figure 13** – Create rule → Actions step → Add an action (optional)

---

### 14. Rule details and Create rule

On the Details step give the rule a name (or keep the default “Elasticsearch query rule”).

Optionally add tags or an investigation guide.

Click **Create rule**.

**Figure 14** – Details step → Rule name → Create rule

---

### 15. Confirm save with no actions

If you did not add an action, Kibana asks for confirmation.

Click **Save rule**. The rule is now active.

**Figure 15** – “Save rule with no actions?” → Save rule

---

## Part C – Create Choropleth Network Map

### 16. Open Maps

From the main menu go to **Analytics → Maps** (or open Maps from a saved Discover session context).

**Figure 16** – Main menu → Analytics → Maps

---

### 17. Set the map query and click Add layer

In the Maps search bar enter a query such as:  
`system.auth.ssh.event : *` and `agent.name:SOC-SSH-Server` and `system.auth.ssh.event: Failed`

Click the blue **Add layer** button.

**Figure 17** – Maps query bar + Add layer button

---

### 18. Choose Choropleth layer

In the Add layer panel select **Choropleth** (“Shade areas to compare statistics across boundaries”).

**Figure 18** – Add layer → Choropleth

---

### 19. Configure the Choropleth layer

- Boundaries source: Administrative boundaries from the Elastic Maps Service
- EMS boundaries: World Countries
- Join field (boundaries): ISO 3166-1 alpha-2 code
- Statistics source data view: Security solution default
- Join field (statistics): source.geo.country_iso_code

Click **Add and continue**.

**Figure 19** – Boundaries = World Countries; Join field = source.geo.country_iso_code

---

### 20. Layer settings and Save the map

Adjust opacity, tooltips, or leave the defaults.

Click the blue **Save** button in the top-right of the Maps UI.

**Figure 20** – Layer settings panel → Save

---

### 21. Save map as “SSH Network Map” and create a new dashboard

Title: **SSH Network Map**

Under “Add to dashboard” select **New**.

Click **Save and go to Dashboard**.

**Figure 21** – Save map → Title = SSH Network Map → Add to dashboard = New

---

## Part D – Save Map to Dashboard & Duplicate for Successes

### 22. Dashboard with the map – click Save

You are taken to a new dashboard that already contains the map panel (“SSH Failed Authentication – Network Map”). Click the blue **Save** button.

**Figure 22** – New dashboard containing the choropleth map → Save

---

### 23. Name the dashboard

Enter the dashboard title **SOC-Authentication-Activity**.

Click **Save**.

**Figure 23** – Save as new dashboard → Title = SOC-Authentication-Activity

---

### 24. Duplicate the map panel

On the saved dashboard open the panel options (three dots) on the map. Choose **Duplicate** so you can create a second map for successful logins.

**Figure 24** – Panel menu → Duplicate

---

### 25. Rename the duplicated panel

Open Settings on the duplicated panel.

Change the title to **SSH Successful Authentication**.

Click **Apply**.

**Figure 25** – Settings → Title = SSH Successful Authentication

---

### 26. Edit the map configuration of the success panel

Click the pencil / “Edit map configuration” icon on the successful-authentication panel to open the map editor for that panel.

**Figure 26** – Edit map configuration icon on the panel

---

### 27. Change the query to Accepted and Save

In the map editor change the filter from Failed to Accepted (or edit the KQL so it uses `system.auth.ssh.event: Accepted`). Click **Save and return**.

You now have a dashboard with two maps: failed and successful SSH authentications by country.

**Figure 27** – Query changed to system.auth.ssh.event: Accepted → Save and return

---

## Next Steps

- Generate additional failed SSH logins in the lab and confirm the threshold rule fires.
- Add an action (email / Slack / index) to the rule so the team is notified.
- Create similar Discover sessions and rules for Windows logon failures or Sysmon events.
- Pin the SOC-Authentication-Activity dashboard to the Kibana home page.
- Document the rule and dashboard in your SOC playbooks / osTicket.

> **Note**: The threshold (count > 5 in 5 minutes) is an example. Adjust it to match the normal baseline of your environment to avoid false positives.

---

**End of Guide — Creating Alerts and Dashboards in Kibana**

*Each of the 27 screenshots appears exactly once • Descriptions match the actual screenshots*
