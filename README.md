# FUTURE_CS_01 — Vulnerability Assessment Report
### Prepared by: Angel Proshia F
### Future Interns | Cyber Security Track | Task 1 | June 2026

---

## Task Overview
A professional, read-only vulnerability assessment of a public web application,
conducted as part of the **Future Interns Cyber Security internship programme**.
The goal is to identify common security weaknesses, classify risks by severity,
and present actionable findings in a business-friendly audit report.

---

## Website Tested

| Field | Details |
|-------|---------|
| **Target** | OWASP Juice Shop |
| **URL** | https://demo.owasp-juice.shop |
| **Version** | v20.0.0 (May 2026) |
| **Type** | Intentionally vulnerable web application — OWASP Foundation training target |
| **Tech Stack** | Node.js 24.x, Express ^4.22.1, Angular |
| **Assessment Date** | Fri, 12 June 2026 |
| **Prepared By** | Angel Proshia F |
| **Report ID** | FUTURE-CS-01-2026 |
| **Classification** | Confidential |

> **OWASP Juice Shop** is a deliberately vulnerable application maintained by
> the OWASP Foundation specifically for security training. It is a fully legal
> and ethical target for this assessment.

---

## Scope

### In Scope
- Public-facing pages only
- HTTP response header analysis (curl + DevTools)
- Cookie attribute inspection (DevTools Application tab)
- JWT token storage inspection (DevTools Local Storage)
- API endpoints observable during normal browsing
- Passive scanner alerts (OWASP ZAP automated scan — passive only)

### Out of Scope
- Login bypass or authentication exploitation
- Brute force attacks
- Denial-of-Service (DoS)
- Any active exploitation or data modification
- Any activity that harms or disrupts the application

---

## Tools Used

| Tool | Version | How It Was Used |
|------|---------|----------------|
| **OWASP ZAP** | 2.15 by Checkmarx | Automated passive scan — spider + alert detection only |
| **Browser DevTools** | Chrome | Network tab, Application tab (cookies, local storage) |
| **curl** | 8.x (Windows CMD) | `curl -k -I https://demo.owasp-juice.shop/` — header capture |
| **jwt.io** | Web tool | JWT token decoding and inspection (read-only) |

---

## Findings Summary

| ID | Vulnerability | Severity | CVSS | OWASP Category | Status |
|----|--------------|----------|------|----------------|--------|
| VULN-01 | SQL Injection in Product Search | 🔴 CRITICAL | 9.8 | A03:2021 Injection | Open |
| VULN-02 | Broken Authentication — Weak JWT Secret | 🟠 HIGH | 8.1 | A07:2021 Auth Failures | Open |
| VULN-03 | Reflected Cross-Site Scripting (XSS) | 🟠 HIGH | 7.4 | A03:2021 Injection | Open |
| VULN-04 | Missing HTTP Security Headers | 🟡 MEDIUM | 5.4 | A05:2021 Misconfiguration | Open |
| VULN-05 | Sensitive Data Exposure via API | 🟡 MEDIUM | 6.5 | A02:2021 Data Exposure | Open |
| VULN-06 | Insecure Cookies — No Secure/HttpOnly | 🟢 LOW | 3.7 | A05:2021 Misconfiguration | Open |
| VULN-07 | Verbose Tech Disclosure via Headers & Errors | 🟢 LOW | 3.1 | A05:2021 Misconfiguration | Open |

**Overall Risk Rating: 🔴 HIGH**

---

## Real Evidence Captured (12 June 2026)

### From curl -k -I https://demo.owasp-juice.shop/
| Header | Value | Finding |
|--------|-------|---------|
| Content-Security-Policy | ❌ MISSING | VULN-04 |
| Strict-Transport-Security | ❌ MISSING | VULN-04 |
| Referrer-Policy | ❌ MISSING | VULN-04 |
| Access-Control-Allow-Origin | ⚠️ Wildcard `*` | VULN-04 |
| X-Frame-Options | ✅ SAMEORIGIN | Safe |
| X-Content-Type-Options | ✅ nosniff | Safe |
| Server | ⚠️ Heroku | VULN-07 |
| X-Recruiting | ⚠️ /#/jobs | VULN-07 |

### From OWASP ZAP — 9 Alerts Found
| # | Alert | Risk |
|---|-------|------|
| 1 | Content Security Policy (CSP) Header Not Set | Medium |
| 2 | Cross-Domain Misconfiguration | Medium |
| 3 | Server Leaks Version Information via "Server" Header | Medium |
| 4 | Strict-Transport-Security Header Not Set | Medium |
| 5 | Timestamp Disclosure - Unix | Low |
| 6 | Information Disclosure - Suspicious Comments | Low |
| 7 | Modern Web Application | Info |
| 8 | Re-examine Cache-control Directives | Info |
| 9 | User Agent Fuzzer | Info |

### From Browser DevTools
| Observation | Finding |
|-------------|---------|
| JWT token stored in Local Storage (key: `token`) | VULN-02 |
| Email stored in plain text in Local Storage | VULN-02 |
| Cookies (continueCode, cookieconsent, language, welcomebanner) — no HttpOnly or Secure flags | VULN-06 |
| `/api/Users` returns 401 with `Express ^4.22.1` version disclosed in error page | VULN-07 |
| `Access-Control-Allow-Origin: *` on API endpoint | VULN-04 |

---

## Repository Structure

```
FUTURE_CS_01/
│
├── README.md                              ← This file
│
├── report/
│   └── Vulnerability_Assessment_Report_FUTURE_CS_01.pdf
│
├── evidence/
│   ├── headers_curl_output.txt            ← Real curl output from 12 Jun 2026
│   ├── zap_passive_scan_alerts.md         ← All 9 ZAP alerts with details
│   └── api_users_response.md              ← API endpoint observation notes
│
└── screenshots/
    ├── README.md                          ← Screenshot index and descriptions
    ├── 01_devtools_response_headers.png
    ├── 02_target_homepage.png
    ├── 03_devtools_cookies.png
    ├── 04_devtools_jwt_token.png
    ├── 05_api_users_version_disclosure.png
    ├── 06_curl_headers_output.png
    ├── 07_zap_alerts_overview.png
    ├── 08_zap_csp_alert_detail.png
    └── 09_zap_scan_results.png
```

---

## Report

**[Download Full Report PDF](report/Vulnerability_Assessment_Report_FUTURE_CS_01.pdf)**

The PDF report includes:
- Cover page with risk summary (1 Critical, 2 High, 2 Medium, 2 Low)
- Table of contents
- Executive summary
- Full scope and methodology
- Findings summary table
- 7 detailed vulnerability findings with CVSS scores, business impact, and remediation steps
- Risk overview and distribution
- 4-phase remediation roadmap with timelines
- Ethics and disclaimer statement

---

## Ethics Statement

This assessment was conducted **solely for educational purposes** as part of
the Future Interns Cyber Security Task 1 programme.

- Read-only, passive scanning only — no active scan performed
- No exploits executed against the application
- No application data modified or exfiltrated
- No brute-force or denial-of-service techniques used
- Target is an officially designated OWASP security training application
- Full compliance with Future Interns Task 1 ethical guidelines

---

## Author

| Field | Details |
|-------|---------|
| **Name** | Angel Proshia F |
| **Programme** | Future Interns — Cyber Security Track |
| **Task** | Task 1 — Vulnerability Assessment Report |
| **Track Code** | CS |
| **Repository** | FUTURE_CS_01 |
| **Date** | June 2026 |

---

*This report is for educational purposes only. All findings relate to an
intentionally vulnerable training application maintained by the OWASP Foundation.*
