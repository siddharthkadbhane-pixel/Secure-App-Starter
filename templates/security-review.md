# Security review checklist

Feature/change: `TODO`  
Reviewer: `TODO`  
Date: `TODO`

## Access and identity

- [ ] Every protected operation checks authentication and server-side authorization.
- [ ] Ownership and tenant scope are checked on reads and writes.
- [ ] Denied and unauthenticated cases have tests.
- [ ] Session, recovery, and admin paths were considered where relevant.

## Data and input

- [ ] Input is schema-validated and bounded at the trust boundary.
- [ ] Queries, output encoding, file paths, and process calls use safe APIs.
- [ ] Sensitive data is minimized and excluded from logs/client bundles.
- [ ] Uploads, outbound requests, and webhook callbacks have feature-specific safeguards where relevant.

## Resilience and configuration

- [ ] Abuse controls, timeouts, and resource limits fit the feature.
- [ ] Security configuration fails closed; no permissive production fallback was added.
- [ ] Secrets and dependency changes were reviewed.
- [ ] Errors do not expose secrets, user data, or internal details.

## Evidence and decision

- [ ] Relevant tests and security tools ran; results are linked or summarized.
- [ ] Threat model was updated for new trust boundaries or sensitive data.
- [ ] Remaining risks have a named owner and review date.
- [ ] No unresolved critical/high risk is being shipped without explicit risk acceptance.

Decision: `Ready / Blocked / Risk accepted`  
Risk owner and expiry (if accepted): `TODO`
