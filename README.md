# Deloitte_Cybersecurity-simulation
Deloitte Cybersecurity simulation - Traffic Logs Analysis

# 🛡️ Deloitte Forage Cyber Simulation – Network Log Analysis Challenge

├── README.md

├── web_activity.log 

├── analysis-notes.md

└── screenshots/


## 📌 Scenario

Daikibo Industrials, a major manufacturing company, experienced a serious production disruption after a **data breach** led to the leak of sensitive internal information. As part of Deloitte’s Cyber Security team, the task was to **analyze web traffic logs** and investigate if the breach could have occurred **without VPN access** and identify **suspicious user activity**.

## 🎯 Objective

- Determine if the attacker had access from the open internet or required VPN tunneling.
- Examine the `web_requests.log` file to:
  - Identify suspicious behavioral patterns.
  - Detect automated behavior.
  - Identify the user ID responsible.

## 🔍 Approach

1. **Log File Format:**
   - Each block starts with an internal **static IP address**.
   - Followed by timestamped requests made to the **Daikibo telemetry dashboard**.
   - Each block = unique IP address.
   - **Sessions** are distinguishable by **dates** and require **new logins**.

2. **What to look for:**
   - Request sequences: Login → Resource loading (JS, CSS, images) → API calls.
   - Suspicious automation: regular time intervals with only API calls.
   - Manual sessions load **all resources**; automated ones do not.

3. **Investigation Steps:**
   - Open the `web_requests.log` in a code editor.
   - Identify blocks that skip loading frontend resources.
   - Observe **automated patterns** (e.g., hourly polling).
   - Find IP/user ID repeating this suspicious pattern.

## 🔐 Findings

- **Access from Internet?** ❌ No.
  - The dashboard resides **within Daikibo’s internal intranet**.
  - External attackers **must use VPN** to reach the dashboard.

- **Suspicious User ID:** `mdB7yD2dp1BFZPontHBQ1Z`
  - Started with normal login and resource loading.
  - Transitioned into **automated hourly API calls** without resource loads.
  - Behavior was too consistent to be human-driven.

## 📈 Skills Demonstrated

- Network traffic log analysis
- Recognizing signs of automation and intrusion
- Practical use of **log forensics** for incident response
- Understanding **internal vs external network access controls**

## 🧠 Learnings

This simulation emphasized how subtle patterns in user behavior can uncover security threats. Manual vs automated traffic distinction is **critical in forensic investigations**, especially in **air-gapped or intranet-only systems**.

## 🔗 Challenge URL

[🔗 Deloitte Forage Cyber Security Simulation](https://www.theforage.com/simulations/deloitte-au/cyber-c1e3)
