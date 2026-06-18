# Wazuh

**Room:** [tryhackme.com/room/wazuhct](https://tryhackme.com/room/wazuhct)

Wazuh is an open-source SIEM + EDR hybrid — good to know since it's free and widely used in home labs and smaller orgs. Already familiar with this from my own Wazuh home lab setup, but good to revisit the platform basics here.

---

## Agents

Agents are the devices/endpoints that record events and processes, then send them to the Wazuh server. Deployed from **Wazuh → Agents → Deploy New Agent**.

---

## Vulnerability Assessment & Security Events

Per-agent vulnerability and security event data is viewed at **Wazuh → Agents → [specific agent]**. Shows known CVEs affecting that endpoint based on installed software.

---

## Policy Auditing

**Wazuh → Modules → Policy Management** — checks an endpoint's configuration against security baselines (CIS benchmarks etc.) and flags non-compliant settings.

---

## Monitoring Logons

**Wazuh → Management → Rules** — this is where detection rules live, including the ones that fire on logon events (failed logins, logins outside business hours, etc.)

---

## Collecting Windows Logs

Windows logs auth attempts, network connections, file access, and app behaviour — but Sysmon is what captures the *detailed* version of this for Wazuh to ingest.

To enable Sysmon with a specific config:
```
Sysmon64.exe -accepteula -i detect_powershell.xml
```

---

## Collecting Linux Logs

Wazuh ships with a ruleset (`/var/ossec/ruleset/rules`) that can parse logs from common services — e.g. Apache2 errors/warnings.

To enable this, the relevant rule needs to be added to the agent's config file:
```
/var/ossec/etc/ossec.conf
```

---

## Auditing Linux Commands (auditd)

For monitoring specific commands/actions (like anything run as root), Wazuh leans on `auditd`.

Install and enable it:
```bash
sudo apt-get install auditd audispd-plugins
sudo systemctl enable auditd.service
sudo systemctl start auditd.service
```

Then configure an audit rule to watch for root-level command execution. This is how you'd catch privilege escalation attempts on a Linux endpoint.

---

## Wazuh API

Two ways to interact with it:
- **Own client** — script/tool you build yourself hitting the API
- **Wazuh's API Console** — built-in interface for testing API calls directly

Useful for automation — pulling agent data or triggering actions programmatically instead of clicking through the UI.

---

## Generating Reports

**Modules → Security Events** → generate a summarised report (e.g. last 24 hours of security events for an agent). Useful for handing off a clean summary instead of raw logs.

---

## Loading Sample Data

For practice without a live environment:
**Wazuh tab → Settings → Sample Data → Add Data** on the relevant cards. Populates the dashboard with fake data to practice navigating and querying.
