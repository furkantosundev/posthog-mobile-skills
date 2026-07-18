---
name: posthog-mobile-init
description: Initialize PostHog and a minimum viable growth measurement system in a mobile application that lacks a trustworthy implementation. Use to discover and implement decision-led analytics, identity, lifecycle, source-of-truth, privacy, attribution, tests, and data-quality validation for React Native, Expo, native iOS, native Android, or Flutter.
---

# Initialize PostHog Mobile Analytics

Build the smallest trustworthy system that answers the product's next important growth decisions. Do not start from a stock event catalog.

## Rules

- Follow: business question -> product decision -> metric -> observable behavior -> event/property -> analysis -> validation.
- Discover the real framework, platforms, installed SDK and version before implementation. Consult current official PostHog documentation for version-sensitive APIs and capabilities; never rely on remembered method names.
- Classify maturity as Foundation, Growth, Experimentation, or Scale and implement only the lowest sufficient level. Treat AARRR as a coverage check, not an architecture.
- Prefer behaviors proving value over app opens, logins, or empty accounts. Do not force a North Star, autocapture, replay, experiments, attribution vendors, or future governance.
- Ask only questions that materially change product, identity, privacy, or schema decisions. Present reasonable assumptions for confirmation.
- Obtain agreement on material product, identity, privacy, attribution, and schema decisions before writing code. Minor implementation details need no separate gate.

## Workflow

1. **Discover the application.** Inspect framework, platforms, SDK/version, navigation, authentication and anonymous identity, persistence, backend sources, payment truth, analytics/observability vendors, environments, consent/ATT/deletion, documentation, and existing definitions.
2. **Draft the foundation.** State product value, critical journey, activation/aha behavior, repeated value and retention, business model, relevant acquisition/retention/monetization/referral/content loops, next decisions, maturity, and minimum scope. Read [growth foundations](references/growth-foundations.md) when defining metrics, loops, retention, or experiments.
3. **Create the measurement plan.** For every signal document business question, decision, metric, native/custom signal, exact trigger, owner/source of truth, required properties, cardinality, client/server ownership, validation, and consuming analysis. Use [measurement model](references/measurement-model.md).
4. **Design the contract.** Distinguish native lifecycle, native screen, custom event, event property, super-property, mutable person property, and immutable person property. Do not duplicate reliable native signals. Define lifecycle timestamps, bounded enums, null/unknown behavior, naming consistent with the project, and sensitive/high-cardinality exclusions.
5. **Design identity and lifecycle.** Define anonymous identity, transition to the canonical identifier, account switching, logout/reset, reinstall, deletion, fresh identity after deletion, cross-device limits, and client/server consistency. Never expose raw device identifiers.
6. **Assign source of truth.** Prefer server truth for purchases, renewals, refunds, subscription state, balances/credits, completed backend jobs, and financial transactions. Separate intent and outcome when both matter; require deduplication and transaction idempotency.
7. **Consider attribution and privacy.** Read [attribution and privacy](references/attribution-privacy.md) whenever acquisition, advertising, ATT, consent, deep links, forwarding, or deletion is in scope. Never infer organic merely because paid evidence is absent.
8. **Implement the minimum sufficient system.** Adapt current official SDK guidance to the discovered stack: environments, initialization, one adapter, typed contracts where beneficial, identity, native lifecycle/screens, critical custom events, authoritative server outcomes, privacy controls, documentation, and tests. Read [implementation patterns](references/implementation-patterns.md). Do not wire every future event.
9. **Validate.** Check environment isolation, duplicate signals, idempotency, offline retry, timestamps/clock skew, required and optional fields, enums/nulls, test-user filtering, cardinality, volume/cost, reconciliation, identity continuity, consent/deletion, and actual payloads in an available live debugger or equivalent. Do not claim external validation without authenticated access.

## Contract rules

- Use custom events only for meaningful behaviors, state transitions, funnel milestones, or intra-screen actions unavailable from reliable native signals.
- Put occurrence context on event properties; persistent segmentation state on super-properties; meaningful person/install attributes on profiles. Do not mirror a concept across layers without a query need.
- Avoid person writes during renders, routine refreshes, or repeated activation. Use immutable writes only for genuinely immutable values.
- Use precise semantics, `_at` for timestamps, and booleans describing observations. Define install, first seen, account created, and first value separately before storing them. Store derived time fields only for a justified query or operational constraint.
- Prefer bounded enums; explicitly define `unknown`, null, and omitted behavior. Avoid PII, sensitive content, and uncontrolled high-cardinality values.

## Experimentation gate

Do not enable experiments automatically. When product need and traffic justify one, define hypothesis, eligible population, assignment unit, exposure moment, primary and secondary metrics, guardrails, expected direction, runtime considerations, contamination risks, and rollout/rollback. Evaluate eligibility before exposure where possible; keep flag delivery separate from business logic and provide safe fallback behavior.

## Output

Return the foundation, maturity decision, minimum plan, analytics contract, implementation, tests, data-quality evidence, dashboard recommendations, privacy/attribution caveats, assumptions, and deferred capabilities with reasons.
