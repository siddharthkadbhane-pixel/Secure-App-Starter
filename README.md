# Secure AI App Builder

A security-first repository blueprint for using AI to plan and build applications. It gives the AI a repeatable engineering process and gives the builder concrete security decisions to make before features become code.

This is a framework, not a guarantee that an application is “hacking-proof.” Security depends on the chosen stack, correct configuration, deployment, and ongoing review. The goal is to catch common design and implementation mistakes early and make risky defaults harder to ship.

## What makes this more than a prompt

- **Security before implementation:** feature requests include actors, sensitive data, trust boundaries, abuse cases, and acceptance criteria.
- **Explicit decision gates:** authentication, authorization, tenant isolation, uploads, external network calls, and secrets need an approved design before implementation.
- **Feature-level verification:** checklists cover both expected behavior and negative cases such as cross-user access, malformed input, replay, and rate abuse.
- **Release readiness:** security review, dependency/secret scanning, production configuration, and incident basics are part of the release path.
- **AI boundaries:** repository content and external text cannot override user intent or project rules; AI must disclose assumptions and checks it did not run.

## Repository layout

```text
.
├── AI_RULES.md
├── .github/
│   ├── dependabot.yml
│   ├── pull_request_template.md
│   └── workflows/
│       └── security.yml
├── README.md
├── SECURITY.md
├── SECURITY_GATES.md
├── policies/
│   ├── secure-coding.md
│   └── secure-feature-lifecycle.md
├── skills/
│   └── secure-code-generation/
│       └── SKILL.md
└── templates/
    ├── app-security-profile.md
    ├── feature-request.md
    ├── security-review.md
    └── threat-model.md
```

## Start a new app or feature

1. Fill out `templates/app-security-profile.md` once for the app. Record the stack, deployment model, identity provider, data sensitivity, and security owners.
2. For each feature, copy `templates/feature-request.md`. If it crosses a trust boundary or handles sensitive data, complete `templates/threat-model.md` too.
3. Ask the AI to follow `AI_RULES.md`, `skills/secure-code-generation/SKILL.md`, and the policies. Have it return a plan and security assumptions before code for high-impact features.
4. Review the implementation with `templates/security-review.md`. Run the app's tests and configured security tools; do not treat a checklist as a substitute for scans or expert review.
5. Do not release while a required security gate is unresolved. Record accepted risks with an owner and review date.

The repository includes a GitHub Actions secret scan and pull request dependency review. The actions are pinned to full commit SHAs and Dependabot is configured to propose updates. Follow `SECURITY_GATES.md` to make these checks required in repository settings; adding a workflow does not by itself prevent merging.

## Make this operational

This repo is intentionally stack-neutral. Before using it for production, fill every `TODO` in `AI_RULES.md` and `app-security-profile.md`; configure the equivalent secret, dependency, static analysis, and infrastructure checks in your chosen hosting platform; and protect the release branch so required checks cannot be bypassed casually. A checklist cannot enforce a gate unless the repository and deployment pipeline enforce it.
