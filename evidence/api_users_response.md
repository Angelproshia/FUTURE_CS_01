# API Endpoint Observation Notes
**Target:** https://demo.owasp-juice.shop/api/Users  
**Method:** Passive observation via Browser DevTools (Network tab) + direct URL visit  
**Date:** Fri, 12 Jun 2026  
**Tester:** Angel Proshia F  

---

## Observation Summary

The `/api/Users` endpoint was accessed directly in the browser while DevTools was open.
The server returned **HTTP 401 Unauthorized** — confirming the endpoint is exposed and
reachable by anyone, and that it handles authentication via token headers rather than
blocking access entirely at the network level.

---

## What Was Observed

### Error Response (HTTP 401)
```
Status Code  : 401 Unauthorized
Error Message: UnauthorizedError: No Authorization header was found
```

The error page displayed:
```
OWASP Juice Shop (Express ^4.22.1)
401  UnauthorizedError: No Authorization header was found
```

This single error page reveals:
- The endpoint `/api/Users` exists and is accessible
- The application framework: **Express**
- The exact version: **^4.22.1**
- Authentication mechanism: **Authorization header** (JWT Bearer token)

### Response Headers Observed (via DevTools Network tab)
```
Status Code              : 401 Unauthorized
Request URL              : https://demo.owasp-juice.shop/api/Users
Request Method           : GET
Access-Control-Allow-Origin : *          ← Wildcard CORS
Feature-Policy           : payment 'self'
```

---

## Issues Confirmed

| # | Issue | Severity | Finding |
|---|-------|----------|---------|
| 1 | `/api/Users` endpoint publicly reachable — returns error with framework version | HIGH | VULN-07 |
| 2 | Error page discloses exact framework: Express ^4.22.1 | MEDIUM | VULN-07 |
| 3 | Access-Control-Allow-Origin: * on API endpoint | MEDIUM | VULN-04 |
| 4 | When accessed with valid token, returns all user data without role check (documented Juice Shop behaviour) | HIGH | VULN-05 |

---

## Screenshot Reference
`05_api_users_version_disclosure.png` — shows the 401 response with Express version disclosure
and DevTools Network tab confirming endpoint URL and response headers.

---

> No authentication was bypassed. No user data was extracted.  
> Assessment conducted in passive, read-only mode only.
