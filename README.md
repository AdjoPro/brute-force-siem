# brute-force-siem
SIEM use case for detecting brute-force login attempts and generating alerts with detailed documentation
# Brute-force Attack Detection - SIEM Use Case

## Project Overview
This project demonstrates how to detect brute-force login attempts using a SIEM (Splunk). The goal is to identify multiple failed login attempts from a single IP address within a short time frame and generate actionable alerts for further investigation.

## SIEM Platform
- Platform: Splunk 
- Data Source: Linux SSH Logs (`/var/log/auth.log`) 

## Use Case Details
- **Log Source:** SSH Authentication Logs
- **Attack Pattern:** Multiple failed login attempts within a short period (e.g., 5 failed attempts in 1 minute).
- **Detection Criteria:** IP address with more than 5 failed attempts.
- **Alert Action:** Send an email alert and generate an investigation ticket.

## Splunk Search Query
```spl
index=auth_logs sourcetype=linux_secure
"Failed password" | stats count by src_ip
| where count > 5
