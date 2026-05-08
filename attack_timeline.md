# Attack Timeline: Phishing to Beaconing

**Date:** 2026-05-15  
**Duration:** 52 minutes from delivery to containment

| Time | Event | Action Taken |
|------|-------|---------------|
| 10:00 AM | Email delivered to jdoe's inbox | None (alert not yet triggered) |
| 10:05 AM | jdoe opens attachment, runs JS script | None |
| 10:06 AM | PowerShell downloads payload.exe | None |
| 10:07 AM | Payload executes, makes outbound C2 connection | None |
| 10:10 AM | Defender alerts on malicious file (signature update) | SOC ticket created |
| 10:12 AM | Analyst begins triage | Investigating |
| 10:15 AM | Analyst confirms malicious activity | Isolated workstation via EDR |
| 10:18 AM | Terminated processes, quarantined file | Containment complete |
| 10:20 AM | Blocked C2 domain and IP at firewall | Eradication |
| 10:25 AM | User password reset, email removed | Recovery |
| 10:52 AM | Incident report drafted | Post-incident |

**Time to contain:** 15 minutes from alert  
**Time to eradicate:** 25 minutes total  
**Business impact:** None – endpoint isolated before lateral movement
