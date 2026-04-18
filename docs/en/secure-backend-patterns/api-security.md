# API Security Design Patterns

This document describes security design patterns for APIs.

This guide does not focus on frameworks or specific configurations.
Instead, it focuses on how to design APIs securely as part of backend systems.

APIs are the interface to the outside world and must be designed with the assumption that they always receive **untrusted input**.

---

# Why APIs Matter

APIs have the following characteristics:

* They are directly accessible from external sources
* All inputs are untrusted
* Processing is executed based on authentication and authorization results

In other words,

**internal processing is executed based on external requests**

As a result, if the design is inadequate, the following issues can occur:

* Privilege escalation
* Execution of unauthorized operations
* Information leakage

---

# How Attacks Work

Attacks against APIs typically follow this flow:

```text
External request
↓
Malicious or unexpected input
↓
Insufficient validation or authorization
↓
Unintended processing is executed
```

The key point is:

**processing is executed without sufficient validation of input or permissions**

---

# Why Problems Occur

The key to API security is **not misplacing where security responsibilities are enforced**.

A common misunderstanding is:

* “Authentication is implemented, so it is secure”
* “Client-side controls are sufficient”

However, in reality:

* APIs can be called directly
* Client-side controls can be bypassed by users

As a result:

**if validation and authorization are insufficient on the server side, unintended operations can be executed**

---

# How to Think About Design

This is the most important point.

As a baseline assumption:

**never trust any input**

On top of that:

**validation and authorization must be enforced on the server side**

---

## Design Principles

### Input validation

* Validate all inputs
* Reject unexpected values

**to prevent malicious input**

---

### Strict authorization

* Always perform authorization checks on the server side
* Verify permissions for each operation

**because client-side controls can be bypassed**

---

### Least privilege

* Allow only necessary operations
* Do not expose unnecessary endpoints

**to limit the impact of compromise**

---

### Error handling

* Do not expose internal details unnecessarily
* Design consistent error responses

**to prevent information leakage**

---

### Rate limiting

* Limit the number of requests
* Throttle abnormal access patterns

**to make attacks harder to succeed**

---

# Relationship with Detection

APIs are not only attack targets but also important points for detection.

For example, the following behaviors can be detected as **deviations from normal behavior**:

* Unusual request frequency
* Access to unexpected endpoints (such as non-public endpoints or unintentionally exposed legacy APIs)
* Operations that are inconsistent with assigned permissions

---

# Recommended Patterns

Practical guidelines:

* Design APIs assuming they will be attacked
* Clearly define responsibility for input, authorization, and output
* Do not trust the client
* Combine preventive controls with detection

---

# Summary

APIs are the entry point of a system and a critical attack surface.

Key points:

* APIs are the interface to the outside world
* Input and authorization must be enforced on the server side
* It is critical to define where security is enforced
* Design input, authorization, and output carefully
* Combine with detection strategies
