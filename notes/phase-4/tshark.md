# TShark

**Room:** [tryhackme.com/room/tshark](https://tryhackme.com/room/tshark)

TShark is command-line Wireshark. Same filters, same dissection engine — but scriptable, automatable, and works over SSH without a GUI. Useful when you need to extract specific fields from a PCAP fast instead of clicking through Wireshark manually.

---

## Installation

Usually comes bundled with Wireshark. Verify:
```bash
apt list tshark
# if not installed:
sudo apt install tshark
```
Also available on Windows as `tshark.exe` in the Wireshark install directory.

---

## Core Commands

**Read a PCAP:**
```bash
tshark -r dns.cap
```
Outputs a summary line per packet — similar to tcpdump output.

**Count total packets:**
```bash
tshark -r dns.cap | wc -l
```

**Filter with display filters (`-Y`):**
```bash
# Show only DNS A record queries
tshark -r dns.cap -Y "dns.qry.type == 1"
```
Same display filter syntax as Wireshark — not BPF.

**Extract specific fields (`-T fields -e`):**
```bash
# Extract just the queried domain names from DNS A records
tshark -r dns.cap -Y "dns.qry.type == 1" -T fields -e dns.qry.name
```
This is where TShark really shines — instead of reading full packet output, you pull only the exact field you care about.

> **Tip:** To find a field name, highlight it in Wireshark's packet details pane and check the bottom-left corner — it shows the field identifier you can use with `-e`.

---

## Lab — DNS Exfiltration

A host on the network was exfiltrating data over DNS. Used Wireshark to spot suspicious DNS traffic, then pivoted to TShark to extract and read the exfiltrated data from the query names.

DNS exfiltration works by encoding data into subdomains of DNS queries — the data gets sent to an attacker-controlled DNS server disguised as legitimate lookups. The queries look like:

```
aGVsbG8=.attacker.com
d29ybGQ=.attacker.com
```

Filtered for DNS queries and extracted the `dns.qry.name` field — the encoded data in the subdomains was the exfiltrated content.

Key lesson: DNS exfiltration is hard to catch without specifically looking at query *content*, not just destination. Volume of queries + unusual subdomain patterns = red flag.
