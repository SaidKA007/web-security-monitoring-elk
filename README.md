# web-security-monitoring-elk
Web security monitoring lab using Apache logs, Filebeat, Elasticsearch, Kibana, and KQL detections.

# Web Security Monitoring with ELK Stack

## Overview

This project is a hands-on SOC lab focused on detecting web attacks using Apache logs and the ELK Stack.

The lab simulates suspicious HTTP activity against a local Apache web server, collects logs with Filebeat, stores them in Elasticsearch, and investigates the events in Kibana using KQL queries.
# Web Security Monitoring with ELK Stack

## Overview

This project is a hands-on SOC lab focused on detecting web attacks using Apache logs and the ELK Stack.

The lab simulates suspicious HTTP activity against a local Apache web server, collects logs with Filebeat, stores them in Elasticsearch, and investigates the events in Kibana using KQL queries.

## Lab Architecture

```text
Attacker / Test Machine
        |
        | HTTP requests
        v
Apache Web Server
        |
        | access.log / error.log
        v
Filebeat
        |
        v
Elasticsearch
        |
        v
Kibana
        |
        v
SOC Analyst Investigation
```text

````markdown
```
Tools Used
Kali Linux
Apache Web Server
PHP
Filebeat
Elasticsearch
Kibana
Docker
KQL
curl
Nikto
Attack Scenarios Simulated
1. Reconnaissance Scanning

Nikto and manual requests were used to simulate web reconnaissance. The goal was to identify suspicious requests to hidden or sensitive paths such as:

/admin
/.env
/.git/config
/backup.zip
/phpmyadmin
2. Brute-Force Login Attempts

Repeated login requests were sent to the login.php endpoint using different password values. This simulates automated password guessing against a web login form.

3. Injection and Path Traversal Attempts

The lab includes detection of suspicious payloads such as:

SQL injection patterns
UNION SELECT attempts
XSS payloads
Path traversal attempts
Requests targeting /etc/passwd
Example Detection Logic

Suspicious activity was identified by looking for:

High number of requests from one source
Many 404 responses in a short time
Requests to hidden files
SQL keywords in URL parameters
XSS script tags
Path traversal sequences
Repeated login attempts
Example KQL Queries

Detect SQL injection:

message: "*UNION*"

Detect hidden file probing:

message: "*.env*"

Detect path traversal:

message: "*../*"

Detect XSS payloads:

message: "*<script>*"

Detect login attempts:

message: "*login.php*" and message: "*admin*"
Investigation Questions

During the investigation, the following SOC questions were answered:

When did the attack start and end?
What source IP generated the suspicious traffic?
Which paths or parameters were targeted?
How many requests were sent?
Did any suspicious request return HTTP 200 OK?
Which activity should be escalated?
Defensive Analysis

The lab also discusses defensive controls such as:

Web Application Firewall rules
Rate limiting
Fail2Ban
Detection tuning
Blocking suspicious request patterns
Key Takeaways

This project helped me practice:

Web log analysis
SIEM investigation workflow
KQL query writing
Web attack detection
Basic SOC triage
Incident timeline building
Defensive thinking for web security monitoring
