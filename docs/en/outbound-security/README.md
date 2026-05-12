# Outbound Security

This directory covers how outbound communication to external services, AI APIs, and other external systems should be understood and controlled as part of security design.

---

# What This Directory Covers

This directory mainly focuses on topics such as:

* How to identify outbound communication
* Which destinations should be allowed
* How to prevent unnecessary outbound communication
* How to handle dynamic outbound communication
* How to make outbound communication visible and traceable

The important idea is:

**not assuming communication should be freely allowed, but allowing only the communication that is necessary.**

---

# Relationship with AI Gateway

AI usage introduces communication with external model APIs and external tools.

AI Gateway is not simply a mechanism for blocking communication. Instead, it acts as a design-level control point for:

* Where communication is sent
* What data is sent
* Which usage should be recorded

This directory focuses specifically on:

**controlling where communication is allowed to go.**

---

# Relationship with Secret Detection

Outbound communication is not only about:

**"where communication is sent,"**

but also:

**"what is being sent."**

Because of this, outbound security is closely related to secret detection.

---

# Documents

* [outbound-communication-control](./outbound-communication-control.md)

---

# Summary

* Outbound communication itself becomes a security boundary
* Allowing only necessary communication is important