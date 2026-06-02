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
