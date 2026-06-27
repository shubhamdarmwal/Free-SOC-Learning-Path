# Network Traffic Basics

**Room:** [tryhackme.com/room/networktrafficbasics](https://tryhackme.com/room/networktrafficbasics)

Understanding what normal network traffic looks like is how you spot what isn't normal. Foundation room before jumping into Wireshark and PCAP analysis.

---

## Why Analyse Network Traffic?

Network traffic analysis (NTA) lets you detect threats that endpoint logs miss entirely — malware communicating out, data being exfiltrated, lateral movement between hosts.

Two common attack patterns visible in traffic:
- **DNS Tunneling** — attacker encodes data inside DNS queries/responses to sneak it past firewalls
- **Beaconing** — malware checking in with a C2 server at regular intervals (regular timing pattern is the giveaway)

---

## TCP/IP Model

| Layer | Name | What it carries |
|-------|------|-----------------|
| 4 | Application | HTTP, DNS, SMB, FTP — what the user/app sees |
| 3 | Transport | TCP/UDP — ports, connections, reliability |
| 2 | Internet | IP addresses — routing between networks |
| 1 | Link | MAC addresses — local delivery on the same network |

When analysing traffic, you're usually working at layers 3–4 but checking layer 7 content for what's actually being sent.

---

## Traffic Sources

**Intermediary Sources** — network devices that sit between endpoints
- Firewalls, routers, switches, proxies — log what passes through them

**Endpoint Sources** — the machines themselves
- Host-based firewall logs, EDR network telemetry, pcap from the endpoint

**Traffic Flows:**
- **North-South** — traffic going in/out of your network (internet-facing). Where you catch C2 comms and exfiltration.
- **East-West** — traffic moving between internal hosts. Where you catch lateral movement.

**Flow Examples:**
- **HTTPS** — encrypted web traffic, need SSL inspection to see content
- **External DNS** — should only go to approved resolvers, unusual destinations = red flag
- **SMB with Kerberos** — normal internal Windows traffic, but abuse of it = lateral movement

---

## How to Observe Network Traffic

**Logs** — firewall logs, proxy logs, DNS logs. High-level visibility, no packet content.

**Full Packet Capture** — captures every byte of traffic:
- **Network Tap** — physical device that copies traffic off the wire
- **Port Mirroring (SPAN)** — switch config that mirrors traffic to an analysis port
- **Tools** — Wireshark, tcpdump, Zeek

**Network Statistics** — flow data (NetFlow/IPFIX) — shows who talked to who, how much data, without storing full packet content. Good for spotting beaconing patterns.

---

## Lab

**Scenario 1 — HTTP traffic**
Paged through the packet table to the last page, last row showed an HTTP GET returning a zip file (10MB response). Expanded the row and found the flag in the body preview.
`THM{FoundTheMalware}`

**Scenario 2 — DNS traffic**
Filtered traffic on the link between sw01 and SRV-DNS. Paged through DNS queries — a TXT record response contained the C2 flag hidden inside the DNS data field. Classic DNS tunneling/C2 via DNS.
`THM{C2CommandFound}`

Key lesson from the lab: malware doesn't always use HTTP/HTTPS for C2. DNS is often overlooked and allowed outbound by default — exactly why attackers abuse it.
