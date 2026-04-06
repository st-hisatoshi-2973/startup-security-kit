# Credential Compromise and Supply Chain Attacks

This document describes supply chain attack patterns originating from credential compromise, such as leaked tokens or compromised accounts.

In recent years, incidents involving stolen API tokens or compromised package registry accounts (e.g., npm) have led to widespread impact across many systems.

This guide focuses on attack flows and practical design considerations.

---

# Overview

This document focuses on **software supply chain attacks**, including those involving dependencies and CI/CD pipelines.

It covers not only traditional third-party compromise, but also attacks that propagate through packages and development processes.

Supply chain attacks do not target systems directly.
Instead, they spread through trusted components and workflows.

A typical flow looks like:

```
Credential compromise
↓
Privilege abuse
↓
Malicious changes through trusted channels
↓
Propagation to downstream users
```

---

# Common Attack Patterns

## Token compromise

Examples:

* Leaked API tokens
* Exposed CI/CD tokens

Impact:

* Unauthorized API usage
* Repository access
* Abuse of automated workflows

---

## Account compromise

Examples:

* Compromised package registry accounts (e.g., npm)

Impact:

* Publishing malicious packages
* Injecting malware into existing packages
* Spreading impact to downstream users

---

# Attack Chains

Supply chain attacks can follow different paths.

## Provider side (OSS / package maintainers)

```
Credential compromise
↓
Privilege abuse
↓
Unauthorized CI/CD usage or package tampering/publishing
↓
Propagation to users
```

---

## Consumer side (general services)

```
Install compromised dependency
↓
Executed in build / CI/CD
↓
Secret and token exfiltration
↓
System compromise
```

---

# Common Issues

## Long-lived tokens

Higher impact if leaked

---

## Excessive privileges

Increases blast radius

---

## Poor token handling

Tokens left in logs or code can be extracted and abused.

Examples:

* API tokens written to logs
* Secrets committed to repositories

---

## Lack of dependency verification

Risk of importing malicious code

---

# Design Considerations

## Token management

* Least privilege
* Short expiration
* Regular rotation

---

## Account protection

* Enable MFA
* Monitor login activity
* Detect suspicious behavior
* Minimize privileges

---

## CI/CD protection

* Secure secret handling
* Restrict workflows
* Isolate execution environments

---

## Dependency management

* Verification and signing
* Vulnerability scanning
* Use trusted sources

---

# Defense is Not Enough

Modern supply chain attacks often involve compromised legitimate accounts or tokens.

In such cases, attacks are executed through legitimate workflows,
making them difficult to prevent using traditional access controls alone.

What becomes critical:

* Designing with compromise in mind
* Detecting anomalies
* Responding quickly

Examples:

* Detecting unusual releases
* Monitoring dependencies
* Preparing incident response processes

---

# Recommended Practices

* Assume credentials can be compromised
* Apply least privilege
* Use short-lived tokens
* Continuously verify dependencies

---

# Summary

Credential compromise can impact the entire supply chain, not just a single system.

Key points:

* Credential management is critical
* Authorization design determines impact scope
* Detection and response are as important as prevention
