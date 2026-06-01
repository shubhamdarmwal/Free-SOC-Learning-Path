# Splunk: The Basics

**Room:** [tryhackme.com/room/splunk101](https://tryhackme.com/room/splunk101)

Splunk is one of the most widely used SIEMs in enterprise SOCs. This room covers how it's built, how to navigate it, and how logs actually get into it.

---

## Splunk Components

**Forwarder** — installed on endpoints and servers, collects logs and ships them to the indexer. Lightweight, runs in the background.

**Indexer** — receives the logs, processes them, and stores them in a searchable format. This is where your data lives.

**Search Head** — the UI you interact with. Sends search queries to the indexer and displays results. What analysts use day-to-day.

```
Endpoint (Forwarder) → Indexer → Search Head (Analyst)
```

---

## Navigating Splunk

The main areas in the UI:
- **Search & Reporting** — where you write SPL queries and investigate
- **Dashboards** — visual overviews built from saved searches
- **Alerts** — rules that fire when search conditions are met
- **Settings** — manage inputs, indexes, users

---

## Adding Data

Splunk can ingest logs in multiple ways — uploading files directly, monitoring a folder, or receiving from a forwarder. Once ingested, Splunk parses the logs and makes them searchable by fields like source, sourcetype, and host.

**Lab:** uploaded a VPN log file into Splunk manually following these steps:

1. **Select Source** — chose the VPN_logs file as the data source
2. **Select Source Type** — told Splunk what format the logs are in (e.g. JSON, syslog) so it parses them correctly
3. **Input Settings** — picked which index to store the logs in and set the hostname to associate with them
4. **Review** — confirmed all settings before committing
5. **Done** — logs uploaded and immediately searchable

Once ingested, ran searches against the VPN logs to analyse the data — filtering by fields Splunk automatically extracted from the log format.
