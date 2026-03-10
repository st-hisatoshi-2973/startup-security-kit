# Developer Security Checklist

This checklist helps developers implement basic security practices during application development.

It is designed for startups and small teams who want practical security guidance without heavy processes.

---

# Quick Checklist

## Authentication

* [ ] MFA is enabled for admin accounts
* [ ] Shared accounts are not used
* [ ] Access tokens have appropriate expiration times

## Authorization

* [ ] Roles and permissions are clearly defined
* [ ] Sensitive actions require stronger access controls

## API Security

* [ ] Input validation is implemented
* [ ] Rate limiting is applied to sensitive endpoints
* [ ] Error messages do not expose sensitive information

## Secrets Management

* [ ] Secrets are not hardcoded in source code
* [ ] Secrets are stored in secure secret management systems
* [ ] Access to secrets is restricted

## Logging and Monitoring

* [ ] Security-related events are logged
* [ ] Sensitive data is not written to logs
* [ ] Logs are monitored

## Dependency Security

* [ ] Dependencies are regularly updated
* [ ] Vulnerability scanning is performed
* [ ] Unnecessary dependencies are removed
* [ ] SBOM is generated for the application

---

# Detailed Checklist

## Authentication

### MFA is enabled for admin accounts

Administrative access should require multi-factor authentication (MFA) whenever possible.

### Shared accounts are not used

Each user should have their own account.

Individual accounts improve accountability and allow access to be revoked without affecting others.

### Access tokens have appropriate expiration times

Access tokens should be short-lived when possible.

Long-lived tokens increase the impact of credential leaks.

---

## Authorization

### Roles and permissions are clearly defined

Applications should clearly define roles and permissions.

Avoid granting broad access when it is not required.

### Sensitive actions require stronger access controls

Critical actions should require stronger protections.

Examples include:

* changing user permissions
* deleting resources
* modifying billing settings

---

## API Security

### Input validation is implemented

All external inputs should be validated.

This includes:

* request parameters
* JSON payloads
* file uploads

### Rate limiting is applied

Rate limiting helps prevent abuse and brute-force attacks.

Sensitive endpoints include:

* login
* password reset
* token generation

### Error messages do not expose sensitive information

Error responses should avoid revealing internal details such as:

* stack traces
* database queries
* internal system details

---

## Secrets Management

### Secrets are not hardcoded

Secrets such as API keys or database passwords should never be committed to source code.

### Use secret management systems

Secrets should be stored using secure systems such as:

* cloud secret managers
* environment variables

### Access to secrets is restricted

Only services and users that require a secret should have access to it.

---

## Logging and Monitoring

### Security events are logged

Log events related to security such as:

* authentication attempts
* permission changes
* administrative actions

### Avoid logging sensitive data

Sensitive information should not appear in logs.

Examples include:

* passwords
* access tokens
* personal data

### Logs are monitored

Logs should be monitored to detect unusual behavior.

---

## Dependency Security

### Dependencies are regularly updated

Outdated dependencies may contain known vulnerabilities.

Use dependency update tools when possible.

### Vulnerability scanning is performed

Security scanning tools should be used to detect vulnerable packages.

Examples include:

* Dependabot
* OSV scanner

### Unnecessary dependencies are removed

Reducing dependencies decreases the attack surface.

### SBOM is generated

The application should generate a Software Bill of Materials (SBOM) to track its dependencies.

An SBOM helps quickly identify affected components when new vulnerabilities are disclosed.

---

# Notes

This checklist focuses on practical security practices for developers.

It is not a complete security framework, but a starting point for improving application security in small teams.
