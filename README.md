# Cyber Security Task 1: Website Vulnerability Assessment Report

[![Internship](https://img.shields.io/badge/Internship-Future%20Interns-blue)](https://futureinterns.com/)
[![Task](https://img.shields.io/badge/Task-Task%201%20(2026)-orange)](#)
[![Scope](https://img.shields.io/badge/Scope-Read--Only%20%2F%20Passive-green)](#)

---

## Executive Summary

This repository contains the vulnerability assessment report and supporting evidence prepared for **Future Interns Cyber Security Task 1 (2026)**.

The objective was to conduct a read-only assessment of a public-facing web application, document observed configuration weaknesses, assign risk levels, and provide remediation guidance.

## Target and Scope

- **Target:** `testphp.vulnweb.com` — Acunetix public test environment
- **Assessment type:** Read-only passive vulnerability audit
- **Assessment date:** October 2026
- **Role:** Cyber Security Intern

### Scope and Ethical Guidelines

The assessment was limited to passive, read-only checks.

| In Scope | Out of Scope |
| --- | --- |
| Public page inspection | Authentication bypass attempts |
| Passive vulnerability scanning | Vulnerability exploitation |
| HTTP response header analysis | Automated brute-force attacks |
| Open port and service detection | Denial-of-service testing |

## Tools and Methodology

1. **Browser developer tools** — Inspected HTTP response headers, cookie security flags, and client-side configuration.
2. **Nmap** — Identified publicly reachable web ports and service versions using `nmap -sV -F testphp.vulnweb.com`.
3. **OWASP ZAP (passive scan)** — Checked for missing security headers, cookie flags, and passive configuration weaknesses.
4. **Canva** — Formatted the assessment report for non-technical readers.

## Findings Summary

| Finding ID | Weakness | Severity | Category | Status |
| --- | --- | --- | --- | --- |
| **V-01** | Missing Content Security Policy (CSP) | Medium | Security header | Documented |
| **V-02** | Missing HTTP Strict Transport Security (HSTS) | Medium | Transport security | Documented |
| **V-03** | Missing clickjacking protection | Low | Security header | Documented |
| **V-04** | Web server version and banner disclosure | Low | Information disclosure | Documented |

## Detailed Findings and Remediation

### V-01: Missing Content Security Policy (CSP)

- **Severity:** Medium
- **Description:** The web server did not provide a `Content-Security-Policy` HTTP header.
- **Business impact:** Without a restrictive policy, the browser has fewer controls over which sources can load scripts and other resources. This can increase the impact of certain injection vulnerabilities.
- **Remediation:** Define and test a Content Security Policy that allows only the resources the application requires. For example:

  ```http
  Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.example
