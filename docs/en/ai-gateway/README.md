# AI Gateway

This directory contains documents related to **AI Gateway**.

An AI Gateway is a concept for controlling interactions with external model APIs (e.g., LLMs),
and designing how AI is integrated into a system.

Unlike security patterns that focus on implementation and configuration,
this topic addresses **how to control AI usage as part of security design**.

---

## What This Covers

AI Gateway focuses on the following perspectives:

* How requests to external model APIs are controlled
* How input and output are handled safely
* How externally transmitted data is managed
* How AI usage is made observable and traceable

The goal is not to introduce a specific tool, but to:

**design AI usage in a way that makes it understandable and controllable**

---

## Relationship with Threat Modeling

Threat modeling clarifies:

**what can go wrong**

AI Gateway defines:

**where and how to apply control**

In other words:

* Threat modeling identifies risks
* AI Gateway defines control points

---

## Position in System Design

AI Gateway is not a specific step in a process.

Instead, it is:

**a control layer for AI usage**

It is embedded into system design and applied across:

* Input handling
* External communication
* Output usage
* Logging and audit

---

## Documents

* [AI Gateway Security Design](./overview.md)

---

## Summary

* AI Gateway defines how AI usage is controlled
* It is a design concept, not a specific tool
* It works together with threat modeling
