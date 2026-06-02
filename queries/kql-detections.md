# KQL Detection Queries

This file contains KQL queries used to detect suspicious web activity in Apache logs.
# KQL Detection Queries

This file contains the main KQL queries used during the web security monitoring investigation in Kibana.

## 1. Reconnaissance Scanning

This query detects requests to suspicious or sensitive web paths that are commonly checked during reconnaissance.

`message: "/admin" OR message: "/phpmyadmin" OR message: "/.env" OR message: "/wp-admin" OR message: "/.git"`

Purpose:

* Find requests to hidden or administrative paths
* Detect possible scanning activity
* Identify suspicious 404 responses caused by probing

## 2. Brute-Force Login Attempts

This query detects repeated requests to the login page.

`message: "login.php"`

This query can be used to focus on login attempts with the admin username.

`message: "login.php" AND message: "admin"`

Purpose:

* Find repeated login attempts
* Identify automated password guessing
* Detect suspicious activity against the login endpoint

## 3. Injection and Path Traversal

This query detects SQL injection, XSS, and path traversal payloads.

`message: "UNION" OR message: "script" OR message: "../" OR message: "etc/passwd"`

Purpose:

* Detect SQL injection keywords such as `UNION`
* Detect XSS payloads containing `script`
* Detect path traversal attempts using `../`
* Detect attempts to access `/etc/passwd`

## 4. Hidden File Probing

This query detects attempts to access hidden files and directories.

`message: ".env" OR message: ".git"`

Purpose:

* Detect probing for sensitive configuration files
* Identify attempts to access hidden directories
* Investigate possible reconnaissance activity

## 5. Suspicious User-Agent

This query detects requests from automated tools.

`message: "curl" OR message: "Nikto"`

Purpose:

* Detect scripted requests
* Identify web scanner activity
* Separate automated traffic from normal browser activity

## Summary

These KQL queries helped identify three main types of suspicious web activity:

* Reconnaissance scanning
* Brute-force login attempts
* Injection and path traversal attempts
