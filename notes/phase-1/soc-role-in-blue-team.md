# SOC Role in Blue Team

**Room:** [tryhackme.com/room/socroleinblueteam](https://tryhackme.com/room/socroleinblueteam)

Where does a SOC analyst sit in a company, who do they report to, and what does the path forward look like?

---

## Company Security Structure

Big companies don't just have a SOC — they have multiple security departments, each handling a different area. The SOC sits under the larger security org, which is all overseen by the CISO at the top.

---

## SOC Analyst Ladder

```
L1 → Alert triage, basic investigation, escalation
L2 → Deeper investigation, threat hunting, mentors L1
L3 / Lead → Complex cases, process improvement
Manager → Runs the team, reports to CISO
```

To move L1 → L2 you need: log analysis, SIEM proficiency, knowing when and how to escalate, and starting to understand attacker TTPs.

---

## Other Defensive Roles Worth Knowing

- **CIRT** — Called in for serious incidents SOC can't handle alone
- **Threat Intelligence Analyst** — Tracks adversaries and feeds IOCs to the SOC
- **Malware Analyst** — Reverse engineers suspicious files
- **Security Engineer** — Builds and maintains the tools the SOC uses
- **GRC Analyst** — Compliance, audits, policies — less technical but important

---

## Lab — CISO Simulation (TrySecureMe)

Given 7 simultaneous incidents across a multinational company and had to assign each one to the right team/role.

The point wasn't technical — it was about understanding *who owns what*. Sending a phishing incident to the wrong team wastes time and lets attackers stay longer.

Got all 7 right → flag.
