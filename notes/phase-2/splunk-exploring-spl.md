# Splunk: Exploring SPL

**Room:** [tryhackme.com/room/splunkexploringspl](https://tryhackme.com/room/splunkexploringspl)

SPL (Search Processing Language) is how you actually talk to Splunk. Everything in a SOC investigation — filtering, correlating, visualising — runs through SPL.

---

## Basic Search

Searches in Splunk run against an index and filter by keywords or field values.

```
index="vpn_logs" username="john"
```

Search & Reporting App is where you write and run all queries. Results come back as events you can drill into.

---

## Search Operators & Order of Evaluation

Operators let you combine conditions:

```
index="logs" status="failed" AND src_ip="10.0.0.1"
index="logs" status="failed" OR status="blocked"
index="logs" NOT user="admin"
```

Order of evaluation: `NOT` → `AND` → `OR` — use brackets when in doubt to force the order you want.

---

## Filtering Commands

**fields** — keep or remove specific fields from results
```
| fields src_ip, username, action
| fields - _raw
```

**dedup** — remove duplicate events based on a field
```
| dedup username
```

**rename** — rename a field for readability
```
| rename src_ip as "Source IP"
```

**regex** — filter events using a regular expression
```
| regex username="^admin.*"
```

---

## Structuring Results

**table** — display results as a clean table with only the columns you want
```
| table _time, username, src_ip, action
```

**Timelining with table** — include `_time` as first column to reconstruct event sequences chronologically. Useful for building attack timelines.

**Subsearches** — run a search inside another search. Inner search runs first, its result feeds into the outer search.
```
index="logs" [search index="watchlist" | fields username]
```
Useful for things like "show me all events from users on my watchlist."

---

## Transforming Commands

These turn raw events into statistics and visualisations.

```
| stats count by username
| stats count by src_ip, action
| top limit=10 src_ip
| rare username
```

**Data enrichment and field manipulation:**
```
| eval risk_score = if(action="failed", 1, 0)
| rex field=_raw "user=(?<username>\w+)"
```

`eval` creates new fields from logic. `rex` extracts fields from raw text using regex — useful when Splunk hasn't auto-extracted what you need.

---

## Anomaly Detection

**Outliers by Country** — spot logins from countries that never appear in normal traffic
```
| stats count by country | sort - count
```

**Outliers by Hour** — find activity happening at unusual times
```
| stats count by date_hour | sort - count
```

**Impossible Travel** — user logs in from London then Mumbai 10 minutes later. Physically impossible, likely account compromise.
```
| stats earliest(_time) as first, latest(_time) as last, values(country) as countries by username
```

**ML-based detection** — Splunk's `anomalydetection` and `| fit` commands can baseline normal behaviour and flag deviations automatically — more advanced, reduces manual rule writing.

---

## Lab Summary

Each section had a lab applying the commands to real log data:
- Basic search — found events by filtering on fields
- Operators — combined conditions to narrow results
- Filtering commands — cleaned up and shaped the output
- Structuring — built readable tables and timelines
- Transforming — ran stats across events to spot patterns
- Anomaly detection — identified suspicious outliers in login data
