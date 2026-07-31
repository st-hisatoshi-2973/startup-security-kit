# Approval Design

This document introduces the concept of approval design for AI usage.

This guide is not about restricting AI from performing actions. Instead, it focuses on **determining which actions should require human approval** as part of security design.

With AI usage,

**AI itself is increasingly becoming an execution entity.**

However,

**being able to perform an action is not the same as being allowed to perform it autonomously.**

For high-impact actions, it is important that a human makes the final decision.

---

# Why Approval Matters

AI systems can perform a wide range of actions autonomously.

For example:

* Modifying source code
* Creating Pull Requests
* Updating databases
* Managing cloud resources
* Interacting with external services

However, allowing AI to perform every action autonomously may lead to:

* Unintended changes
* Incorrect operations
* Unexpected impact

Because of this,

**high-impact actions should require a human to make the final decision.**

---

# The Problem Is "Leaving Important Decisions to AI Alone"

One of the risks in AI usage is:

**allowing AI to make important decisions without human involvement.**

For example:

* Deploying to production
* Merging Pull Requests
* Updating production databases
* Deleting cloud resources
* Publishing information externally

The important point is:

**the greater the potential impact of an action, the more important it is for a human to review it before it is executed.**

---

# How to Think About It as Design

This is the most important point in this document.

Approval should be treated as a design problem of:

**ensuring that humans make the final decision, rather than simply preventing AI from acting.**

---

# Design Principles

## Clearly Define Which Actions Require Approval

First, identify which actions should require approval.

For example:

* Deploying to production
* Merging Pull Requests
* Updating production databases
* Deleting cloud resources
* Publishing information externally

The important point is:

**clearly defining approval targets based on risk.**

---

## Provide the Information Needed for Approval

When AI proposes an action, the approver should have enough information to make an informed decision.

For example:

* The action to be performed
* The reason for the action
* The expected impact
* The execution entity

The important point is:

**ensuring that approvers have sufficient information to make an informed decision.**

---

## Define Approval Levels Based on Risk

Not every action requires the same approval process.

For example:

* Low-risk actions may be executed automatically.
* Medium-risk actions may require approval from a designated reviewer.
* High-risk actions may require approval from multiple reviewers.

The important point is:

**designing approval levels that match the level of risk.**

---

## Record Approval Decisions

In addition to whether an action was approved, record information such as:

* Who approved it
* When it was approved
* What was approved

The important point is:

**making approval decisions traceable afterward.**

---

# Practical Guidelines

* Clearly define which actions require approval.
* Provide the information needed for approval.
* Design approval levels based on risk.
* Record approval decisions.
* Ensure that humans make the final decision for high-impact actions.

---

# Summary

The essence of approval is:

**ensuring that humans make the final decision, rather than simply preventing AI from acting.**

Key points:

* Being able to perform an action is not the same as being allowed to perform it autonomously.
* High-impact actions should require human approval.
* Design approval levels according to risk.
* Make approval decisions traceable.
