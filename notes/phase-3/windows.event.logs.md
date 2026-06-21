# Windows Event Logs

**Room:** [tryhackme.com/room/windowseventlogs](https://tryhackme.com/room/windowseventlogs)

Before jumping into a SIEM, you need to understand what Windows is actually logging natively and how to pull it manually. This room covers that foundation.

---

## Types of Event Logs

- **System** — OS-level events: hardware changes, drivers, system changes
- **Security** — logon/logoff activity, defined by audit policy. Main source for investigating unauthorized access
- **Application** — app errors, warnings, events
- **Directory Service** — Active Directory changes (mainly on domain controllers)
- **File Replication Service** — Group Policy and logon script syncing across domain controllers
- **DNS** — domain event logging on DNS servers
- **Custom** — app-defined logs with their own size/ACL settings

---

## Ways to Access Logs

1. **Event Viewer** — GUI tool
2. **wevtutil.exe** — command-line tool to query, export, archive, clear logs
3. **Get-WinEvent** — PowerShell cmdlet, most flexible for filtering

---

## Get-WinEvent Examples

```powershell
# List all logs
Get-WinEvent -ListLog *

# List providers
Get-WinEvent -ListProvider *

# Filter by provider
Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }

# Recommended: FilterHashtable (faster, cleaner)
Get-WinEvent -FilterHashtable @{
  LogName='Application'
  ProviderName='WLMS'
}

# Hunting encoded PowerShell / secrets in script block logs
Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-PowerShell/Operational'; ID=4104} | Select-Object -Property Message | Select-String -Pattern 'SecureString'
```

---

## XPath Queries

Used to query the event log XML directly with conditions.

```
*[System[(Level <= 3) and TimeCreated[timediff(@SystemTime) <= 86400000]]]
```
This pulls events with severity ≤ 3 in the last 24 hours.

---

## Event ID Reference Resources

Didn't memorise every event ID — instead noted where to look them up when needed:
- Windows Logging Cheat Sheet (older but still useful)
- NSA's "Spotting the Adversary with Windows Event Log Monitoring"
- Microsoft's "Events to Monitor" (AD security best practices)
- Microsoft's full Security Auditing and Monitoring Reference

---

## Lab — 4 Scenarios

**Scenario 1 — PowerShell downgrade attack**
PowerShell was approved org-wide, but visibility was needed. Investigated logging gaps.
- Event ID for downgrade attack: **400**
- Attack timestamp: **12/18/2020 7:50:33 AM**

**Scenario 2 — Log clearing detection**
Security team wanted visibility on cleared event logs.
- Log clear event recorded under Record ID: **27736**
- Computer name: **PC01.example.corp**

**Scenario 3 — Emotet encoded PowerShell payload**
Threat intel pointed to Event ID 4104 with "ScriptBlockText" — found the encoded payload.
- First variable name in the script: **$Va5w3n8**
- Attack timestamp: **8/25/2020 10:09:28 PM**
- Execution Process ID: **6620**

**Scenario 4 — Suspicious enumeration via net1.exe**
Intern suspected of enumerating Administrators group members.
- Group Security ID enumerated: **S-1-5-32-544**
- Event ID confirming it: **4799**

---

## Key Lesson

Event IDs alone don't tell the full story — context (process, timestamp, account, command line) is what turns a log entry into an actual finding. 4104, 400, and 4799 specifically are worth remembering since they come up constantly in PowerShell abuse and group enumeration investigations.
