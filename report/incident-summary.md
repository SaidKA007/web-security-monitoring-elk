# Incident Summary

## Scenario

A local Apache web server was monitored using Filebeat, Elasticsearch, and Kibana. The purpose of this lab was to simulate common web attacks and investigate them using Apache logs in a SIEM environment.

The attacks were performed only against a local test environment.

## Tools Used

* Kali Linux
* Apache Web Server
* Filebeat
* Elasticsearch
* Kibana
* KQL
* curl
* Nikto

## Incidents Investigated

| Incident                     | Description                                                                           | Evidence                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Reconnaissance Scanning      | Requests to sensitive paths such as `/admin`, `/.env`, `/phpmyadmin`, and `/.git`     | Multiple suspicious requests and 404 responses            |
| Brute-Force Login            | Repeated requests to `login.php` with the same username and different password values | Many login attempts in a short time                       |
| Injection and Path Traversal | SQL injection, XSS, and path traversal payloads sent to the web application           | `UNION`, `script`, `../`, and `/etc/passwd` found in logs |

## Findings

The simulated attacks were successfully captured in Apache access logs and investigated in Kibana.

Reconnaissance activity was identified by requests to hidden or administrative paths. These requests are suspicious because normal users usually do not visit paths such as `/.env`, `/.git`, or `/phpmyadmin`.

Brute-force activity was identified by repeated requests to `login.php`. The requests used the same username but different password values, which indicates automated password guessing.

Injection and path traversal activity was identified by suspicious payloads in URL parameters. The logs contained SQL injection keywords, XSS-related strings, and path traversal patterns.

## Verdict

The activity should be treated as suspicious. In a real SOC environment, these events would require further investigation, alert triage, and possible escalation.

## Recommendations

* Monitor repeated 404 responses from the same source.
* Alert on suspicious paths such as `.env`, `.git`, `/admin`, and `/phpmyadmin`.
* Detect SQL injection and XSS payloads in URL parameters.
* Monitor repeated login attempts to authentication endpoints.
* Apply rate limiting to login pages.
* Use WAF rules to block common web attack patterns.
* Review suspicious user agents such as `curl` and `Nikto`.
