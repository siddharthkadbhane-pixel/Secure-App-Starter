# Secure feature lifecycle

Use these gates for every app feature. Increase scrutiny when the feature touches identity, authorization, tenant boundaries, sensitive data, money, file handling, or external systems.

## 1. Define

- Name the user-visible behavior and the data it reads or changes.
- Identify every actor: anonymous user, signed-in user, organization member, administrator, service, and support operator as applicable.
- Classify data as public, internal, personal, sensitive, or secret. Collect the minimum and define retention/deletion expectations.
- Map trust boundaries: browser to server, service to service, tenant to tenant, and app to third-party provider.
- Record abuse cases: unauthorized access, account enumeration, brute force, spam, replay, resource exhaustion, malicious files, and forged callbacks as relevant.

**Gate:** Do not implement a sensitive flow until its actor permissions and data boundary are clear.

## 2. Design

- Choose established framework/provider mechanisms for authentication, sessions, cryptography, and validation.
- Write an authorization rule in positive terms and define the default-deny behavior.
- Decide how secrets are provisioned, rotated, and kept out of logs and client bundles.
- Define limits, timeouts, rate controls, safe error behavior, and audit events.
- Consider failure modes: provider outage, duplicate callback, partial write, retry, and stale permission.

**Gate:** Resolve or explicitly accept high-impact assumptions before generating implementation code.

## 3. Implement

- Enforce identity and authorization in trusted server-side code for every operation.
- Validate input at the boundary, then use safe APIs for database, filesystem, HTML, and process interactions.
- Keep risky features disabled until configuration is present; fail closed on missing security configuration.
- Avoid exposing internal identifiers, secrets, stack traces, or unnecessary personal data.
- Keep the change focused; document security-relevant decisions near the code or in project docs.

## 4. Verify

- Test positive and negative authorization cases, including a different user and a different tenant.
- Test malformed, oversized, repeated, expired, and unexpected inputs as relevant.
- Test state changes and callbacks against duplicate delivery, invalid signatures, and out-of-order events where relevant.
- Run project tests, static analysis, secret scanning, dependency auditing, and configuration scans available for the stack.
- Review the diff for accidental secrets, unsafe defaults, debug endpoints, permissive CORS, and disabled controls.

**Gate:** A failed required security check blocks release until fixed or formally risk-accepted.

## 5. Release and operate

- Use separate least-privilege credentials per environment; production secrets must come from the approved secret manager.
- Verify HTTPS, secure cookie settings, allowed origins, security headers, backups, and access logging in the deployed environment.
- Have a way to revoke credentials, disable a risky feature, and respond to a suspected exposure.
- Track unresolved risks with an owner, severity, mitigation, and review date. Do not call a checklist proof of security.
