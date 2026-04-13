# CI/CD Security Design Patterns

This document describes security design patterns for CI/CD (Continuous Integration / Continuous Delivery).

This guide focuses not on tool configuration, but on how to design CI/CD securely
as part of a backend system.

CI/CD is a powerful mechanism for automating the development process,
but it can also become a critical entry point for attackers.

---

# Why CI/CD Matters

CI/CD has the following characteristics:

* Jobs and scripts defined in CI/CD are executed automatically
* It has permissions to apply changes to production environments
* It can access secrets used for deployment and external integrations

As a result, once compromised, it can lead to:

* Workflow tampering
* Deployment of malicious code or configurations
* Impact spreading to users and systems

---

# How Attacks Work

Attacks against CI/CD typically follow this flow:

```
Compromised credentials
↓
Access to CI/CD
↓
Abuse or modification of workflows
↓
Execution of malicious processes or deployment
```

The key point is:

**legitimate mechanisms are abused as they are**

---

# Common Issues

The following problems are commonly seen in CI/CD security:

---

## Excessive permissions

* The same permissions are granted across all environments
* Unnecessary access to resources is allowed

---

## Insufficient trigger control

* Workflows are executed directly from external pull requests
* Deployments are triggered under unintended conditions

---

## Improper secret handling

* Long-lived tokens are used
* Secrets are broadly accessible within CI/CD

---

## Overtrusting workflows

* Scripts and configurations executed in CI/CD are not verified
* External inputs are executed without validation

---

# Design Principles

Security for CI/CD should be designed with the following assumption:

```
CI/CD can be compromised
```

---

## Least privilege

* Separate permissions by environment
* Restrict access to only what is necessary

---

## Separation of execution

* Separate build and deployment processes

The build stage handles external inputs such as code changes and dependencies,
which may involve untrusted execution.

The deployment stage directly affects production environments.

Therefore, it is important to separate trust boundaries
so that only trusted steps can perform deployments.

---

## Trigger control

* Properly control execution conditions based on external inputs
* Require explicit approval for production deployments

---

## Secret management

* Use short-lived tokens
* Limit scopes to the minimum required
* Use OIDC where possible

By using OIDC:

* Long-lived credentials are no longer required
* Temporary credentials can be issued at runtime

---

# Relationship with Detection

CI/CD is not only a potential entry point for attacks,
but also an important target for detection.

For example, the following behaviors may indicate anomalies:

* Unexpected workflow executions
* Releases at unusual times
* Changes in configuration

---

# Recommended Patterns

Practical guidelines:

* Do not implicitly trust CI/CD
* Clearly separate permissions and execution boundaries
* Apply proper controls when external inputs are involved
* Consider both compromise and detection in design

---

# Summary

CI/CD improves development efficiency,
but it can also become a critical attack entry point.

Key points:

* CI/CD is an attack target
* Legitimate mechanisms can be abused
* Permissions, execution, and triggers must be carefully designed
* Detection should be considered together with prevention
