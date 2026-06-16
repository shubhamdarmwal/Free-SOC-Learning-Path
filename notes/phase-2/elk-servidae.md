# Servidae: Log Analysis in ELK

**Room:** [tryhackme.com/room/servidae](https://tryhackme.com/room/servidae)

A full incident investigation using Kibana — tracing an attacker's actions step by step through logs, from initial compromise to data exfiltration.

---

## Scenario

Bill Smith, a Finance Exec at Servidae Industries, opened a PDF attachment from an unknown sender. Shortly after, his workstation started acting up — slow, freezing — and EDR flagged suspicious network activity and unauthorized commands on his machine between **18:45–19:01 on May 11, 2023**.

Job: investigate the logs in Kibana and reconstruct what the attacker did.

---

## Kibana Basics

Set the time filter to the incident window (18:45–19:01) to narrow the Discover tab down to only relevant logs — same approach as any real investigation, don't drown in irrelevant noise.

**Key fields used throughout:**
- `agent.name` — which workstation generated the log
- `event.category` — type of event (process execution, command-line activity etc.)
- `process.command_line` — full command string run by a process
- `process.name` / `process.parent.name` — process and what spawned it
- `related.user` — user tied to the event
- `source.ip` / `destination.ip` — network event endpoints

---

## Tracing the Attack Chain

**1. Discovery**
Attacker downloaded `winPEAS.exe` (a privilege escalation enumeration tool) via PowerShell from an external server. After running it, they queried the Windows Registry (`reg query`) to validate a privilege escalation path winPEAS pointed to.

**2. Privilege Escalation**
Used KQL to filter for `.msi` activity in command lines — found a malicious `.msi` package used to escalate privileges.

**3. Persistence**
Multiple persistence techniques found:
- Created a new admin account via `net user` with no password expiry — classic backdoor account
- Scheduled task creation for persistence
- Registry edits for persistence

**4. Lateral Movement**
Attacker enumerated the internal network, found an internal payroll server, and brute-forced Bill's account on it. Once in, captured session cookie values from HTTP requests and eventually exfiltrated a sensitive file.

---

## Key Lesson

This room is basically a mini real-world IR case — phishing → recon → privesc → persistence → lateral movement → exfiltration. Following that chain through raw logs in Kibana (instead of reading it in a report) is what actually builds the instinct for "what do I check next" during a real investigation.
