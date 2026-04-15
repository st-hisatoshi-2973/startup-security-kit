# Startup Security Kit AI Review

## Purpose
This review evaluates code changes using Startup Security Kit security principles.

---

## Review Process

1. Read the current git diff first
2. Identify security-relevant areas (auth, tokens, external calls, logging, etc.)
3. Refer to relevant Startup Security Kit documents:
   - checklist/*
   - secure-backend-patterns/*
4. Produce actionable findings

---

## Knowledge Sources

When reviewing, refer to the following as needed:

### Checklist
- `startup-security-kit/docs/en/checklists/developer-security-checklist.md`

### Secure-Backend-Patterns
- `startup-security-kit/docs/en/secure-backend-patterns/jwt-authentication.md`
- `startup-security-kit/docs/en/secure-backend-patterns/rbac-authorization.md`
- `startup-security-kit/docs/en/secure-backend-patterns/detection-and-response.md`
- `startup-security-kit/docs/en/secure-backend-patterns/ci-cd.md`
- `startup-security-kit/docs/en/secure-backend-patterns/dependency-security.md`

Do not blindly list all items.
Select only relevant items based on the code.

---

## Required Review Points

Focus on:

- Authentication / Authorization flaws
- Secret exposure
- Excessive privilege
- Sensitive data in logs
- External communication / dependencies
- AI-related risks
  - Sensitive data sent to AI
  - Unsafe automation
  - Missing human approval

---

## Output Format

For each finding:

### Severity
High / Medium / Low

### Finding
What is wrong

### Why it matters
Impact

### Suggested fix
Concrete fix

### Detection / Logging
How to detect this issue in production

### Human check
What should be manually verified

---

## Review Principles

- Be specific and actionable
- Prefer real risks over theoretical ones
- If unsure, explicitly say "Needs confirmation"
- Do not over-report low-value issues

---

## Important

- Do NOT dump checklist items
- Use checklist/patterns only as supporting knowledge
- Always tie findings to actual code