# Secure coding baseline

Use this baseline for generated changes and tailor it to the app's threat model and stack. Prefer safe framework features over custom security code.

## Inputs and data

- Validate untrusted input at system boundaries; reject invalid values clearly.
- Use parameterized database queries and context-aware output encoding.
- Enforce size and format limits for uploads, requests, and parsed data.
- Avoid unsafe deserialization, shell construction, and path handling.
- Prevent server-side request forgery: restrict destinations, protocols, redirects, and resolved IP ranges for user-influenced outbound requests.
- Protect browser state-changing requests against CSRF where cookie credentials are used; use appropriate SameSite settings and origin checks as defense in depth.
- Set a restrictive content security policy and security headers appropriate to the app; avoid wildcard CORS with credentials.
- For uploads, enforce size/type limits, generate storage names, store outside executable/public paths, and scan or quarantine where the threat model requires it.

## Identity and access

- Enforce authorization on the server for every protected operation.
- Check ownership and tenant scope on every object lookup and mutation; do not rely on opaque IDs to prevent IDOR/BOLA.
- Deny by default. Centralize policy decisions where practical and test both allowed and denied cases.
- Protect login, recovery, invitation, and sensitive actions against brute force, enumeration, replay, and session fixation.
- Rotate session identifiers after authentication or privilege changes; make logout and revocation invalidate active credentials as appropriate.
- Use least privilege for users, services, and credentials.
- Do not rely on hidden UI controls as access control.
- Avoid logging passwords, tokens, session identifiers, or sensitive personal data.

## Secrets and dependencies

- Read secrets from an approved secret store or environment; never hard-code them.
- Add dependencies only when needed; prefer maintained packages and pin versions when appropriate.
- Run dependency and secret scanning tools when available.
- Review package install scripts, transitive dependencies, lockfile changes, and permissions before adding or upgrading packages.
- Use a restrictive Content Security Policy and security headers appropriate to the app; never put secrets in client-side bundles.

## Errors and operations

- Return safe errors to users; keep sensitive implementation details out of responses.
- Preserve security-relevant audit events without logging sensitive values.
- Use timeouts and resource limits for network calls and expensive operations.
- Apply rate limits and abuse controls to authentication, public APIs, expensive operations, and sensitive workflows.
- Make security-sensitive operations safe under retries: use idempotency or replay protection where appropriate.
- Encrypt sensitive data in transit and at rest using platform-supported mechanisms; minimize collection and retention.
- Keep development, test, and production credentials and data separate.
- Keep security settings enabled; do not disable checks to get a green build.

## Verification

- Add or update tests for normal behavior, invalid input, and access-control boundaries.
- Run relevant tests, linting, type checks, and available security scans.
- Review the final diff for accidental secrets, broad permissions, unsafe defaults, and unrelated changes.
- State which checks were run and which were not.
- Ensure tests include unauthenticated access, wrong-user/wrong-tenant access, invalid state transitions, and relevant abuse limits.
