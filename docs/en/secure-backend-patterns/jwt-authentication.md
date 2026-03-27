# JWT Authentication Patterns

This document provides practical JWT authentication patterns for backend developers.

JWT is widely used, but often implemented without a clear understanding of its design trade-offs.
This guide focuses on simple, practical patterns that can be applied in real systems.

---

# Overview

JWT (JSON Web Token) is a compact, signed token used to represent claims between parties.

JWT consists of three parts: header, payload, and signature.

In practice, the structure and signing mechanism are mostly defined by the JWT specification.
This document focuses on **how to design the payload (claims)**, which has the biggest impact on security and maintainability.

---

# Basic Flow

A typical JWT-based authentication flow:

```
Login
↓
Access Token issued
↓
Client stores token
↓
Client sends token in requests (Authorization header)
↓
Server verifies token
```

Example header:

```
Authorization: Bearer <token>
```

---

# Token Design

Designing the token payload is one of the most important aspects of JWT usage.

## Recommended Claims

* `sub`: user identifier
* `iat`: issued at
* `exp`: expiration time

Depending on the use case:

* `iss`: issuer (who issued the token)
* `aud`: audience (who the token is intended for)

---

## What NOT to include

JWT payloads should not include:

* sensitive data (passwords, secrets)
* large data
* frequently changing data

JWT is not encrypted by default, and once issued, it cannot be easily modified.

---

## Should you include roles in JWT?

| Option               | Pros                                             | Cons                                                 |
| -------------------- | ------------------------------------------------ | ---------------------------------------------------- |
| Include roles in JWT | No DB lookup required<br>Fast authorization      | Roles may become stale<br>Difficult to revoke/update |
| Do not include roles | Always up-to-date authorization<br>More flexible | Requires DB/cache lookup                             |

### Recommended approach

* Include only minimal information in JWT (`sub`)
* Fetch roles/permissions from the backend when needed

If roles are included, keep token lifetime short.

---

# Token Lifetime

JWT is stateless, so expiration design is critical.

| Token         | Purpose                         | Recommendation                   |
| ------------- | ------------------------------- | -------------------------------- |
| Access Token  | Used for API access             | Short-lived (e.g., 5–15 minutes) |
| Refresh Token | Used to issue new access tokens | Longer-lived                     |

Short-lived access tokens reduce the impact of token leakage.

---

# Common Pitfalls

### Long-lived tokens

Long expiration increases risk if tokens are leaked.

---

### Treating JWT as session storage

JWT should not store all user state.

---

### Trusting JWT too much

JWT proves that the token was issued by your server,
not that the current state is still valid.

---

### No revocation strategy

JWT cannot be easily revoked once issued.

Consider:

* short expiration
* token rotation
* server-side checks for critical actions

---

# When NOT to use JWT

JWT is not always the best choice.

### When you need immediate revocation

Use server-side sessions if you must invalidate access immediately.

---

### When user state changes frequently

Frequent changes (roles, permissions) can lead to stale data in JWT.

---

### When simplicity is more important

For small systems, session-based authentication may be simpler.

---

### When tokens become too complex

Avoid putting too much data into JWT.

Reasons:

* Increased token size (network overhead)
* Data becomes stale
* Higher risk of sensitive data exposure
* Violates JWT’s primary purpose (authentication)

JWT should be used to identify users, not to carry application state.

---

# Recommended Pattern

A practical and simple approach:

* Use short-lived access tokens
* Use refresh tokens for renewal
* Keep JWT payload minimal (`sub`, `exp`)
* Include `iss` / `aud` when needed
* Fetch authorization data from backend when needed
* Avoid storing sensitive or dynamic data in JWT

---

# Summary

JWT is a powerful tool, but requires careful design.

* Focus on payload design, not token structure
* Keep tokens simple
* Limit lifetime
* Avoid embedding dynamic data
* Do not rely on JWT alone for authorization
