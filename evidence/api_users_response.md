# API Endpoint Observation Notes
**Target:** https://demo.owasp-juice.shop/api/Users  
**Method:** Passive observation via Browser DevTools (Network tab)  
**Date:** June 2026  
**Tester:** Angel Proshia F  

---

## Observation Summary

While browsing the application as a standard authenticated user, the **Network tab** in
Browser DevTools revealed that the `/api/Users` endpoint returns a full list of user
objects without any role-based access restriction.

---

## Response Structure Observed

The endpoint returns an array of user objects. Field names and types are documented below.
**No actual user data is reproduced here.**

```json
{
  "status": "success",
  "data": [
    {
      "id": [integer],
      "username": "[string]",
      "email": "[email address]",
      "password": "[bcrypt hash — should NEVER be returned]",
      "role": "[string: customer / admin / deluxe]",
      "createdAt": "[ISO 8601 timestamp]",
      "updatedAt": "[ISO 8601 timestamp]",
      "deletedAt": null
    }
    // ... all registered users returned
  ]
}
```

---

## Issues Identified

| # | Issue | Severity |
|---|-------|----------|
| 1 | Full user list accessible to any authenticated user (no role check) | HIGH |
| 2 | Password hashes (bcrypt) returned in API response | HIGH |
| 3 | Role field exposed — enables privilege enumeration | MEDIUM |
| 4 | Timestamps expose user account creation patterns | LOW |

---

## Stack Trace Leakage (Separate Observation)

When an error condition was triggered during passive browsing, the server returned
a verbose stack trace containing:

- Internal file paths (e.g. `/app/routes/...`)
- Node.js 24.x runtime version string
- Express middleware chain details
- SQLite database file path

This information significantly reduces the reconnaissance effort needed by an attacker.

---

## Related Finding
**VULN-05** — Sensitive Data Exposure via API Responses

---

> No data was downloaded, stored, or used beyond this observation note.  
> Assessment conducted in passive, read-only mode only.
