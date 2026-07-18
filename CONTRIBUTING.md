# Contributing

Thank you for improving PostHog Mobile Skills.

## Principles

- Start from product decisions, not an arbitrary event catalog.
- Keep guidance app-agnostic, framework-conditional, and portable across Agent Skills-compatible clients.
- Verify version-sensitive PostHog APIs against current official documentation; do not encode remembered SDK methods as timeless facts.
- Preserve progressive maturity. Do not force autocapture, replay, experimentation, attribution vendors, event versioning, or governance machinery.
- Keep `posthog-mobile-audit` strictly read-only.
- Do not add application-specific events, repository layouts, harness invocation syntax, credentials, personal data, or production payloads.
- Avoid duplicating detailed explanations between skills; place reusable depth in the appropriate reference file.

## Changes

1. Open an issue for material changes to identity, privacy, attribution, event semantics, or suite architecture.
2. Keep each `SKILL.md` focused and below 500 lines.
3. Use imperative instructions and relative links to bundled references.
4. Validate every changed skill with `skills-ref validate skills/<skill-name>`.
5. Include realistic prompts that demonstrate the changed behavior in the pull request description.

Do not add a review skill. Remediation belongs to `posthog-mobile`; read-only inspection belongs to `posthog-mobile-audit`.
