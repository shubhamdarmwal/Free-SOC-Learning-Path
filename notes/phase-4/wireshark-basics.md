# Wireshark: The Basics

**Room:** [tryhackme.com/room/wiresharkthebasics](https://tryhackme.com/room/wiresharkthebasics)

Wireshark is the go-to tool for PCAP analysis. This room covers navigation, packet inspection, filtering, and extracting useful artifacts from captures.

---

## Tool Overview

Wireshark captures and dissects network traffic — you can load a saved `.pcap`/`.pcapng` file or capture live traffic directly.

Key things you can do:
- **Load PCAP files** — open saved captures for investigation
- **Colour packets** — Wireshark auto-colours traffic by protocol (green = TCP, dark blue = DNS, etc.) — helps spot traffic types at a glance
- **Traffic sniffing** — capture live from an interface
- **Merge PCAPs** — combine multiple capture files into one
- **View file details** — see capture metadata, SHA256 hash, comment, packet count

---

## Packet Dissection

Each packet is broken down into layers matching the TCP/IP model:

```
Frame          → physical layer details (size, timestamp)
Ethernet II    → MAC addresses (Link layer)
IP             → source/destination IPs, TTL (Internet layer)
TCP/UDP        → ports, flags, payload size (Transport layer)
HTTP/DNS/etc.  → actual application data (Application layer)
```

Clicking into any layer in the packet details pane expands its fields.

---

## Packet Navigation

- **Go to Packet** — jump directly to a packet number (`Ctrl+G`)
- **Find Packets** — search for a string/value across packet details, bytes, or hex (`Ctrl+F`)
- **Mark Packets** — highlight packets for reference without filtering
- **Packet Comments** — annotations added to specific packets in the capture
- **Export Objects** — extract files transferred over HTTP, SMB, FTP etc. directly from the capture (`File → Export Objects`)
- **Expert Info** — Wireshark's built-in analysis flagging errors, warnings, and notes across the capture (`Analyze → Expert Info`)
- **Time Display Format** — change how timestamps display (UTC, relative, epoch etc.)

---

## Packet Filtering

Wireshark has two filter types:
- **Capture filters** — applied before capturing, limits what gets recorded (BPF syntax)
- **Display filters** — applied after, hides/shows packets without discarding them (Wireshark syntax)

Common display filter patterns:
```
http                          # show only HTTP traffic
ip.addr == 10.0.0.1           # filter by IP
tcp.port == 443               # filter by port
http.request.method == "GET"  # filter by HTTP method
dns                           # show only DNS
```

Other useful filtering approaches:
- **Apply as Filter** — right-click any field → auto-builds the display filter for that value
- **Conversation Filter** — show all traffic between two specific endpoints
- **Follow Stream** — reassemble the full TCP/HTTP/UDP conversation in readable form (`Right-click → Follow → HTTP Stream`)
- **Apply as Column** — add any field as a column in the packet list for quick reference

---

## Lab Answers (Exercise.pcapng)

**File Details**
- Capture file flag (from comments): `THM{...}`
- Total packets: found in Statistics → Capture File Properties
- SHA256: from the same file properties view

**Packet 38 (HTTP packet dissection)**
- Markup language under HTTP: `eXtensible Markup Language` (XML)
- Arrival date: found in Frame layer
- TTL: found in IP layer
- TCP payload size: found in TCP layer
- e-tag value: found in HTTP response headers

**Packet Navigation**
- Searched "r4w" in packet details → found Artist 1's name
- Packet 12 comment: read directly from packet comments pane
- `.txt` file: extracted via `File → Export Objects → HTTP` → read the alien's name
- Expert Info warnings count: found in `Analyze → Expert Info → Warnings tab`

**Filtering**
- Packet 4 → right-click HTTP → Apply as Filter → query: `http`
- Displayed packets after filter: shown in the bottom status bar
- Packet 33790 → Follow HTTP Stream → total artists and second artist name found in the server's response body
