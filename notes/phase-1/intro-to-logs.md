# Intro to Logs

**Room:** [tryhackme.com/room/introtologs](https://tryhackme.com/room/introtologs)

Logs are the backbone of everything a SOC does. No logs = no visibility = flying blind.

---

## Why Logs Matter

When something happens on a network or system, logs are what answer:

- What happened?
- When did it happen?
- Where did it happen?
- Who is responsible?
- Were their actions successful?
- What was the result?

Without logs, incident response is basically guesswork.

---

## Log Types, Formats & Standards

Different systems produce different log types — OS logs, application logs, network logs, auth logs etc. They come in different formats (plain text, JSON, XML, CEF, LEEF) and there are standards like syslog that help normalize them so tools can actually parse them consistently.

---

## Log Collection, Management & Centralisation

Logs sitting on individual machines are useless at scale. You need to collect them, ship them to a central location (like a SIEM), and manage them from there. Covered the different ways to do this — agents, syslog forwarding, API-based collection.

---

## Log Storage, Retention & Deletion

Logs can't be kept forever — storage costs money. Organizations define retention policies (e.g. 90 days, 1 year) based on compliance requirements. Also learned how logs can be tampered with or deleted by attackers to cover their tracks, which is why log integrity matters.

---

## Lab — Log Analysis Process

Hands-on with actual log analysis — using tools and techniques to go through logs, spot anomalies, and identify adversary activity. The process is basically: collect → normalize → filter → correlate → investigate.
