# AI Gateway Security Design

This document outlines how to approach security design for AI usage, focusing on how an AI Gateway should be treated as part of the system.

## What is an AI Gateway?

In this document, an **AI Gateway** is defined as:

**a layer that centrally controls requests to and responses from AI systems (external model APIs such as LLMs)**

The term “AI Gateway” is used in various contexts (e.g., API proxying, routing), but here it specifically refers to:

**a gateway for security, control, and observability**

---

This guide does not introduce specific tools or products.
Instead, it focuses on **how to control AI usage as part of security design**.

---

# Why an AI Gateway is Needed

In modern development, using AI—especially external model APIs (e.g., LLMs)—has become common.

However,

**AI usage introduces risks that differ from traditional API usage.**

---

# What Changes with AI Usage

At a glance, AI usage may resemble calling an external API. However, there are critical differences.

The key difference is:

**input and output handling extends beyond the control of the application**

For example:

* User input directly becomes part of the AI processing logic (prompt)
* Model-side behavior operates outside explicitly defined application logic
  (e.g., reasoning, tool-based calls to external APIs, databases, or internal functions)
* Output can directly influence application behavior

In other words:

**part of the application’s logic effectively exists outside the system as dynamic processing**

Unlike traditional APIs,

**model behavior can vary significantly depending on configuration and context, making it difficult for the application to fully predict outcomes**

---

# The Core Problem: Lack of Control

The fundamental issue with AI usage is:

**the inability to control what is sent, where it is sent, and how it is used**

For example:

* Sensitive data may be unintentionally sent to external systems
* Malicious or invalid input may be passed directly to the model
* Unexpected outputs may be used without validation

All of these stem from:

**the absence of a control point**

---

# How to Approach This in Design

This is the most important point.

AI should not be used directly. Instead:

**all interactions must go through a defined control point**

---

## Design Principles

### Route All Requests Through the Gateway

All AI requests must go through the AI Gateway.

* Do not connect clients or services directly to vendor APIs
* Centralize all entry points through the gateway

**Avoid creating uncontrolled paths.**

---

### Control Input

Validate and control input before sending it to the model.

* Remove sensitive information (tokens, personal data, etc.)
* Filter malicious or invalid input
* Prevent unintended data exposure

**Control what is sent externally.**

---

### Control Output

Do not trust model output by default—validate it before use.

* Detect unexpected or unsafe content
* Filter or constrain output
* Limit its impact on system behavior

**Treat output as untrusted data.**

---

### Ensure Observability

Make AI usage visible and traceable.

* What requests were sent
* What responses were returned
* Which features triggered the usage

**Enable monitoring, auditing, and incident investigation through logging.**

---

### Manage External Data Flow

Make it possible to understand and control what data is sent externally.

* Data being transmitted
* Model APIs being used
* Allowed destinations (e.g., allowlists)

**Define data boundaries for protection and vendor governance, and enforce them where appropriate.**

---

# Relationship with Threat Modeling

Introducing AI creates new attack surfaces:

* Input → Prompt Injection
* Output → Unsafe or malicious usage
* External communication → Data leakage
* Tool execution → Over-privileged actions
* Model / vendor → Supply chain risks

Threat modeling identifies these risks.

The AI Gateway provides the answer to:

**where and how to apply control**

---

# Practical Guidelines

* Never use AI directly—always introduce a control layer
* Control both input and output
* Manage all externally transmitted data
* Ensure visibility into usage
* Integrate with existing security practices

---

# Summary

The essence of AI security is:

**creating a state where you can understand and control what is sent, where it goes, and how it is used**

Key points:

* Treat AI as an external service
* Introduce a control point instead of direct usage
* Manage input, output, and communication
* Design in conjunction with threat modeling
