# Data Protection

This directory covers how to protect secrets and sensitive data.

In modern systems, secrets are no longer simply stored in one place.
They pass through many different boundaries, such as:

* AI
* APIs
* Logs
* CI/CD
* External services

As a result,

**it is important not only to control where data is stored, but also where it is sent.**

---

# What This Directory Covers

This directory focuses on topics such as:

* How to detect secrets
* How to control data before it crosses trust boundaries
* How to handle secrets when using AI or external services
* How to integrate with logging and auditing
* How to think about false positives and missed detections

The important idea is:

**not “finding leaks after they happen,” but “controlling data before it leaves.”**

---

# Relationship With AI Gateways

When using AI systems, user input and internal data may be sent directly to external model APIs.

Because of this, AI Gateways need to define:

* What data can be sent
* What data must not be sent
* Where controls should be applied

This directory focuses particularly on:

**what should not be allowed to cross trust boundaries.**

---

# Documents

* [secret-detection](./secret-detection.md)

---

# Summary

* Secrets cross many different boundaries
* Transmission paths are just as important as storage locations
* Detection and control before external transmission are critical
