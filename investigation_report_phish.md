# Incident Investigation Report: Phishing Email with Malicious Attachment

**Incident ID:** SOC-INV-2026-001  
**Date:** 2026-05-15  
**Analyst:** Chase Harvey  
**Severity:** High (potential ransomware delivery)

---

## Alert Details

- **Detection Source:** Microsoft Defender for Office 365 (O365)
- **Alert Name:** `Malicious attachment detected in email`
- **User Affected:** jdoe@botiumtoys.com
- **Email Subject:** "Urgent: Invoice #INV-4421"
- **Attachment:** `invoice_4421.zip` → extracted `invoice_4421.js`

---

## Triage & Investigation

| Step | Action | Finding |
|------|--------|---------|
| 1 | Checked email headers | Sender domain `payments-update.com` is 2 days old, SPF/DKIM fail |
| 2 | Sandboxed attachment | JS file executed PowerShell to download `payload.exe` from `hxxp://evil[.]com/update` |
| 3 | Checked user endpoint | Process tree: `outlook.exe` → `wscript.exe` → `powershell.exe` → `payload.exe` (suspicious) |
| 4 | Network logs | Outbound connection to `evil[.]com:443` at 10:32 AM, then beaconing every 60 seconds |
| 5 | Endpoint scans | `payload.exe` detected as `Trojan.Emotet` by Defender (signature updated 1 hour after first execution – so initial miss) |

**IOCs extracted:**
- File hash (JS): `b5c2e8f9a1d4...`
- File hash (EXE): `d7e3a9c2b5f1...`
- Domain: `evil[.]com`
- IP: `185.130.5.253`

---

## Containment & Eradication

- **Immediate:** Isolated user workstation via EDR (sent `isolate` command)
- **Removed:** Terminated malicious processes (`wscript.exe`, `powershell.exe`, `payload.exe`) via EDR
- **Quarantined:** Email removed from all mailboxes using O365 Explorer
- **Blocked:** Added domain and IP to firewall block list
- **User reset:** Password reset, forced logout of all sessions

---

## Lessons Learned

- **Defect:** Defender signature update lag allowed ~50 minutes of execution. Recommendation: Enable **block at first sight** + **ASR rules** to prevent script execution from Office macros.
- **Improvement:** Add email alert for first-time sender domains less than 7 days old.

**Status:** Resolved – no ransomware deployment or lateral movement detected.
