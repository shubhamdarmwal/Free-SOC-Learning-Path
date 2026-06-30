# Network Security Essentials

**Room:** [tryhackme.com/room/networksecurityessentials](https://tryhackme.com/room/networksecurityessentials)

A full attack-chain investigation using raw firewall, IDS, and VPN logs — done manually via command line (grep/cut/sort/uniq) instead of a SIEM UI. Good for understanding what's actually happening under the hood before a SIEM does it for you.

---

## Network Basics

A small enterprise network is made up of: user workstations, file/DB servers, app servers (web/email/VPN), AD/auth servers, routers/switches, and firewalls/perimeter devices.

**Host-Centric Logs** — OS logs (Windows Event Logs, syslog), application logs, security tool logs (AV, EDR, HIDS)

**Network-Centric Logs:**
- Firewalls — first place to check for unauthorized connection attempts
- IDS/IPS — flags known attack signatures and anomalies in real time
- Routers/Switches — flow data (who talked to whom, how much data)
- Web Proxies — visibility into web traffic, policy violations, exfiltration
- VPN — tracks remote access, who connected from where and when

---

## The Network Perimeter

The perimeter is the boundary between internal network and the outside world — firewalls, IDS/IPS, proxies sit here. It's the first layer where attacks are visible, which makes it the analyst's first stop when investigating.

---

## Pattern Recognition (Key Takeaways)

- One source → many destinations = **scanning**
- One source → one destination, repeated = **brute-forcing**
- Perfectly regular time intervals = **beaconing (malware C2)**
- Context matters more than a single log line — an IDS alert explaining *why* something was flagged is far more useful than a bare firewall block.

---

## Quick Scenario Examples (from the room)

**Port scanning** — same external IP hitting multiple ports (21, 22, 23, 25, 53) on one internal host in seconds → classic scan, mostly blocked by firewall.

**SQL Injection / XSS / Directory Traversal** — WAF logs showing `action=BLOCK` with `attack_type` field directly naming the attack. Filtering on BLOCK is the fastest way to surface real threats.

**VPN brute-force** — flood of `FAILED_AUTH` against common usernames (admin, guest, user) from one IP, with scattered legit `SUCCESS_AUTH` from real employees mixed in. Grouping by source IP isolates the attacker.

---

## Lab — Full Breach Investigation

This was the real meat of the room — tracing an entire intrusion through three log files: `firewall.log`, `ids_alerts.log`, `vpn_auth.log`.

### 1. Reconnaissance
```bash
cat firewall.log | grep "BLOCK" | cut -d' ' -f5 | cut -d: -f1 | sort -nr | uniq -c
```
Counted blocked connections by source IP — one IP stood out with way more BLOCKs than anything else, scanning ports 21/22/23/445/3389. Pivoted to check if any of its requests got through:
```bash
cat firewall.log | grep <suspicious_ip> | grep "ALLOW"
```
Confirmed the attacker eventually got an ALLOW — meaning they found a way in.

### 2. VPN Brute-Force / Credential Access
```bash
cat vpn_auth.log | grep FAIL | cut -d' ' -f3 | sort -nr | uniq -c
```
Same suspicious IP had 118 failed VPN logins — way above normal. Filtered further and found a string of FAILs against a service account (`svc_*`) followed by a SUCCESS — credential stuffing/brute-force paid off, attacker got an internal IP assigned.

### 3. Lateral Movement
```bash
cat firewall.log | grep <compromised_internal_ip> | grep "ALLOW" | head
```
Compromised host started probing other internal machines on SMB/RDP/SSH (445/3389/22). Cross-referenced with IDS alerts and found `ET EXPLOIT Possible MS-SMB Lateral Movement` — confirmed the attacker pivoted further into the network via SMB.

### 4. C2 Beaconing
```bash
cat ids_alerts.log | grep C2 | head
```
Found repeated `ET TROJAN Possible C2 Beaconing` alerts from the compromised host to an external IP on port 4444 — at regular time intervals, the textbook beaconing pattern.

### 5. Data Exfiltration
```bash
cat firewall.log | grep <compromised_ip> | cut -d' ' -f5,6,7 | uniq | sort
```
Found a large volume of outbound traffic from the compromised host to an external IP on ports 80/8080. IDS confirmed it:
```
ET INFO Possible HTTP POST Large Upload [Classification: Potential Data Exfiltration]
```

---

## Key Lesson

This room is basically the full kill chain reconstructed from raw logs: **scan → brute-force → lateral movement → C2 → exfiltration.** Doing it manually with grep/cut/sort instead of a SIEM forces you to actually understand *what* a SIEM is doing for you under the hood — pivoting on IPs, correlating across log sources, and narrowing noise down to signal. Same investigation would take seconds in Splunk, but the manual version builds the actual analyst instinct.
