# Threat Modeling

This directory contains documents related to **threat modeling**.

Threat modeling is the practice of identifying **what can potentially happen in a system**, and serves as the starting point for deciding how to defend against it.

Unlike security patterns that focus on implementation and configuration, threat modeling focuses on **organizing risks as a prerequisite for security design**.

---

## What This Covers

Threat modeling addresses the following perspectives:

* What kinds of attacks or misuse could occur
* Where trust boundaries exist
* How input, permissions, and data flow through the system
* Not only intended use, but also how misuse can occur

The key point is not to apply a specific framework, but to
**concretely identify risks before design begins**.

---

## Relationship with Secure Backend Patterns

`secure-backend-patterns` primarily focuses on:

**how to design and implement systems securely**

For example:

* API design
* Token and secret management
* Logging / audit
* Dependency and CI/CD security

In contrast, threat modeling serves a different role:

```
Threat Modeling → What can happen
Secure Backend Patterns → How to defend
```

In other words:

* Threat modeling clarifies **what to protect and why**
* Secure backend patterns define **how to protect it**

---

## How to Use This

A typical flow is as follows:

```
1. Identify threats (threat modeling)
2. Design defenses (secure backend patterns)
3. Implement, detect, and respond (logging / audit, etc.)
```

This approach enables:

* Designing based on identified risks
* Integrating security intentionally, rather than as an afterthought

---

## Documents

* [overview](./overview.md)

---

## Summary

* Threat modeling organizes risks before design
* It serves a different role from implementation patterns
* It provides the foundation for other security design practices
