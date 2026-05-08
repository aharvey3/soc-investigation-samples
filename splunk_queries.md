# Handy Splunk (SPL) Queries for SOC Triage

## 1. Find all failed logins for a specific user
```spl
index=winsecurity EventID=4625 TargetUserName=jdoe
| stats count by WorkstationName, SourceNetworkAddress
| sort - count
