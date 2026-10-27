# Enforce the security gates

Workflow files create checks. Repository settings must make those checks and human review mandatory before code can merge.

## GitHub repository settings

Before production use, configure the following in the GitHub repository:

1. **Ruleset or branch protection for the default branch**
   - Require pull requests; require at least one approval from a person other than the author.
   - Dismiss stale approvals when new commits are pushed and require approval of the latest reviewable push.
   - Require all conversations resolved.
   - Require the `Secret scan` and `Dependency review` status checks after their first successful run. Add the app's test and code-scanning checks too.
   - Require a security owner to review changes to `.github/workflows/**`, `.github/dependabot.yml`, `AI_RULES.md`, `policies/**`, and `skills/**`. Add real maintainers to `CODEOWNERS` and require code-owner approval. A pull request can edit its own workflow, so these files need trusted review.
   - Block force pushes and branch deletion; restrict bypass to a small, named emergency group and audit bypass use.
2. **Secret protection**
   - Enable secret scanning and push protection where available. Treat leaked credentials as compromised: revoke/rotate them; removing a string from the latest commit is not enough.
   - Enable private vulnerability reporting in repository settings, or put a monitored security contact in `SECURITY.md`. The starter's `TODO` is not a usable disclosure channel.
3. **Dependency security**
   - Enable Dependabot alerts and security updates. Review update PRs; do not auto-merge major or security-sensitive changes without verification.
4. **Code scanning**
   - Configure code scanning for the languages in the app and require its results before merge. The right setup depends on language and GitHub plan; do not claim CodeQL is active until a scan appears in the repository's Security tab.
5. **Workflow trust**
   - Keep `GITHUB_TOKEN` permissions read-only by default. Use separate, narrowly scoped jobs for write operations.
   - Never run untrusted pull request code in `pull_request_target` with secrets or write permissions.
   - All Actions in the sample workflow are pinned to full commit SHAs. Let Dependabot propose SHA updates and verify the publisher and release before accepting them.
   - Do not use self-hosted runners for untrusted public pull requests unless they are disposable and isolated.

## Local and app-specific gates

The included workflow checks secrets and changed dependencies. Gitleaks comments and artifact upload are disabled; its GitHub token has read-only workflow permissions. For organization-owned repositories, configure the `GITLEAKS_LICENSE` Actions secret. Dependency Review fails on known vulnerabilities from low severity upward in runtime, development, and unknown dependency scopes. It needs GitHub dependency graph support; private repositories may also need the required GitHub Advanced Security entitlement. It does not know the app's programming language, build system, infrastructure, auth model, or runtime configuration. Add and require the correct tests, static analysis, infrastructure scan, and deployment checks after choosing the stack.

## Verify enforcement

Open a test pull request and confirm that required checks run and a failed required check blocks merging. Also verify that an ordinary contributor cannot bypass the rules. Review the settings after repository transfers or plan changes.
