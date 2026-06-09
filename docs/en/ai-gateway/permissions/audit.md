# Audit Design

This document introduces the concept of audit design for AI usage.

This guide is not simply about logging or record keeping. Instead, it focuses on **how to make AI activities traceable** as part of security design.

With AI usage,

**AI itself is increasingly becoming an execution entity.**

Because of this,

**it is necessary to make it possible to trace who performed what action and when.**

---

# Why Audit Matters

AI systems perform a wide range of actions.

For example:

* File access
* Command execution
* External communications
* GitHub operations
* Cloud operations

Without knowing:

* What happened
* Who performed the action
* What was affected

it becomes difficult to investigate incidents and respond appropriately.

Because of this,

**the ability to trace what happened**

becomes important.

---

# The Problem Is "Lack of Traceability"

One of the risks in AI usage is:

**being unable to trace what happened.**

For example:

* Not knowing who performed an action
* Not knowing what was executed
* Not knowing when it occurred
* Not knowing where data was sent
* Not knowing why an action was blocked

The important point is:

**the inability to identify the cause of an incident and respond appropriately becomes a risk.**

---

# How to Think About It as Design

This is the most important point in this document.

Audit should be treated as a design problem of:

**making activities traceable, rather than simply recording them.**

---

# Design Principles

## Clearly Define What Should Be Audited

First, identify what should be included in audit records.

For example:

* File access
* Command execution
* External communications
* GitHub operations
* Cloud operations
* Permission evaluation results

The important point is:

**clearly defining what you want to trace.**

---

## Record Traceable Information

Audit records should contain information that allows activities to be traced afterward.

For example:

* Execution time
* Executing user
* AI used
* Executed action
* Permission evaluation result
* `request_id`
* `trace_id`

The important point is:

**being able to correlate related activities.**

---

## Do Not Record Sensitive Information

Audit records are important, but

**not everything should be recorded as-is.**

For example:

* API keys
* Access tokens
* Passwords
* Personal information

should not be recorded in plain form.

The important point is:

**balancing traceability and confidentiality.**

---

## Consider Tampering

Audit logs are often used during incident investigations.

Because of this, considerations should be made for:

* Deletion
* Tampering
* Overwriting

The important point is:

**not only recording information, but also preserving it in a trustworthy state.**

---

# Practical Guidelines

* Clearly define audit targets
* Record traceable information
* Avoid recording sensitive information
* Consider log tampering
* Maintain the ability to investigate incidents afterward

---

# Summary

The essence of audit is:

**making activities traceable, rather than simply recording them.**

Key points:

* AI itself is increasingly becoming an execution entity
* Being able to trace what happened becomes important
* Balance confidentiality and traceability
* Maintain the ability to investigate incidents afterward
