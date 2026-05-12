# Security Review Checklist

## Injection

- [ ] SQL queries use parameterized statements or an ORM — no string concatenation with user input
- [ ] Shell commands do not interpolate user input
- [ ] Template rendering escapes output — no raw HTML injection from untrusted sources
- [ ] File paths derived from user input are validated and confined to expected directories (path traversal)

## Authentication & Authorization

- [ ] Every endpoint that requires authentication checks the session/token before executing
- [ ] Authorization is checked at the resource level, not just the route level
- [ ] Privilege escalation paths are not possible (user cannot grant themselves admin, etc.)
- [ ] Session tokens are not logged, leaked in URLs, or returned in responses unnecessarily

## Input Validation

- [ ] All external inputs (query params, request bodies, headers, webhooks) are validated before use
- [ ] Numeric inputs have range checks; string inputs have length limits
- [ ] File uploads validate type, size, and content — not just extension
- [ ] Validation happens on the server, not only on the client

## Secrets & Credentials

- [ ] No credentials, API keys, or secrets are hardcoded in source code
- [ ] Environment variable names used for secrets are documented but values are not
- [ ] Secrets are not logged or returned in API responses
- [ ] Any new env vars required by this change are documented in README or .env.example

## Dependencies

- [ ] New dependencies are from well-maintained, audited sources
- [ ] No dependency brings in known CVEs (check with `npm audit`, `pip-audit`, etc.)
- [ ] Pinned versions where security matters

## Cryptography

- [ ] Passwords are hashed with a strong algorithm (bcrypt, argon2, scrypt) — never MD5/SHA1
- [ ] Tokens use cryptographically secure random sources
- [ ] TLS is enforced for all external calls — no `http://` to external services
