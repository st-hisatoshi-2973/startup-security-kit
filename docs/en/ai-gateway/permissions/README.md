# AI Permission Design

This directory covers how to think about permission design for AI usage.

In traditional systems, access control was mainly focused on:

* Users
* APIs
* Services

However, with AI usage,

**AI itself is increasingly becoming an execution actor**

in many situations.

For example:

* Reading files
* Executing commands
* Communicating with external services
* Operating GitHub
* Accessing cloud environments
* Connecting to databases

Because of this,

**"what should be allowed for AI"**

itself becomes an important security design concern.

---

# What This Directory Covers

This directory mainly focuses on topics such as:

* What AI can access
* What AI can execute
* Which operations require approval
* How operations should be traced and audited

The important idea is:

**not giving AI unrestricted permissions, but allowing only the permissions that are necessary.**

---

# Relationship with AI Gateway

AI Gateway functions as a control point for AI usage.

This directory focuses specifically on:

**permission design for what AI should be allowed to do.**

---

# Relationship with Outbound Security

AI usage introduces communication with external services and AI APIs.

Because of this,

* Where AI can communicate
* Which external tools AI can use

also become part of permission design.

---

# Relationship with Secret Detection

AI may have access to credentials or sensitive information.

Because of this,

* What information AI can access
* What information can be sent to AI

also become part of permission design.

---

# Documents

* [Access Permission Design](./access.md)
* [Execution Permission Design](./execution.md)

The following documents are planned:

* [approval](./approval.md)
* [audit](./audit.md)

---

# Summary

* AI itself is increasingly becoming an execution actor
* "What should be allowed for AI" becomes important
* Design with least privilege
* Combine permissions with approval and auditing