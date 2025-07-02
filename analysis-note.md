# 🔎 Analysis Notes – Deloitte Forage Cyber Security Simulation

## 🧠 Objective Recap

Analyze `web_requests.log` to:
- Determine whether the dashboard was accessible from the public internet.
- Identify any suspicious user behavior (especially automated requests).

---

## 🧭 Step-by-Step Analysis

### 1️⃣ Understand Log Structure

Each block of log entries:
- Starts with a **static internal IP address**
- Contains **timestamped HTTP requests** to the internal dashboard
- Ends with an empty line
- Each block represents **a unique device/session**

> 🔍 Tip: Use a code editor (VS Code or Sublime Text) with small font + full screen to improve readability.

---

### 2️⃣ Detecting Public Internet Access

- ✅ Confirmed that **all IP addresses are internal static IPs**.
- 🛑 The dashboard is hosted **inside Daikibo’s intranet**.
- 🔐 No evidence of exposed endpoints or public IPs in any session.
- ✔️ **Conclusion**: Dashboard access is **intranet-only** via internal IPs or VPN tunneling.

---

### 3️⃣ Spotting Suspicious Behavior

#### ✅ Normal User Behavior:
- Login page hit (`/login`)
- Resource requests (CSS, JS, images)
- Dashboard rendering
- Occasional refreshes

#### 🚨 Suspicious Pattern:
- `User ID: mdB7yD2dp1BFZPontHBQ1Z`
- Timeline:
  - Normal login sequence at first
  - Transition to hourly API requests only: `/api/factory_status` and `/api/machine_status`
  - No resource loading (CSS, images, scripts)
- Behavior is **too consistent** to be human-driven → classic automation fingerprint
- **Huge amount of traffic generated**

#### 🧠 Indicators of Automation:
- Identical requests at **exactly one-hour intervals**
- Absence of associated frontend requests
- Consistent targeting of all four factory APIs
- No date-based login renewal in some sessions — suggesting stored credentials or reuse

---

## ✅ Final Answers (from quiz)

| Question | Answer |
|---------|--------|
|1) Looking at the web_requests.log, what is the user ID with the most suspicious activity? | ❌ No, the attacker has no direct access to the status dashboard (Intranet ONLY) |
|2) Looking at the web_requests.log, what is the user ID with the most suspicious activity? | `mdB7yD2dp1BFZPontHBQ1Z` |

---

## 🔚 Conclusion

This simulation helped solidify core principles of log forensics:
- Manual vs. automated behavior
- Recognizing patterns in session structure
- Investigating internal-only systems for insider threats
