# Dependency Security Design Patterns

This document describes security design patterns for dependencies (libraries and packages).

This guide does not focus on tool configuration or scanning techniques.
Instead, it focuses on how to handle dependencies securely as part of backend system design.

Modern software heavily relies on external packages.
While they provide convenience, they can also become entry points for attacks.

---

# Why Dependencies Matter

Dependencies have the following characteristics:

* They are not your own code
* They are managed and updated externally
* They are executed with the same privileges as your application

In other words,

**trusted external code is executed as part of your system**

As a result, once a problematic dependency is introduced, it can lead to:

* Execution of malicious code
* Theft of credentials
* Compromise of the entire system

---

# How Attacks Work

Attacks leveraging dependencies typically follow this flow:

```
Malicious package publication or compromise
↓
Included as a dependency
↓
Code is executed during build or runtime
↓
System or credentials are compromised
```

The key point is:

**legitimate mechanisms are abused as they are**

---

# Why Problems Occur

The core issue in dependency security is **incorrect assumptions**.

A common assumption is:

**dependencies are provided safely**

In reality, risks such as the following exist:

* Package takeover
* Malicious updates
* Typo squatting (packages with similar names)

**trusted dependencies are executed without sufficient verification**

This is the core problem.

---

# How to Think About Design

This is the most important point.

## Change the assumption

**Do not implicitly trust dependencies**

---

## Design Principles

### Version pinning

* Explicitly fix dependency versions

**to prevent unintended updates**

---

### Controlled updates

* Manage dependency updates in a controlled (reviewable) manner
* Understand the impact of updates (which features or services are affected)

**to maintain control over changes**

---

### Minimize dependencies

* Avoid adding unnecessary packages
* Remove unused dependencies

**to reduce the attack surface**

---

### Separation of execution

* Separate build-time and runtime dependencies
* Execute only build artifacts in production environments

**to prevent unnecessary code from running in production**

---

### Awareness of trust boundaries

* Be aware of where external code is executed

**to understand the scope of impact**

---

# Relationship with Detection

Dependencies are not only a point of spread for attacks, but also an important target for detection.

For example, the following behaviors may indicate anomalies:

* Unexpected addition of dependencies
* Sudden changes in versions
* Suspicious network activity

**these can be detected as deviations from normal behavior**

---

# Recommended Patterns

Practical guidelines:

* Do not implicitly trust dependencies
* Clearly define what is included and its impact
* Control updates deliberately
* Combine with detection strategies

---

# Summary

Dependencies improve development efficiency,
but they can also become a critical point for attack propagation.

Key points:

* Dependencies are an attack target
* Legitimate mechanisms can be abused
* The problem lies in assumptions
* Design for inclusion, updates, and execution is critical
* Detection should be considered alongside prevention
