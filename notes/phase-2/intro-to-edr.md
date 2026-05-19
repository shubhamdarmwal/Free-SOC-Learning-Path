# Introduction to EDR

**Room:** [tryhackme.com/room/introductiontoedrs](https://tryhackme.com/room/introductiontoedrs)

Antivirus catches known bad stuff. EDR catches everything else.

---

## AV vs EDR

| | Antivirus | EDR |
|---|---|---|
| Detection method | Signature-based | Behaviour-based + signatures |
| Visibility | File scanning | Full endpoint activity |
| Response | Quarantine/delete | Isolate, kill process, rollback |
| Threat coverage | Known malware | Known + unknown + fileless attacks |

AV asks "is this file malicious?" — EDR asks "is this behaviour malicious?"

---

## How EDR Works

**Agent** — lightweight software installed on every endpoint. Constantly collects telemetry and sends it back to the EDR console.

**EDR Console** — central place where analysts see all endpoint activity, alerts, and can take response actions across every machine from one place.

**After Detection** — EDR doesn't just alert, it can:
- Isolate the endpoint from the network
- Kill the malicious process
- Remove the threat
- Roll back changes (e.g. ransomware file encryption)

**Integration** — EDR feeds into the SIEM. So the SOC gets endpoint telemetry alongside network and log data in one view.

---

## Telemetry

Telemetry = everything the agent is silently recording on the endpoint:

- Process creation and termination
- File reads, writes, deletions
- Network connections made by processes
- Registry changes
- User logins and privilege changes
- Script execution (PowerShell, cmd, etc.)

This is why EDR catches fileless attacks that AV misses — there's no malicious file to scan, but there's always suspicious behaviour to catch.

---

## Detection & Response

EDR detects through behaviour rules and ML models — if a process does something that looks like lateral movement, credential dumping, or persistence, it fires an alert.

Response is the key differentiator from AV. A few clicks from the console and you can contain a threat across hundreds of endpoints without physically touching a single machine.

---

## Lab — EDR Triage (TECH THM)

Given access to an EDR console with multiple medium and high severity detections. Had to triage each one — look at the telemetry, understand what the process did, and answer questions about the detections.

Same workflow as real SOC work: alert comes in → check process tree → check network connections → check file activity → verdict.
