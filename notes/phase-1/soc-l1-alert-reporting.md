# SOC L1 Alert Reporting

**Room:** [tryhackme.com/room/socl1alertreporting](https://tryhackme.com/room/socl1alertreporting)

How to write proper alert reports, when and how to escalate, and how to communicate in tricky situations. Directly relevant to the SOC Simulator and SAL1 cert.

---

## Alert Reporting — The Five Ws

Every alert report should answer these:

- **Who** — which user logged in, ran the command, or downloaded the file
- **What** — the exact action or sequence of events
- **When** — when the suspicious activity started and ended
- **Where** — which device, IP, or website was involved
- **Why** — your reasoning for the final verdict (most important one)

**Lab:** wrote a report in the simulator following this format → got the flag.

---

## Escalation

When to escalate and how:

1. Move alert to **In Progress**, do your analysis
2. Write the alert report, set your verdict (e.g. True Positive)
3. If escalation needed, assign to L2 on shift
4. L2 gets notified and picks up from your report

Your report is what L2 works from — a bad report wastes their time and slows response down.

**Lab:** escalated an alert to L2 correctly → got the flag.

---

## Communication — Real Scenarios

These are the situations that catch L1s off guard:

**L2 is unavailable for 30+ minutes on a critical alert**
Don't wait. Call L2 → then L3 → then your manager. Know where emergency contacts are before you need them.

**Account compromise alert on Slack/Teams**
Don't message the user on the breached platform. Use an alternative — phone call, personal email. The attacker may be watching.

**Alert flood with criticals mixed in**
Prioritise by workflow, but immediately inform L2 about the volume. Don't silently drown.

**You realise you misclassified an alert days later**
Tell L2 immediately. Don't sit on it hoping it was nothing — threat actors can stay quiet for weeks before doing damage.

**SIEM logs aren't parsing correctly**
Don't skip the alert. Investigate what you can, then report the issue to L2 or the SOC engineer.
