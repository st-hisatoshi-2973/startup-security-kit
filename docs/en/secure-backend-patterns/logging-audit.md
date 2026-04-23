# Security Design Patterns for Logging / Audit

This document introduces security design patterns for logging and auditing.

This guide does not focus on specific tools or analysis methods.
Instead, it focuses on **how to design logging as part of the backend to enable detection and response**.

Logs are not just records — they are the **foundation for detecting, tracing, and responding to incidents**.

---

# Why Logging Design Matters

From a security perspective, attacks often occur in the following way:

```
Legitimate authentication
↓
Legitimate authorization
↓
Malicious action
```

In these cases:

* seemingly valid tokens
* seemingly valid permissions
* seemingly valid APIs

are used, making the activity **appear normal at a glance**.

Therefore, it is critical to ensure that:

**you can trace who did what, with which privileges, even after the fact**

---

# Why Problems Occur

Many logging-related issues come from the fact that:

**logs exist for recording, but are not designed for traceability**

Common examples:

* Only endpoints or messages are recorded
* No linkage to authentication or authorization context
* The actor (who performed the action) is unknown

In such cases:

* anomalies cannot be detected
* impact scope cannot be identified
* response cannot be performed quickly

---

# How to Think About the Design

This is the most important point.

Logs should not be something added after an incident.
They must be **designed from the beginning**.

If logging is added after an incident occurs,
the actions that happened at that time cannot be traced.

Also, correlation IDs and core schema should be defined early,
so that fields can be extended later without breaking traceability.

The goal is:

**to design logs so that detection and response are possible**

---

## Design Principles

### Ensure Traceability of Actions

Design logs to follow the flow of:

**authentication → authorization → action**

| Phase          | Perspective | Example                   |
| -------------- | ----------- | ------------------------- |
| Authentication | Actor       | User ID, service account  |
|                | Credential  | Token ID, API key ID      |
| Authorization  | Permission  | Role, scope               |
| Action         | Operation   | Create, update, delete    |
|                | Resource    | User, file, configuration |
|                | Source      | IP address, user agent    |
|                | Result      | Success / failure         |

By recording this information, you can reconstruct:

**authentication → authorization → action**

as a complete trace.

Logs must also be protected so that modification or deletion is difficult,
while preserving the ability to trace actions.

---

### Maintain Correlation

Logs should not exist in isolation — they must be correlated.

* Assign request IDs or trace IDs
* Link logs using token IDs or session IDs

This enables:

**reconstructing a sequence of actions across multiple logs**

---

### Use Structured Logging

Logs should not be human-readable text only, but structured data.

* Output in structured formats such as JSON
* Clearly separate fields

For example, having at least the following fields makes logs usable for detection and tracing:

* timestamp
* event_name
* actor_id
* token_id / session_id
* role / scope
* resource_id
* request_id / trace_id
* outcome (success / failure)

This allows logs to be:

**queried, analyzed, and used for detection by systems**

---

### Define What to Log

Logs include both **operational logs** and **audit logs**.

Operational logs are used to understand system behavior and errors,
and are used for incident detection, recovery, and operational improvement.

Audit logs, on the other hand, serve as evidence
to verify the legitimacy of actions after the fact.

Therefore, audit logs must:

* be resistant to tampering
* be properly access-controlled
* have defined retention periods
* include audit trails for access and deletion of the logs themselves

Not all logs need the same level of detail.
Important actions must be clearly defined.

Audit logs must allow you to trace:

* who
* using which credential
* with what permissions
* performed which action

Important examples (both success and failure):

* login / authentication
* token issuance and revocation
* permission changes (role assignment/removal)
* administrative operations (deletion, configuration changes)
* authorization failures (insufficient permissions)
* validation errors

These are:

**critical events that must always be recorded as audit logs**

---

### Do Not Log Sensitive Data

The following information must never be included in logs:

* token values
* API keys
* secrets
* Authorization headers

What is needed is an identifier, not the secret itself.

---

# Relationship with Detection

Logging design directly impacts detection capability.

With well-designed logs, you can:

* detect abnormal operations
* identify deviations from normal behavior
* detect actions inconsistent with assigned permissions

Additionally:

**being able to identify which token or user performed an action**

enables:

* impact analysis
* token revocation
* account control

---

# Recommended Pattern

Practical guidelines:

* design logs from the beginning
* record authentication, authorization, and actions consistently
* ensure logs are correlatable
* never include sensitive data
* design with detection and response in mind

---

# Summary

Logs are not just records — they are a critical foundation for security.

Key points:

* logging is a design problem, not an afterthought
* the ability to trace "who did what with which privileges" is essential
* correlation and structure enable analysis
* logs must support detection and response
