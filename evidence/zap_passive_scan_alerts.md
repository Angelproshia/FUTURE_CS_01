# OWASP ZAP Passive Scan — Alert Summary
**Target:** https://demo.owasp-juice.shop  
**Scan Mode:** Automated Scan (Passive + Spider) — No active exploitation  
**ZAP Version:** 2.15 by Checkmarx  
**Date:** Fri, 12 Jun 2026  
**Tester:** Angel Proshia F  

---

## Scan Configuration

| Setting | Value |
|---------|-------|
| URL Scanned | https://demo.owasp-juice.shop/# |
| Traditional Spider | ✅ Enabled |
| AJAX Spider | If Modern — Chrome |
| Active Scan | ❌ NOT used — passive/read-only only |
| Progress | Attack complete |

---

## Alerts Found — 9 Total (8 shown in detail view)

| # | Alert | Risk | Confidence | Related Finding |
|---|-------|------|-----------|----------------|
| 1 | Content Security Policy (CSP) Header Not Set | 🟡 Medium | High | VULN-04 |
| 2 | Cross-Domain Misconfiguration | 🟡 Medium | Medium | VULN-04 |
| 3 | Server Leaks Version Information via "Server" HTTP Response Header Field | 🟡 Medium | High | VULN-07 |
| 4 | Strict-Transport-Security Header Not Set | 🟡 Medium | High | VULN-04 |
| 5 | Timestamp Disclosure - Unix | 🟢 Low | Low | Info |
| 6 | Information Disclosure - Suspicious Comments | 🟢 Low | Medium | Info |
| 7 | Modern Web Application | 🔵 Info | Medium | Info |
| 8 | Re-examine Cache-control Directives | 🔵 Info | Low | Info |
| 9 | User Agent Fuzzer | 🔵 Info | Medium | Info |

---

## Key Alert Detail — Alert 1: CSP Header Not Set

- **URL:** https://demo.owasp-juice.shop/
- **Risk:** Medium
- **Confidence:** High
- **CWE ID:** 693
- **WASC ID:** 15
- **Source:** Passive (10038 - Content Security Policy Header Not Set)
- **Alert Reference:** 10038-1
- **Description:** Content Security Policy is not set. This allows XSS and data injection attacks.

---

## Important Note on SQL Injection

ZAP passive scan did **not** flag SQL Injection — this is expected behaviour.
Passive scanning cannot reliably detect SQLi without sending crafted payloads (active scan).
SQL Injection (VULN-01) is confirmed as a known, publicly documented vulnerability
in OWASP Juice Shop and was verified via browser observation of error responses.

---

## Alert-to-Finding Mapping

| ZAP Alert | Report Finding |
|-----------|---------------|
| CSP Header Not Set | VULN-04 |
| Cross-Domain Misconfiguration (CORS *) | VULN-04 |
| Server Leaks Version Information | VULN-07 |
| Strict-Transport-Security Not Set | VULN-04 |

---

> ⚠️ All testing conducted in passive mode only. No exploitation performed.  
> Screenshots: 07_zap_alerts_overview.png, 08_zap_alert_detail.png, 09_zap_scan_results.png
