# Secret Detection Concepts

This document introduces the basic concepts of secret detection.

Rather than simply introducing regular expressions or detection tools, this guide focuses on **how to prevent secrets from crossing trust boundaries** as part of security design.

Secrets become a problem when they are:

**unintentionally transmitted, recorded, or shared outside trust boundaries.**

---

# Why Secret Detection Matters

In modern systems, secrets pass through many different places.

For example:

* API requests
* Logs
* CI/CD
* Chats
* AI inputs
* External services

As a result,

**protecting only where secrets are stored is no longer sufficient.**

---

# The Problem Is “Unintentional External Transmission”

Secret leakage is not caused only by third-party attacks.

It can also occur when secrets are:

**unintentionally transmitted externally through legitimate features or operations.**

For example:

* GitHub commits
* Log output
* Sending data to AI systems
* Requests to external APIs

In practice, however, problems often arise such as:

* Not knowing where the secret was sent
* Not knowing what was included
* Not being able to trace who sent it

Therefore, the important point is:

**not finding leaks after the fact, but detecting them before they cross trust boundaries.**

---

# What Counts as a Secret

A secret is information that creates risk if exposed externally.

For example:

* API keys
* Access tokens
* Secrets
* Passwords
* Personal information
* DB connection strings
* Internal identifiers

An important point is that:

**it is not limited to authentication credentials themselves.**

For example, internal system configuration details or identifiers may also provide clues for attackers.

*Note: The definition of personal information may vary depending on laws, regulations, or organizational policies.*

---

# How to Think About It as a Design Problem

This is the most important point in this document.

Secret detection should be treated as:

**a design approach for detecting and controlling secrets before they are externally transmitted, rather than simply searching for them.**

---

# Design Principles

## Define What Should Be Detected

First, clarify what should be treated as a secret.

For example:

* API keys
* JWTs
* Bearer tokens
* Cloud credentials
* Personal information
* Internal system identifiers

Without clearly defining detection targets,

**it becomes impossible to determine what should be stopped.**

---

## Detect Using Patterns

Many secrets have recognizable formats.

For example:

* Prefixes
* Fixed lengths
* Base64 formats
* UUID formats
* JWT formats

These can often be detected using regular expressions or similar approaches.

However,

**patterns alone have limitations.**

---

## Supplement With Context

Some secrets cannot be identified by format alone.

For example:

* Being sent together with descriptions such as “API key”
* Included in Authorization headers
* Used within the context of specific services

In other words,

**where and how the data is used**

also matters.

---

## Assume False Positives and Misses

Secret detection can never be perfect.

There are difficult cases such as:

* Distinguishing from random strings
* Partially extracted values
* Encoded or transformed information

Therefore, the goal should not be:

**achieving 100% detection, but reducing risk.**

It is also important not to rely on a single detection mechanism alone.

Risk reduction should combine multiple approaches such as:

* Masking
* Blocking
* Reviews
* Logging
* Transmission controls

---

## Control Before External Transmission

The most important point is:

**controlling secrets before they are externally transmitted.**

For example:

* AI Gateways
* API Gateways
* CI/CD
* Webhooks
* Sending data to external logging platforms

These are all:

**points where trust boundaries are crossed**

and should be treated as control points for detection and enforcement.

---

# Relationship With AI Gateways

[AI Gateway](../ai-gateway/README.md)

When using AI systems, user input or internal data may be sent directly to external model APIs.

Therefore, it becomes important to:

* Detect secrets before sending data to AI systems
* Mask secrets
* Block requests
* Record detection events in logs

AI Gateways can serve as:

**one of the control points for secret detection.**

---

# Relationship With Logging and Auditing

Secret detection is also closely related to logging design.

For example:

* Recording detection events
* Tracing with request_id
* Identifying who attempted transmission
* Recording intended destinations

These make it possible to create:

**a state where incidents can be traced afterward.**

At the same time,

**logs themselves must not contain secrets.**

Instead of recording the detected values themselves, systems can record metadata such as request_id in order to maintain traceability without exposing secrets.

---

# Practical Guidelines

* Define what counts as a secret
* Detect using both patterns and context
* Assume false positives and misses
* Control before crossing trust boundaries
* Combine with logging and auditing for traceability

---

# Summary

The essence of secret detection is:

**preventing secrets from crossing trust boundaries.**

Key points:

* Secrets can be externally transmitted through many paths
* Context matters in addition to patterns
* Think in terms of risk reduction rather than perfect detection
* Control at points where trust boundaries are crossed
* Secret detection is closely related to AI Gateways and logging design
