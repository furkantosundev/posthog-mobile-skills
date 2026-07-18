---
name: posthog-mobile
description: Design, implement, improve, or remediate a trustworthy PostHog measurement system for a mobile application. Use for end-to-end PostHog setup, growth measurement design, audit remediation, or refactoring events, properties, identity, attribution, privacy, and analytics architecture across React Native, Expo, native iOS, native Android, or Flutter.
---

# PostHog Mobile Orchestrator

Build the smallest trustworthy measurement system that can answer the product's next important growth decisions. Add capabilities only as maturity and evidence require.

## Non-negotiable operating rules

- Reason in this order: business question -> product decision -> metric -> observable behavior -> event/property -> analysis -> validation. Never begin with an arbitrary event catalog.
- Inspect the actual product, stack, installed PostHog SDK version, and official current PostHog documentation before giving version-sensitive API guidance. Never invent method names.
- Support React Native, Expo, native iOS, native Android, and Flutter without assuming any framework or repository layout.
- Prefer meaningful value signals over app opens, logins, empty registrations, or indiscriminate interaction tracking.
- Use AARRR only as a coverage check. Consider the critical journey, activation, repeated value, retention, acquisition, referral/content/invite, monetization, resurrection, and subscription or transaction lifecycles when relevant.
- Do not force autocapture, session replay, a North Star, experimentation, an attribution vendor, or scale governance.
- Keep product analytics separate from crash monitoring unless an explicit decision connects them.
- Never silently rename or remove established production events or properties.

## Workflow

1. Inspect repository code and product documentation. Discover framework, platforms, SDK and version, navigation, authentication, persistence, backend event sources, payments, current analytics, environments, privacy/ATT/deletion behavior, tests, and analytics definitions.
2. Determine whether a meaningful PostHog integration exists. Inventory initialization, capture, screens/lifecycle, identity, properties, flags/experiments, server ingestion, revenue, attribution, and documentation.
3. Establish the likely product value, critical journey, activation, repeated-value behavior, business model, growth loops, and next decisions. State assumptions; ask only questions that materially change the result.
4. Classify maturity and choose the lowest sufficient level:
   - **Foundation:** environments, initialization, identity, privacy, lifecycle/screens, critical journey, activation, few high-value signals, segmentation, validation.
   - **Growth:** acquisition, funnels, retention, monetization, loops, reactivation, campaign analysis, event ownership—only when relevant.
   - **Experimentation:** eligibility, assignment, exposure, metrics, guardrails, contamination control, rollout, kill switches, cleanup—only with a real need and sufficient traffic.
   - **Scale:** governance, migrations, warehouse, reconciliation, sampling, volume budgets, advanced attribution, groups, ownership—only when operationally justified.
5. If no trustworthy integration exists, execute the complete initialization workflow documented here: discover the app; draft the product measurement foundation; create a minimum measurement plan; design event/property, identity, lifecycle, source-of-truth, privacy, and attribution contracts; implement; test; validate payloads. If the active environment can discover a compatible `posthog-mobile-init` sibling, it may delegate. Otherwise execute these instructions directly.
6. If an integration exists, execute a read-only audit first: compare decision coverage, code, runtime frequency, identity transitions, tests, documentation, payloads, and approved dashboard state; prioritize evidence-backed defects and risks. If the active environment can discover `posthog-mobile-audit`, it may delegate. Otherwise reproduce this audit directly.
7. Translate the next product questions into a minimum viable plan. For every signal record the decision, metric, trigger, source of truth, properties, cardinality, ownership, validation, and consuming analysis. Every event must earn its place.
8. Present material assumptions, tradeoffs, schema decisions, and historical implications.
9. Obtain approval before changing established semantics, identity, historical continuity, attribution, privacy/ATT behavior, production dashboards, feature flags, experiments, or external systems. Do not stop for minor implementation choices.
10. Implement the approved scope through one adapter and typed contracts when useful. Prefer authoritative server outcomes for financial transactions, subscription state, balance changes, and completed backend jobs; distinguish client intent from server truth and prevent double counting.
11. Update application code, tests, and analytics documentation together. Do not wire speculative future events.
12. Validate proportionately: environments, payload shape, identity continuity, deduplication/idempotency, retries, timestamps, null/enums, test users, cardinality, volume/cost, reconciliation, privacy, and actual payloads in an available debugger. Never claim external validation without access.
13. Re-run relevant audit checks.

## Measurement and contract minimum

Distinguish native lifecycle events, native screen events, custom events, event properties, super-properties, mutable person properties, and immutable person properties. Do not duplicate reliable native signals. Use occurrence context on events, persistent segmentation state as super-properties, and only meaningful person/install attributes on profiles. Avoid repeated profile writes, sensitive content, uncontrolled strings, and mirrored concepts across layers.

Define anonymous-to-identified transition, canonical identifier, switching, logout/reset, reinstall, deletion, fresh post-deletion identity, cross-device limits, and client/server consistency. Do not expose device identifiers. Define lifecycle terms such as install, first seen, account created, and first value before storing timestamps; use `_at` for explicit timestamps and define null/unknown behavior.

## Completion report

Report decisions, implementation changes, historical-data implications, dashboard/migration work, privacy and attribution implications, validation evidence, external configuration still required, and deliberately deferred capabilities with reasons. Recommend one North Star candidate only when evidence supports it; otherwise state what would validate the hypothesis.
