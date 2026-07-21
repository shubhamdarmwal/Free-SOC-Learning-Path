# File and Hash Threat Intel

**Room:** [tryhackme.com/room/fileandhashthreatintel](https://tryhackme.com/room/fileandhashthreatintel)

How to investigate a suspicious file using heuristics, hashing, threat intel platforms, and sandbox analysis — then map findings to MITRE ATT&CK.

---

## Filepath & Filename Heuristics

Before even running a file, the path and name can give away a lot:
- Files in `%TEMP%`, `%APPDATA%`, or `C:\Users\Public\` are red flags — legitimate software rarely runs from there
- Names mimicking system binaries (e.g. `svch0st.exe`, `svchost32.exe`) = masquerading
- Double extensions (`invoice.pdf.exe`) = classic trick
- Random-looking names (`a3f9b2.exe`) = likely dropped by malware

---

## File Hash Lookup

Generate a hash to get a unique fingerprint of the file:
```bash
sha256sum <filename>    # Linux
Get-FileHash <filename> # PowerShell
```

Then check it against:

**VirusTotal** (`virustotal.com`)
- Shows vendor detections, family labels, first seen date, behavioral tags
- Check the **Relations** tab for connected IPs, domains, dropped files

**MalwareBazaar** (`bazaar.abuse.ch`)
- Community-sourced malware database
- Good for cross-referencing family, tags, and first-seen dates
- Often has download access to samples for researchers

---

## Sandbox Analysis

**Dynamic analysis** = run the file in an isolated environment and observe what it actually does.

Common sandbox tools:
- **Hybrid Analysis** (`hybrid-analysis.com`) — free, detailed reports
- **Any.run** — interactive sandbox
- **Joe Sandbox**, **Triage** — more advanced options

What to look for in a sandbox report:
- Files dropped during execution
- Registry changes
- Network connections made
- Commands/scripts executed
- MITRE ATT&CK technique mappings

**Sandbox limitations:** some malware detects it's in a sandbox and stays dormant — so a clean sandbox result doesn't always mean clean.

---
