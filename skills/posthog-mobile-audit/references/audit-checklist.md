# Detailed Audit Checklist

Record evidence with file/line, runtime trace, test, payload, or approved read-only external reference. Separate confirmed defects, probable risks, and maturity options.

## Growth coverage

- Reconstruct product value, critical journey, activation hypothesis, repeated-value behavior, business model, loops, maturity, and next decisions.
- Map each documented event/metric to a business question, product decision, analysis, and validation. Identify orphan signals and unanswered material decisions.
- Test whether activation predicts retention/value rather than assuming registration or login does.
- Check acquisition, abandonment, retention/resurrection, monetization/value linkage, referral/content/invite loops, inputs, outcomes, diagnostics, and guardrails only where relevant.
- Use AARRR as a gap check. Do not penalize justified Foundation scope for lacking Experimentation or Scale capabilities.

## Event architecture

- Inventory native lifecycle/screens, custom events, autocapture, session replay, adapter calls, and raw SDK bypasses.
- Compare exact trigger semantics and runtime frequency. Find duplicate lifecycle/screens, overlapping milestones, success events emitted on intent, and low-value interaction noise.
- Verify naming consistency with the existing project without imposing a universal convention.
- Confirm every event has an owner, source of truth, consuming analysis, and validation route.

## Properties

- Classify event, super-, mutable person, and immutable person properties.
- Find duplicated concepts, wrong layers, stale super-properties, repeated profile writes, incorrect immutable defaults, and render/activation write amplification.
- Verify types, units, bounded enums, null/omitted/unknown semantics, timestamp `_at` meaning, boolean truth, cardinality, sensitivity, and necessity.
- Ensure install, first seen, account created, and first value are not conflated.

## Identity

- Trace fresh anonymous use, authentication, canonical identifier binding, alias/merge behavior, account switching, logout/reset, cross-device behavior, reinstall, deletion, and fresh post-deletion identity.
- Verify client/server identifiers agree and no raw device identifiers leak to logs/docs.
- Test for pre-login loss, duplicate people, account contamination, stale user properties, and reconnecting deleted identity.

## Lifecycle

- Trace cold/warm start, foreground/background, navigation, process recreation, development reloads, and platform-specific scenes/activities.
- Compare SDK defaults and actual installed-version behavior with current official PostHog documentation.
- Detect duplicate automatic/manual lifecycle or screens and misleading session assumptions.

## Source of truth

- Assign each material outcome to client or server. Client UI intent must not masquerade as authoritative completion.
- Verify server ownership of completed backend jobs, balances/credits, subscription state, and financial outcomes when applicable.
- Inspect correlation, idempotency, retries, delivery guarantees, reconciliation, authentication, and duplicate client/server emission.

## Revenue

- Trace intent, checkout, purchase, renewal, failure, cancellation, refund, recovery, currency, amount/value, product/plan, transaction identifier, and authoritative status.
- Compare analytics totals to payment/subscription source of truth and document timing, taxes, currency conversion, and refund semantics.
- Treat missing lifecycle stages as defects only if decisions require them.

## Experimentation

- Confirm a real hypothesis and sufficient maturity/traffic before assessing completeness.
- Inspect eligibility, assignment unit, stable assignment, actual exposure moment, primary/secondary metrics, guardrails, contamination, runtime, rollout, fallback, kill switch, and stale-flag cleanup.
- Detect exposure recorded for ineligible/unaffected users or repeated flag evaluation that inflates exposure.

## Attribution

- Separate channel, source, campaign, content, and referral evidence.
- Classify evidence as deterministic, self-attributed, aggregate, or unknown. Reject “not paid = organic.”
- Inspect campaign links, Universal/App Links, deferred deep links, referral/creator codes, surveys, Apple Ads/AdServices, SKAdNetwork/AdAttributionKit, Android mechanisms, and provider callbacks when applicable.
- Verify first/last/current-touch semantics, overwrite behavior, link fallback, fraud/abuse controls, and reconciliation.

## Privacy

- Inventory collected and forwarded data, PII/sensitive/free-text/high-cardinality fields, identifiers, retention, access, and destinations.
- Trace consent unknown/opt-in/opt-out, queue behavior, ATT/IDFA boundaries, advertising forwarding, minimization, and safe defaults.
- Trace deletion across local SDK state, product backend, PostHog, queues, warehouse/exports, attribution and advertising systems. Do not make legal conclusions; identify evidence and policy gaps.

## Data quality

- Verify development/staging/production isolation, internal/test-user filtering, payload schema, required/optional properties, enums, nulls, timestamps/clock skew, ordering, offline queues, retry duplicates, queue loss, and SDK compatibility.
- Compare code, contract docs, tests, live debugger payloads when accessible, and authoritative server records.
- Never claim live or dashboard validation without authenticated access.

## Cost

- Estimate events per active user, duplicate/retry amplification, autocapture/replay volume, property size/cardinality, person-profile writes, and server duplicates.
- Identify unused signals before suggesting sampling. Evaluate whether sampling preserves rare conversions, financial truth, and analytical weighting.

## Documentation

- Compare event definitions, trigger examples, ownership, properties, identity, consent, environments, source of truth, tests, dashboards, and deprecation state against code.
- Identify undocumented raw capture, stale catalogs, incompatible tests, and undefined decision consumers.

## Migration

- Inventory all producers and consumers before proposing semantic changes.
- Determine whether history remains comparable, whether a derived property suffices, and whether dual-write/versioning has a justified overlap need.
- Identify backfill feasibility and limits, dashboard/pipeline cutover, validation, deprecation owner/date, and rollback.

## Evidence standard

Use **Confirmed** only when direct code, runtime, payload, test, documentation contradiction, or approved external state proves the issue. Use **Probable** when architecture and call paths make the risk likely but runtime/external evidence is unavailable. Severity reflects impact on decisions, identity/privacy, financial truth, historical continuity, or cost—not code style.
