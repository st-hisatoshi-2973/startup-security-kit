# RBAC Authorization Patterns

This document provides practical RBAC (Role-Based Access Control) design patterns for backend development.

RBAC is widely used in many systems, but poor design can lead to unnecessary complexity
and make systems difficult to maintain and extend.

This guide focuses on simple and practical design.

---

# Overview

RBAC (Role-Based Access Control) assigns roles to users
and controls access based on those roles.

Basic structure:

```
User
↓
Role
↓
Permission
```

Permissions represent what actions are allowed.

---

# Design Principles

## Keep roles simple

Too many roles can lead to role sprawl.

Example:

* admin
* admin_readonly
* admin_limited
* admin_super

Avoid overloading roles with too many variations.
Use permissions for fine-grained control.

---

## Roles represent user responsibilities

Roles should represent what a user is responsible for within the system.

Example:

* Admin
* Editor
* Viewer

---

## Define permissions clearly

Permissions represent allowed actions.

Example:

* read
* write
* delete

Designing permissions explicitly enables flexible and scalable authorization.

---

# Relationship with JWT

When combining RBAC with JWT, careful design is required.

## Including roles in JWT

Pros:

* No database lookup required
* Fast authorization

Cons:

* Roles may become stale
* Difficult to update or revoke permissions

---

## Recommended approach

```
JWT → identity (sub)
RBAC → authorization (backend)
```

Authorization should be handled on the server side.

When using JWT, keep the payload minimal.

---

# Common Pitfalls

## Too many roles

Hard to manage

---

## Overusing roles for fine-grained control

Requires proper permission design

---

## Performing authorization on the client side

Security risk

---

## Relying only on JWT for authorization

Cannot reflect state changes

---

# When NOT to use RBAC

RBAC is not always the best choice.

## When you need condition-based access control

Example:

* Users can edit only their own resources

In such cases, ABAC (Attribute-Based Access Control) may be more suitable.

---

## When permissions change frequently

RBAC alone may not be sufficient

---

# Recommended Pattern

A practical and simple approach:

* Keep roles minimal
* Use permissions for flexibility
* Perform authorization on the backend

---

# Summary

RBAC is simple, but design matters.

Key points:

* Avoid too many roles
* Define permissions clearly
* Perform authorization on the server side
* Do not rely too much on JWT
