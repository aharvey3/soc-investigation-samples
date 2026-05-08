# SOC Investigation Samples – Chase Harvey

This repository contains **realistic, anonymized artifacts** from Security Operations Center (SOC) work:  
detection rules, investigation reports, queries, and playbooks.

**Role context:** Tier 1/2 SOC Analyst, Detection Engineer, Incident Responder

---

## Contents

| File | What it shows |
|------|----------------|
| `investigation_report_phish.md` | Full investigation of a phishing email leading to malware |
| `sigma_rule_susp_process.yml` | Sigma detection rule for unusual process creation |
| `splunk_queries.md` | Handy SPL queries for hunting & alert triage |
| `playbook_phishing.md` | Step-by-step response playbook for phishing incidents |
| `attack_timeline.md` | Timeline from initial alert to containment |

---

## Why this matters

SOC teams need analysts who can:
- **Triage alerts** quickly and accurately
- **Write detection logic** (Sigma, SPL, KQL)
- **Document investigations** clearly
- **Follow playbooks** and suggest improvements

These samples demonstrate all of the above.

---

## How to use

- Review the investigation report to understand my thought process.
- Try running the Sigma rule in your own lab (e.g., with Elastic or Splunk).
- Use the playbook as a template for your own team.

Questions or feedback? Open an issue or reach out.
