FUTURE_CS_01 — Vulnerability Assessment Report
Future Interns | Cyber Security Track | Task 1


## Task Overview
A professional, read-only vulnerability assessment of a public web application, conducted as part of the **Future Interns Cyber Security internship programme**. The goal is to identify common security weaknesses, classify risks, and present actionable findings in a business-friendly audit report.

---

## Website Tested

| Field | Details |
|-------|---------|
| **Target** | [OWASP Juice Shop](https://demo.owasp-juice.shop) |
| **URL** | https://demo.owasp-juice.shop |
| **Version** | v20.0.0 (May 2026) |
| **Type** | Intentionally vulnerable web app — OWASP Foundation training target |
| **Stack** | Node.js 24.x, Express, Angular |
| **Purpose** | Ethical security testing / education only |
| **Assessment Date** | June 2026 |
| **Prepared By** | Angel Proshia F |
| **Report ID** | FUTURE-CS-01-2026 |

**OWASP Juice Shop** is a deliberately vulnerable application maintained by the OWASP Foundation specifically for security training. It is a safe and legal target for this assessment.

---

## Scope

### In Scope
- Public-facing pages only
- HTTP response header analysis
- Cookie attribute inspection
- Client-side source code review (Browser DevTools)
- API endpoints observable during normal browsing
- Passive scanner alerts (OWASP ZAP)

### Out of Scope
- Login bypass / authentication exploitation
- Brute force attacks
- Denial-of-Service (DoS)
- Any active exploitation or data modification
- Any activity that harms or disrupts the application

---

## Tools Used

| Tool | Version | Usage |
|------|---------|-------|
| **OWASP ZAP** | 2.15 | Passive scan — spider + alert detection only |
| **Browser DevTools** | Chrome 125 | Headers, cookies, local storage, network tab |
| **curl** | 8.x | HTTP response header capture (`curl -I`) |
| **jwt.io** | Web | JWT token decoding and inspection (read-only) |
| **Nmap** | 7.94 | Light service fingerprinting (read-only) |

---

## Findings Summary

| ID | Vulnerability | Severity | CVSS | OWASP Category |
|----|--------------|----------|------|----------------|
| VULN-01 | SQL Injection in Product Search | 🔴 CRITICAL | 9.8 | A03:2021 Injection |
| VULN-02 | Broken Authentication — Weak JWT Secret | 🟠 HIGH | 8.1 | A07:2021 Auth Failures |
| VULN-03 | Reflected Cross-Site Scripting (XSS) | 🟠 HIGH | 7.4 | A03:2021 Injection |
| VULN-04 | Missing HTTP Security Headers | 🟡 MEDIUM | 5.4 | A05:2021 Misconfiguration |
| VULN-05 | Sensitive Data Exposure via API | 🟡 MEDIUM | 6.5 | A02:2021 Data Exposure |
| VULN-06 | Insecure Cookies — No Secure/HttpOnly | 🟢 LOW | 3.7 | A05:2021 Misconfiguration |
| VULN-07 | Verbose Server Banner / Tech Disclosure | 🟢 LOW | 3.1 | A05:2021 Misconfiguration |

**Overall Risk Rating: 🔴 HIGH**

---

## 📁 Repository Structure

```
FUTURE_CS_01/
│
├── README.md
│
├── report/
│   └── Vulnerability_Assessment_Report_FUTURE_CS_01.pdf
│
├── evidence/
│   ├── headers_curl_output.txt
│   ├── zap_passive_scan_alerts.md
│   └── api_users_response.md
│
└── screenshots/
    └── (your tool screenshots here)
```

---

## Final Report

**[ Download Report PDF](report/Vulnerability_Assessment_Report_FUTURE_CS_01.pdf)**

The report includes:
- Cover page with risk summary badges
- Table of contents
- Executive summary
- Scope & methodology
- Findings summary table (all 7 vulnerabilities)
- Detailed findings with CVSS scores, impact, and remediation
- Risk overview and distribution
- Remediation roadmap with timelines
- Ethics and disclaimer statement

---

## Ethics Statement

This assessment was conducted **solely for educational purposes** as part of the Future Interns programme.

- Read-only, passive scanning only — no active scan performed
- No exploits executed
- No data modified or exfiltrated
- No brute-force or DoS techniques used
- Target is an officially designated security training application
- Full compliance with Future Interns Task 1 ethical guidelines

---

## Author

**Angel Proshia F**
Future Interns — Cyber Security Track
Task 1 | June 2026
Track Code: `CS` | Repository: `FUTURE_CS_01`

---

*This report is for educational purposes only. All findings relate to an intentionally vulnerable training application maintained by the OWASP Foundation.*
