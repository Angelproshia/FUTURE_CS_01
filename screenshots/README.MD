# Screenshots — Evidence Index
**Tester:** Angel Proshia F  
**Target:** https://demo.owasp-juice.shop  
**Date:** Fri, 12 Jun 2026  
**Tools Used:** Browser DevTools (Chrome), OWASP ZAP 2.15, curl (Windows CMD)  

---

## All 9 Screenshots

---

### 01_devtools_response_headers.png
**Tool:** Browser DevTools — Network Tab  
**What It Shows:** HTTP response headers captured from the Juice Shop homepage.
Confirms presence of `Server: Heroku`, `X-Recruiting: /#/jobs`,
`X-Frame-Options: SAMEORIGIN`, `X-Content-Type-Options: nosniff`,
and the `Reporting-Endpoints` header disclosing Heroku infrastructure.  
**Finding:** VULN-04, VULN-07  

---

### 02_target_homepage.png
**Tool:** Chrome Browser  
**What It Shows:** OWASP Juice Shop homepage fully loaded at
`https://demo.owasp-juice.shop` — confirms the target website
was accessible and in scope for assessment.  
**Finding:** Scope confirmation  

---

### 03_devtools_cookies.png
**Tool:** Browser DevTools — Application Tab → Cookies  
**What It Shows:** Four cookies set by the application:
`continueCode`, `cookieconsent`, `language`, and `welcomebanner`.
The `HttpOnly` and `Secure` columns are completely blank,
confirming neither flag is set on any cookie.
The `SameSite` attribute is also absent.  
**Finding:** VULN-06 — Insecure Cookies  

---

### 04_devtools_jwt_token.png
**Tool:** Browser DevTools — Application Tab → Local Storage  
**What It Shows:** Local Storage at `https://demo.owasp-juice.shop`
contains two keys — `email` (value: `test123@gmail.com`) and
`token` (value: a full JWT string starting with `eyJ0eXAiOiJKV1Qi...`).
Storing JWT tokens in Local Storage makes them accessible to
any JavaScript on the page, amplifying XSS risk.  
**Finding:** VULN-02 — Broken Authentication / Weak JWT  

---

### 05_api_users_version_disclosure.png
**Tool:** Browser DevTools — Network Tab + Direct URL visit  
**What It Shows:** Visiting `https://demo.owasp-juice.shop/api/Users`
returned HTTP `401 Unauthorized` with the error message
`UnauthorizedError: No Authorization header was found`.
The error page itself discloses `OWASP Juice Shop (Express ^4.22.1)` —
revealing the exact framework name and version number.
DevTools Network tab confirms the endpoint is reachable and
`Access-Control-Allow-Origin: *` is set in response headers.  
**Finding:** VULN-05 — Sensitive Data Exposure, VULN-07 — Tech Disclosure  

---

### 06_curl_headers_output.png
**Tool:** curl (Windows Command Prompt)  
**Command Run:** `curl -k -I https://demo.owasp-juice.shop/`  
**What It Shows:** Full HTTP response headers captured from command line.
Confirms:
- `Server: Heroku` — platform disclosed
- `Access-Control-Allow-Origin: *` — wildcard CORS
- `Feature-Policy: payment 'self'` — incomplete policy
- `X-Recruiting: /#/jobs` — non-standard header
- `X-Frame-Options: SAMEORIGIN` — present ✅
- `X-Content-Type-Options: nosniff` — present ✅
- No `Content-Security-Policy` — missing ❌
- No `Strict-Transport-Security` — missing ❌  

**Finding:** VULN-04, VULN-07  

---

### 07_zap_alerts_overview.png
**Tool:** OWASP ZAP 2.15 by Checkmarx — Alerts Panel  
**What It Shows:** ZAP passive scan completed against
`https://demo.owasp-juice.shop` and found **9 alerts** total:
1. Content Security Policy (CSP) Header Not Set
2. Cross-Domain Misconfiguration
3. Server Leaks Version Information via "Server" Header
4. Strict-Transport-Security Header Not Set
5. Timestamp Disclosure - Unix
6. Information Disclosure - Suspicious Comments
7. Modern Web Application
8. Re-examine Cache-control Directives
9. User Agent Fuzzer  

**Finding:** VULN-04, VULN-07  

---

### 08_zap_csp_alert_detail.png
**Tool:** OWASP ZAP 2.15 — Individual Alert Detail  
**What It Shows:** Detail view of Alert 1 — Content Security Policy (CSP)
Header Not Set. Confirms:
- URL: `https://demo.owasp-juice.shop/`
- Risk: Medium
- Confidence: High
- CWE ID: 693
- WASC ID: 15
- Source: Passive scan (Alert Reference 10038-1)  

**Finding:** VULN-04 — Missing HTTP Security Headers  

---

### 09_zap_scan_results.png
**Tool:** OWASP ZAP 2.15 — Automated Scan View  
**What It Shows:** Full ZAP interface showing the Automated Scan
was run against `https://demo.owasp-juice.shop/#` with
traditional spider and AJAX spider (Chrome) enabled.
Progress bar shows `Attack complete`.
The Alerts tab at the bottom confirms 8 alerts visible in this view.
This screenshot proves the scan methodology — passive mode only,
no active exploitation performed.  
**Finding:** Methodology / Scope proof  

---

## Summary Table

| Screenshot | Tool | Finding(s) Proven |
|-----------|------|------------------|
| 01_devtools_response_headers.png | DevTools Network | VULN-04, VULN-07 |
| 02_target_homepage.png | Chrome Browser | Scope confirmation |
| 03_devtools_cookies.png | DevTools Application | VULN-06 |
| 04_devtools_jwt_token.png | DevTools Application | VULN-02 |
| 05_api_users_version_disclosure.png | DevTools Network | VULN-05, VULN-07 |
| 06_curl_headers_output.png | curl / CMD | VULN-04, VULN-07 |
| 07_zap_alerts_overview.png | OWASP ZAP | VULN-04, VULN-07 |
| 08_zap_csp_alert_detail.png | OWASP ZAP | VULN-04 |
| 09_zap_scan_results.png | OWASP ZAP | Methodology proof |

---

> All screenshots were taken during a **read-only passive assessment**.  
> No exploits were executed. No data was modified or extracted.  
> Assessment conducted by **Angel Proshia F** — Future Interns Cyber Security Task 1.
