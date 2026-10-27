# Lightweight threat model

Complete for features that cross trust boundaries or handle sensitive data. Keep it short, specific, and tied to the proposed change.

## Scope and assets

- Feature/change:
- Assets to protect (accounts, data, money, service availability, secrets):
- Out of scope:

## Actors and trust boundaries

- Anonymous users:
- Authenticated roles/tenants:
- Services/providers:
- Where does untrusted input enter and where does it go?

## Data flow

Describe the request, validation, authorization, storage, and response path. Note sensitive fields and where they are stored or logged.

## Abuse cases

| Threat | Impact | Mitigation | Verification |
| --- | --- | --- | --- |
| A user accesses another user's/tenant's object | Data exposure or modification | Enforce ownership/tenant scope server-side | Negative cross-user and cross-tenant tests |
| Invalid or oversized input reaches a sensitive operation | Injection, crash, or resource exhaustion | Validate schema and apply limits | Boundary and size tests |
| Repeated or forged action/callback | Duplicate action or unauthorized state change | Rate limit, verify authenticity, and make idempotent where needed | Replay/invalid-signature tests |
| TODO: add feature-specific abuse case | TODO | TODO | TODO |

## Decisions and open risks

- Security decisions:
- Assumptions that must be confirmed:
- Risk owner and review date for accepted risks:
