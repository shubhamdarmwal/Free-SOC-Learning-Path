# 🔐 Free TryHackMe SOC Labs – Step-by-Step Learning Path

A **structured, phase-based learning path** using free TryHackMe rooms for aspiring **SOC Analysts (L1 & L2)**, **Blue Teamers**, and **DFIR practitioners**. Every room here is free. Follow the phases in order for maximum learning progression.

> ⚠️ TryHackMe occasionally paywalls rooms without notice. Verify free access before starting.

---

## 🗺️ Learning Path Overview

```
Phase 1 → Foundations & SOC Mindset
Phase 2 → Core SOC Tools (SIEM, EDR)
Phase 3 → Windows & Linux Log Analysis
Phase 4 → Network Traffic Analysis
Phase 5 → Threat Intelligence & Detection
Phase 6 → Incident Response
Phase 7 → Memory & Advanced Forensics
Phase 8 → CTF Capstone Challenges
```

---

## ✅ Progress Tracker

| Phase | Topic | Rooms | Status |
|-------|-------|-------|--------|
| 1 | Foundations | 4 | ⬜ |
| 2 | Core SOC Tools | 8 | ⬜ |
| 3 | Windows & Linux Logs | 9 | ⬜ |
| 4 | Network Traffic Analysis | 6 | ⬜ |
| 5 | Threat Intel & Detection | 5 | ⬜ |
| 6 | Incident Response | 6 | ⬜ |
| 7 | Memory & Advanced Forensics | 2 | ⬜ |
| 8 | CTF Capstone Challenges | 5 | ⬜ |

> Replace ⬜ with ✅ as you complete each phase.

---

## 🟢 Phase 1 — Foundations & SOC Mindset

> **Goal:** Understand what a SOC is, what analysts do, and how blue teaming works. Start here, no exceptions.

| # | Room | What You'll Learn | Link | Notes |
|---|------|-------------------|------| ----- |
| 1 | 🛡️ Defensive Security Intro | Big picture of blue team — Threat Intel, SOC, DFIR, Malware Analysis, SIEM | [🔗 Visit](https://tryhackme.com/room/defensivesecurityintroqW) | [📝](notes/phase-1/defensive-security-intro.md) |
| 2 | 🔵 SOC Role in Blue Team | SOC structure, L1/L2/L3 roles, analyst responsibilities | [🔗 Visit](https://tryhackme.com/room/socroleinblueteam) | [📝](notes/phase-1/soc-role-in-blue-team.md) |
| 3 | 🧾 Intro to Logs | What logs are, types, formats, where they come from | [🔗 Visit](https://tryhackme.com/room/introtologs) |
| 4 | 🧠 SOC Analyst Basics | SOC L1 alert reporting, how to write an alert report | [🔗 Visit](https://tryhackme.com/room/socl1alertreporting) |

---

## 🔵 Phase 2 — Core SOC Tools (SIEM & EDR)

> **Goal:** Get hands-on with the tools every SOC analyst uses daily — Splunk, ELK, Wazuh, and Sentinel.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 5 | 📊 Introduction to SIEM | SIEM concepts, log aggregation, alert correlation | [🔗 Visit](https://tryhackme.com/room/introtosiem) |
| 6 | 🖥️ Introduction to EDR | Endpoint Detection & Response fundamentals | [🔗 Visit](https://tryhackme.com/room/introductiontoedrs) |
| 7 | 🛠️ Splunk 101 | Splunk basics, search interface, dashboards | [🔗 Visit](https://tryhackme.com/room/splunk101) |
| 8 | 🧠 Splunk: Exploring SPL | Search Processing Language, filters, stats | [🔗 Visit](https://tryhackme.com/room/splunkexploringspl) |
| 9 | 🧿 Wazuh | Wazuh SIEM — open source SOC stack | [🔗 Visit](https://tryhackme.com/room/wazuhct) |
| 10 | 📊 ELK 101 | Investigating with ELK (Elasticsearch, Logstash, Kibana) | [🔗 Visit](https://tryhackme.com/room/investigatingwithelk101) |
| 11 | 🧮 ELK: Servidae | Log analysis deep-dive in ELK | [🔗 Visit](https://tryhackme.com/room/servidae) |
| 12 | 📊 MS Sentinel | Microsoft Sentinel cloud SIEM | [🔗 Visit](https://tryhackme.com/room/mssentineljustlooking) |

---

## 🟡 Phase 3 — Windows & Linux Log Analysis

> **Goal:** Learn to read and investigate OS-level logs — the bread and butter of SOC L1 work.

### Windows

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 13 | 🪟 Windows Event Logs | Event Viewer, key Event IDs, log categories | [🔗 Visit](https://tryhackme.com/room/windowseventlogs) |
| 14 | 🪵 Windows Log Analysis | Windows logging for SOC — Sysmon, audit policies | [🔗 Visit](https://tryhackme.com/room/windowsloggingforsoc) |
| 15 | 📂 Windows Threat Detection | Detecting attacks in Windows logs | [🔗 Visit](https://tryhackme.com/room/windowsthreatdetection1) |
| 16 | 👨‍💻 Investigating Windows | Full Windows forensics investigation challenge | [🔗 Visit](https://tryhackme.com/room/investigatingwindows) |
| 17 | 🔍 Investigating Windows 2.0 | Advanced Windows log forensics | [🔗 Visit](https://tryhackme.com/room/investigatingwindows2) |
| 18 | 💻 Osquery | Query endpoints like a database for EDR | [🔗 Visit](https://tryhackme.com/room/osqueryf8) |

### Linux

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 19 | 🐧 Linux Logging for SOC | Auth logs, syslog, journald, audit logs | [🔗 Visit](https://tryhackme.com/room/linuxloggingforsoc) |
| 20 | 🐧 Linux Threat Detection | Detecting attacker activity in Linux logs | [🔗 Visit](https://tryhackme.com/room/linuxthreatdetection1) |
| 21 | 🐧 Linux Server Forensics | Full Linux forensics investigation | [🔗 Visit](https://tryhackme.com/room/linuxserverforensics) |

---

## 🟠 Phase 4 — Network Traffic Analysis

> **Goal:** Investigate network-level activity — PCAPs, protocols, anomalies. Essential for alert triage.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 22 | 📶 Network Traffic Basics | Protocols, packet structure, traffic types | [🔗 Visit](https://tryhackme.com/room/networktrafficbasics) |
| 23 | 🔒 Network Security Essentials | Network monitoring, baselines, protection | [🔗 Visit](https://tryhackme.com/room/networksecurityessentials) |
| 24 | 🌐 Wireshark | Wireshark basics — capture, filter, analyze | [🔗 Visit](https://tryhackme.com/room/wiresharkthebasics) |
| 25 | ❄️ TShark | Command-line Wireshark for SOC pipelines | [🔗 Visit](https://tryhackme.com/room/tshark) |
| 26 | 🧾 NetworkMiner | Passive network forensics tool | [🔗 Visit](https://tryhackme.com/room/networkminer) |
| 27 | 🌐 Event Horizon | Wireshark + file analysis challenge | [🔗 Visit](https://tryhackme.com/room/eventhorizonroom) |

---

## 🔴 Phase 5 — Threat Intelligence & Detection

> **Goal:** Learn how to identify, classify, and hunt for threats using IOCs, YARA, and threat intel feeds.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 28 | 🗂️ File and Hash Threat Intel | Using file hashes as IOCs, VirusTotal, threat intel platforms | [🔗 Visit](https://tryhackme.com/room/fileandhashthreatintel) |
| 29 | 🔬 YARA | Writing YARA rules for malware detection | [🔗 Visit](https://tryhackme.com/room/yara) |
| 30 | 🧠 YARA Advanced | Threat hunting with YARA — real-world rule writing | [🔗 Visit](https://tryhackme.com/room/threathuntingwithyara) |
| 31 | 🕵️ Threat Hunting Without Logs | Hunting for threats when logs are missing | [🔗 Visit](https://tryhackme.com/room/loglesshunt) |
| 32 | ⚔️ APT Detection (Volt Typhoon) | Detect a real nation-state APT campaign | [🔗 Visit](https://tryhackme.com/room/volttyphoon) |

---

## 🟣 Phase 6 — Incident Response

> **Goal:** Handle a full incident — from detection through scoping, containment, and investigation.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 33 | 📘 IR Playbooks | How to follow and use IR playbooks | [🔗 Visit](https://tryhackme.com/room/irplaybooks) |
| 34 | 🔎 Identification & Scoping | Scoping an incident before diving in | [🔗 Visit](https://tryhackme.com/room/identificationandscoping) |
| 35 | ⚡ Detecting Web Attacks | Identifying web-based attacks in logs | [🔗 Visit](https://tryhackme.com/room/detectingwebattacks) |
| 36 | 🛡️ AppSec IR | Application security incident response | [🔗 Visit](https://tryhackme.com/room/appsecir) |
| 37 | 🍯 Initial Access Pot | Investigate attacker initial access via honeynet | [🔗 Visit](https://tryhackme.com/room/initialaccesspot) |
| 38 | 📡 Overpass 2 — Hacked | Full IR via log analysis on a compromised box | [🔗 Visit](https://tryhackme.com/room/overpass2hacked) |

---

## ⚫ Phase 7 — Memory & Advanced Forensics

> **Goal:** Analyze RAM dumps and volatile memory — critical for malware investigation and advanced DFIR.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 39 | 🧠 Memory Forensics | RAM dump analysis fundamentals | [🔗 Visit](https://tryhackme.com/room/memoryforensics) |
| 40 | 🧊 Volatility | Volatility framework — processes, network, artifacts | [🔗 Visit](https://tryhackme.com/room/volatility) |

---

## 🏆 Phase 8 — CTF Capstone Challenges

> **Goal:** Apply everything you've learned in realistic, timed SOC scenarios. These simulate actual analyst work.

| # | Room | What You'll Learn | Link |
|---|------|-------------------|------|
| 41 | 📑 SOC Alert Triage | Full SOC L1 alert triage simulation | [🔗 Visit](https://tryhackme.com/room/socl1alerttriage) |
| 42 | 🎯 First Shift CTF | Your first SOC shift — multi-skill challenge | [🔗 Visit](https://tryhackme.com/room/first-shift-ctf) |
| 43 | 🕳️ h4cked | PCAP investigation challenge | [🔗 Visit](https://tryhackme.com/room/h4cked) |
| 44 | 🕷️ Carnage | Advanced traffic analysis challenge | [🔗 Visit](https://tryhackme.com/room/carnage) |
| 45 | 📌 CCT2019 | PCAP forensics competition challenge | [🔗 Visit](https://tryhackme.com/room/cct2019) |

> **Bonus:** [🔗 Chaining Vulnerabilities](https://tryhackme.com/room/chainingvulnerabilitiesZp) — Understand exploit chains from a defender's perspective. Great if you're coming from a bug bounty / red team background.
> 
> [🔗 Network Discovery Detection](https://tryhackme.com/room/networkdiscoverydetection) — Detect Nmap and asset discovery activity on your network.

---

## 🧭 Suggested Weekly Schedule

| Week | Phases | Focus |
|------|--------|-------|
| Week 1 | Phase 1 + 2 | SOC foundations + SIEM tools |
| Week 2 | Phase 3 | Windows & Linux log analysis |
| Week 3 | Phase 4 + 5 | Network traffic + Threat intel |
| Week 4 | Phase 6 + 7 | Incident response + Memory forensics |
| Week 5 | Phase 8 | CTF challenges — test everything |

---

## 💡 Free Tier Tips

- **1-hour AttackBox limit:** Read theory tasks without launching the VM. Save your time for challenge rooms.
- **Answer tasks from reading:** Most Phase 1–2 rooms can be completed without the VM at all.
- **Save AttackBox for:** Investigating Windows, h4cked, Carnage, Volatility, and CTF rooms.

---

## 🔗 Pair With These Free Platforms

| Platform | Best For | Cost |
|----------|----------|------|
| [CyberDefenders](https://cyberdefenders.org) | DFIR investigations, blue team CTFs | Free |
| [LetsDefend](https://letsdefend.io) | Real SOC alert queue simulation | Free tier |
| [BlueTeamLabs Online](https://blueteamlabs.online) | Phishing, PCAP, malware triage labs | Free tier |

---

## 🏅 Target Certifications After This Path

- CompTIA CySA+
- SC-200: Microsoft Security Operations Analyst
- Blue Team Level 1 (BTL1)
- GCIH (GIAC Certified Incident Handler)

---

## 💙 Credit

Original room collection by [AtikBagwan00](https://github.com/AtikBagwan00/tryhackme-soc-free-labs). This repo reorganizes those rooms into a structured learning path.

---

> ⭐ Star this repo if it helped you. Fork it to track your own progress.
