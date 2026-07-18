---
name: posthog-mobile-audit
description: Perform a strictly read-only audit of a mobile PostHog implementation for growth decision coverage, technical trustworthiness, identity, schema, attribution, privacy, cost, data quality, and migration risk. Use for React Native, Expo, native iOS, native Android, or Flutter analytics audits and evidence-backed findings without modifying code, documentation, dashboards, flags, experiments, configuration, or external systems.
---

# Audit PostHog Mobile Analytics

Remain strictly read-only. Do not modify application code, documentation, dashboards, feature flags, experiments, PostHog configuration, or any external system. If remediation is requested, route to a compatible `posthog-mobile` orchestrator when discoverable or reproduce its approval-gated workflow directly.

## Principles

- Audit whether the smallest trustworthy measurement system answers the product's next decisions—not whether every PostHog feature is used.
- Follow: business question -> product decision -> metric -> observable behavior -> event/property -> analysis -> validation.
- Discover the actual framework, platforms, installed SDK and version. Check version-sensitive behavior against current official PostHog documentation; never assume remembered APIs.
- Treat AARRR as a coverage check. Do not label advanced capabilities defects when product maturity does not justify them.
- Distinguish confirmed defects, probable design risks, and optional maturity improvements. Do not report stylistic preferences.

## Workflow

1. Discover product value, critical journey, activation, repeated value, business model, loops, maturity, stack, SDK/version, and stated growth model.
2. Identify the product decisions the current system is expected to support.
3. Inventory initialization, capture calls, native lifecycle/screens, adapter boundaries, identify/alias, person and immutable writes, super-properties, reset/logout/deletion, flags/exposure, server ingestion, payments/subscriptions, attribution, deep links, tests, and documentation.
4. Trace runtime call frequency and identity transitions, including render/activation repetition, account switching, logout, reinstall, and deletion.
5. Compare documentation, code, tests, available payload evidence, and dashboards only where authenticated, approved read-only access exists.
6. Evaluate technical trustworthiness and growth decision coverage using [the detailed audit checklist](references/audit-checklist.md).
7. Prioritize evidence-backed findings. Report none when no material issue exists.

## Growth questions

Determine whether trustworthy data can answer: where valuable users come from; critical-journey abandonment; activation and its relationship to retention; repeated value; inputs influencing outcomes; guardrails; connection between monetization and value; referral/content/invite loops; resurrection; and which events support actual decisions. Flag low-value activity only when it crowds out or distorts meaningful signals.

## Technical risks

Check for adapter bypass, duplicate native/custom lifecycle or screens, overlapping events, duplicate semantics, wrong property layers, excessive identity/profile writes, stale super-properties, bad immutable defaults, misleading timestamps/booleans, identity discontinuity, account contamination, deletion failures, client/server double counting, missing idempotency, retry duplicates, environment contamination, schema drift, unbounded/high-cardinality values, sensitive payloads, volume/cost risk, missing payload QA, version incompatibility, documentation/test drift, and historical migration risk.

## Attribution and privacy

Audit channel/source/campaign separation; evidence for defaults; deterministic, aggregate, self-attributed, and unknown evidence; Apple Ads/AdServices; SKAdNetwork or AdAttributionKit; attribution provider behavior; Universal Links and deferred deep links; campaign links and referral codes; surveys; ATT/IDFA; consent, opt-out, deletion, minimization, and advertising forwarding.

Never infer organic from missing paid evidence, describe deferred deep linking as an ATT bypass, present aggregate attribution as deterministic user-level evidence, or assume a vendor is required.

## Dashboard-aware audit

With approved read-only access, inspect dependencies in insights, funnels, retention, cohorts, dashboards, flags, experiments, surveys, alerts, and pipelines. Without access, finish the repository audit, explicitly state that external state was not verified, and use [dashboard migration](references/dashboard-migration.md) for a focused manual checklist. Never imply access that was unavailable.

## Findings format

For each material finding provide:

- Severity: Critical, High, Medium, or Low
- Confidence: Confirmed or Probable
- Category: Growth, Data quality, Identity, Schema, Attribution, Privacy, Cost, or Migration
- Finding and concrete evidence
- Why it matters and the product decision affected
- Recommended decision
- Migration/historical-data risk
- Suggested remediation

Use clickable file and line references when supported. Conclude with audit scope, maturity assessment, validation performed, inaccessible external dependencies, and optional improvements clearly separated from defects.
