# NetworkMiner

**Room:** [tryhackme.com/room/networkminer](https://tryhackme.com/room/networkminer)

NetworkMiner is a Network Forensic Analysis Tool (NFAT) — not a replacement for Wireshark, but a complement. Where Wireshark is for deep packet inspection, NetworkMiner is for quick host context and artifact extraction.

---

## What It's Good For

- Identifying hosts in a capture (IP, MAC, hostname, OS)
- Extracting files, images, credentials, and keywords from PCAPs automatically
- Getting a fast overview of what happened without manually hunting through packets
- Spotting anomalies and attack indicators (port scans, traffic spikes)

## What It's Not Good For

- Large PCAP files — gets slow/unwieldy
- Active traffic investigation requiring detailed filtering
- Replacing a proper IDS

---

## Two Operating Modes

**Sniffer Mode** — passive live capture, fingerprints hosts without sending any traffic itself

**PCAP Parsing Mode** — load a saved capture file and let it automatically reassemble and extract artifacts

---

## Key Tabs

| Tab | What you find there |
|-----|---------------------|
| **Hosts** | All identified hosts — IP, MAC, OS (fingerprinted via Satori/p0f) |
| **Sessions** | Detected network sessions between hosts |
| **DNS** | All DNS queries with details |
| **Credentials** | Extracted credentials and password hashes — huge for forensics |
| **Files** | Files extracted from the capture (with source/dest, protocol, timestamp) |
| **Images** | Images pulled from the traffic — viewable directly in the tool |
| **Parameters** | HTTP parameters and values extracted from requests |
| **Keywords** | Cleartext strings and keywords found in the traffic |
| **Messages** | Extracted emails, chats, messages |
| **Anomalies** | EternalBlue exploit attempts and spoofing detections |

---

## Practical Use in Forensics

Load a PCAP → NetworkMiner auto-populates all tabs. Instead of manually filtering in Wireshark:
- Go to **Credentials** tab first to check for exposed passwords
- Go to **Files** tab to see what was transferred
- Go to **Hosts** tab to understand what devices were talking
- Check **Anomalies** for anything that flagged automatically

Right-click the filename in the Case Panel → **Show Metadata** to see file-level details about the capture itself.
