# Handy Splunk (SPL) Queries for SOC Triage

## 1. Find all failed logins for a specific user
```spl
index=winsecurity EventID=4625 TargetUserName=jdoe
| stats count by WorkstationName, SourceNetworkAddress
| sort - count
index=winsecurity EventID=4625
| stats count by SourceNetworkAddress
| where count > 10
| lookup geoip SourceNetworkAddress
index=endpoint process_name=powershell.exe
| search process_path=*Downloads* OR *Temp*
| table _time, host, user, process_commandline
index=sysmon EventCode=1
| join type=inner host, process_id [ search index=sysmon EventCode=3 | fields host, process_id, dest_ip ]
| table _time, host, user, image, commandline, dest_ip
index=* sourcetype=WinEventLog:Security
| search _time>=relative_time(now(), "-5m@m") _time<=now()
| sort _time

---

## 5. Phishing Playbook Snippet

**File:** `playbook_phishing.md`

```markdown
# Phishing Incident Response Playbook (SOC Tier 1)

**Objective:** Contain and eradicate phishing emails that have been delivered to user mailboxes.

---

## Triggers
- User reports suspicious email
- Email gateway alert (malicious URL/attachment)
- EDR alert from sandbox detonation

---

## Step 1: Initial Triage (5 min)
- [ ] Capture email subject, sender, recipient, timestamp.
- [ ] Check if user clicked any link or opened attachment.
- [ ] Determine if any payload executed (check EDR for process tree).

## Step 2: Containment (10 min)
- [ ] If not yet opened: delete email from mailbox (O365 Explorer or PowerShell).
- [ ] If opened: isolate workstation via EDR immediately.
- [ ] Block sender domain and any extracted URLs/IPs at firewall.

## Step 3: Investigation (30 min)
- [ ] Extract IOCs (hashes, domains, IPs).
- [ ] Scan endpoint for persistence (scheduled tasks, run keys).
- [ ] Check other mailboxes for same email.

## Step 4: Eradication & Recovery
- [ ] Remove malicious files/quarantine.
- [ ] Reset user password, revoke sessions.
- [ ] Reimage workstation if persistence found.

## Step 5: Post-Incident
- [ ] Write incident report (5 Ws).
- [ ] Suggest detection improvements (e.g., new Sigma rule).
