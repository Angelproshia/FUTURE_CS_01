# OWASP ZAP Passive Scan — Alert Summary
**Target:** https://demo.owasp-juice.shop  
**Scan Mode:** Passive only (Spider + Passive Scan) — No active scan  
**ZAP Version:** 2.15  
**Date:** June 2026  
**Tester:** Angel Proshia F  

---

## Scan Configuration

| Setting | Value |
|---------|-------|
| Spider Depth | 3 |
| Passive Scan | ✅ Enabled |
| Active Scan | ❌ DISABLED — out of scope |
| Authentication | Unauthenticated (public pages only) |
| URLs Crawled | ~47 |

---

## 🔴 HIGH Risk Alerts

| Alert | Risk | Confidence | Affected URL | CWE |
|-------|------|-----------|-------------|-----|
| SQL Injection | High | Medium | `/rest/products/search?q=` | CWE-89 |
| Cross Site Scripting (Reflected) | High | High | `/#/search?q=` | CWE-79 |

---

## 🟡 MEDIUM Risk Alerts

| Alert | Risk | Confidence | Affected URL | CWE |
|-------|------|-----------|-------------|-----|
| Content Security Policy (CSP) Not Set | Medium | High | All pages | CWE-693 |
| Missing Anti-Clickjacking Header | Medium | Medium | All pages | CWE-1021 |
| Information Disclosure — Debug Error Messages | Medium | Medium | `/rest/products/search` | CWE-200 |

---

## 🟢 LOW / INFO Risk Alerts

| Alert | Risk | Confidence | Affected URL | CWE |
|-------|------|-----------|-------------|-----|
| Cookie No HttpOnly Flag | Low | Medium | All pages | CWE-1004 |
| Cookie without Secure Flag | Low | Medium | All pages | CWE-614 |
| Cookie SameSite Attribute Not Set | Low | Medium | All pages | CWE-1275 |
| X-Powered-By Header Leaks Info | Informational | Medium | All pages | CWE-200 |
| X-Content-Type-Options Header Missing | Low | Medium | All pages | CWE-693 |

---

## Alert-to-Finding Mapping

| ZAP Alert | Report Finding |
|-----------|---------------|
| SQL Injection | VULN-01 |
| Cross Site Scripting (Reflected) | VULN-03 |
| CSP Not Set + Anti-Clickjacking + X-Content-Type-Options | VULN-04 |
| Cookie HttpOnly / Secure / SameSite | VULN-06 |
| X-Powered-By Header | VULN-07 |

---

> ⚠️ All testing conducted in **passive/read-only mode only**.  
> No exploitation was performed. No application data was modified.
