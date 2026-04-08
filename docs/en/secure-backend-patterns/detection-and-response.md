# Detecting Credential Abuse: Design Patterns

This document describes design patterns for detecting credential abuse, such as the misuse of compromised tokens or accounts.
This guide focuses on backend design rather than operational monitoring or tooling.

In recent years, attacks increasingly rely on compromised credentials, allowing malicious actions to be executed through legitimate workflows.
As a result, detection becomes as important as prevention.

---

# Why Detection Matters

Many attacks follow this pattern:

```
Valid authentication
↓
Valid authorization
↓
Malicious actions
```

In these cases, all actions appear legitimate,
making them difficult to prevent using access control alone.

Therefore, it is critical to detect:

```
Abnormal behavior that appears normal
```

---

# What to Detect

Detection should focus on deviations from expected behavior.

---

## Authentication signals

Suspicious login behavior:

* Sudden changes in IP address or location
* Spikes in login attempts
* Logins at unusual times

---

## Authorization signals

* Unexpected role or permission changes
* Increase in privileged operations
* Access to resources not typically used

---

## Token usage signals

* Token usage from new environments
* Abnormal request frequency
* Unusual access patterns

Examples:

* A large number of API requests in a short period
* Access to API endpoints not previously used
* Backend tokens being used from frontend contexts

---

## CI/CD signals

* Unexpected workflow executions
* Changes in build or deployment configurations
* Releases at unusual times

Examples:

* Deployments triggered late at night
* Releases bypassing approval processes

---

## Dependency signals

* Newly added dependencies
* Sudden version changes
* Suspicious package updates

---

# Designing for Detection

Detection is not just about collecting logs.
Systems must be designed to make abnormal behavior visible.

---

## Make actions traceable

* Include user identifiers (e.g., sub) in logs
* Track token identifiers (e.g., jti)
* Clearly record action types

Examples:

* user_id (who performed the action)
* token_id (which credential was used)
* role (under what permissions)
* action (what was executed)

---

## Define normal behavior

* Understand typical usage patterns
* Define what constitutes abnormal activity

---

## Enable correlation

Link the following:

* Authentication (who logged in)
* Authorization (what permissions were used)
* Actions (what was executed)

This allows tracing sequences of suspicious activities.

---

# Initial Response

Detection must be followed by action.

Basic flow:

```
Containment
↓
Impact assessment
↓
Remediation and recovery
```

Typical responses:

* Revoke tokens
* Invalidate sessions
* Temporarily restrict accounts or roles
* Roll back recent changes

If compromise is suspected:

* Identify affected actions and scope
* Remove unauthorized permissions
* Rotate secrets
* Review audit logs and implement preventive measures

---

# Recommended Practices

* Assume credentials can be abused
* Design systems to expose abnormal behavior
* Incorporate detection, not just prevention
* Prepare for rapid response

---

# Summary

Recent attacks often leverage valid credentials and legitimate workflows.

Key points:

* Prevention alone is not sufficient
* Detecting abnormal behavior is critical
* Detection must be built into system design
