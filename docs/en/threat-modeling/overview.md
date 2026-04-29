# Threat Modeling Overview

This document introduces the fundamental concepts of threat modeling.

This guide does not focus on explaining specific frameworks. Instead, it focuses on **how to identify “what can go wrong” as part of security design**.

Security is not determined by how you defend a system, but by
**how well you understand what can happen before designing it.**

---

# Why Threat Modeling Matters

When designing systems, the focus is often on *how to build* or *how to protect* them.

However,

**you cannot defend against attacks you have not anticipated.**

In other words:

```text
You don't know what can happen
↓
You don't know what to protect
↓
You cannot design appropriate defenses
```

---

# What is Threat Modeling?

Threat modeling is the process of:

**identifying what kinds of attacks or misuse could occur in a system**

The key is not the framework itself, but:

**thinking concretely about risks before designing the system**

---

# How to Approach It in Design

This is the most important point.

Threat modeling should be treated as:

**a process to clarify “what can go wrong” before design begins**

---

## Key Design Perspectives

### Identify Trust Boundaries

First, clearly define the system’s boundaries (trust boundaries).

* Points where input comes from outside (APIs, forms, etc.)
* Points where trust boundaries are crossed (e.g., public API → internal API, communication between different trust domains)
* Points where data leaves the system

These are all:

**potential entry points for attacks**

---

### Question Both Input and Usage

Assume all input is untrusted.

* Unexpected values
* Malformed input

In addition, consider how the system may be used—or misused:

* Direct API access without going through the frontend
* Using valid permissions against unintended targets
  (e.g., using permission to update your own data to modify someone else’s data)
* Combining legitimate features to achieve unintended outcomes

The key point is:

**not only valid input, but also unintended usage must be considered**

---

### Understand How Permissions Are Applied

Clarify how the system determines *who can do what*.

* Who is acting (user / service)
* What permissions are applied (roles / scopes)
* Where those permissions are granted

For example:

* A user is identified through login
* API tokens grant specific operation permissions
* Admin roles expand the range of allowed actions

The key point is:

**how permissions are determined and where they can be applied**

---

### Trace Data Flow

Understand how data flows through the system.

* Where it enters
* How it is processed
* Where it is stored
* Where it exits

This helps identify:

**risks of data leakage and unintended use**

---

# Relationship with STRIDE

In threat modeling, frameworks are sometimes used to organize identified risks.

A common example is **STRIDE**:

* Spoofing
* Tampering
* Repudiation
* Information Disclosure
* Denial of Service
* Elevation of Privilege

STRIDE can be used as:

**a checklist to ensure threats are considered comprehensively**

Typical usage:

* After identifying boundaries, inputs, permissions, and data flows
* When you want to systematically explore possible threats

However, the key point is:

**the goal is not classification, but identifying threats**

---

# Relationship with Other Designs

Threat modeling is used in combination with other security design practices.

For example:

* CI/CD: Where attacks can enter
  (`docs/en/secure-backend-patterns/ci-cd.md`)

* Dependencies: How issues can spread
  (`docs/en/secure-backend-patterns/dependency-security.md`)

* API: Where input is accepted
  (`docs/en/secure-backend-patterns/api-security.md`)

* Tokens: How authentication and authorization are established
  (`docs/en/secure-backend-patterns/token-secret.md`)

* Logging: How to detect and trace activity
  (`docs/en/secure-backend-patterns/logging-audit.md`)

In other words:

**threat modeling serves as the foundation for all other security design decisions**

---

# Practical Guidelines

In practice:

* Identify threats before designing the system
* Analyze boundaries, inputs, permissions, and data flow
* Consider misuse, not just intended use
* Use frameworks as support, not as the goal
* Combine with other security design practices

---

# Summary

Threat modeling is the starting point of security design.

Key points:

* Security is determined by understanding what can happen
* You cannot defend against unanticipated threats
* Identify risks before designing
* Analyze boundaries, inputs, permissions, and data flow
* It serves as the foundation for other security practices
