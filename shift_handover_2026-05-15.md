# SOC Shift Handover Report

**Shift:** Day (08:00 – 17:00)  
**Analyst:** Chase Harvey  
**Date:** 2026-05-15  
**Next Shift Analyst:** Taylor Chen

---

## Open Incidents

| Incident ID | Severity | Summary | Status | Actions Taken | Handoff Notes |
|-------------|----------|---------|--------|---------------|----------------|
| SOC-101 | High | Phishing with malware attachment (jdoe) | Contained, awaiting user reimage | Isolated host, removed email, blocked IOCs | User not yet reimaged – follow up with help desk ticket #4421 |
| SOC-102 | Medium | Multiple failed logins from 185.130.5.253 | Investigation ongoing | IP blocked, user MFA confirmed working | Need to check if this IP appears in other logs (sentinel queries ready) |
| SOC-103 | Low | False positive – internal scan triggered web filter | Closed | Whitelisted internal scanner IP | None |

---

## Metrics for Today

| Metric | Count |
|--------|-------|
| New alerts | 47 |
| False positives | 31 |
| True positives | 16 |
| Incidents escalated | 3 |
| Average time to triage | 8 minutes |

---

## Notable Events

- **10:32 AM** – Defender signature delay allowed ~50 min execution of Emotet. Logged as detection gap.
- **14:15 PM** – Firewall upgrade caused 2-minute logging gap. Confirmed no missed alerts.

---

## Intelligence Notes

- New C2 domain observed: `evil-update[.]ru` – added to block list.
- MS-ISAC alert: Increased Qakbot activity targeting manufacturing. We have no manufacturing assets.

---

## TODOs for Next Shift

- [ ] Confirm user jdoe workstation is reimaged.
- [ ] Run hunting query for `evil-update[.]ru` across last 7 days.
- [ ] Review updated Sigma rule (PR #42) and test in staging.
