# Dashboard Dependency and Migration

Use this as a read-only inspection checklist or as a manual checklist when authenticated PostHog access is unavailable. Do not mutate dashboards or external state in audit mode.

## Dependency inventory

For every affected event/property, identify:

- Insights, trends, funnels, paths, retention reports, cohorts, dashboards, subscriptions/alerts.
- Feature flags, experiments, surveys, annotations, actions/derived definitions.
- Exports, warehouse models, reverse ETL, webhooks, CDP destinations, advertising forwarding, APIs, notebooks, and scheduled reports.
- Owners, audiences, decision cadence, filters, breakdowns, formulas, date windows, and historical expectations.

Record verified dependencies separately from items requiring an owner to check. Never imply external inspection without access.

## Rename and semantic impact

Determine whether the proposal is:

- A display/naming cleanup with unchanged meaning.
- A property type/enum/null correction.
- A trigger or population change that breaks historical comparability.
- A source-of-truth/identity change that can alter counts and attribution.

Do not silently reuse an existing name for new meaning. Document the last comparable date and expected discontinuity.

## Choose the least costly migration

Prefer, in order when valid:

1. Fix producer behavior without renaming when semantics remain the same.
2. Use an analysis-time derived property/action when it can express the correction reliably.
3. Introduce an additive field while preserving the event meaning.
4. Rename/version only when meaning materially changes and comparison would mislead.

### Dual-write criteria

Dual-write only when important consumers cannot cut over atomically, an overlap window provides measurable validation value, and duplicate interpretation can be controlled. Define start/end dates, owners, cost, deduplication/query rules, and removal test. Do not leave dual-write indefinite.

## Backfill limitations

A backfill can transform stored facts but cannot reconstruct unobserved client context, genuine exposure, deleted identity, consent status, missing attribution evidence, or reliable occurrence time. Mark modeled/imputed data and avoid mixing it invisibly with observed events. Confirm whether the analytics platform and downstream systems support the intended correction before promising it.

## Consumer migration

For each insight/funnel/cohort/report:

1. Capture the current definition and baseline result.
2. Create or specify the replacement definition without mutating in audit mode.
3. Define historical window and comparability expectations.
4. Validate counts, unique users, identity, ordering, exclusions, breakdowns, and revenue totals.
5. Update dependent dashboards, alerts, experiments/flags, and pipelines through the approved remediation workflow.
6. Record owner and cutover date.

## Cutover and validation

Choose atomic cutover or time-bounded overlap. Validate producer payloads, event volume, unique identities, funnel conversion, retention cohorts, revenue reconciliation, attribution distribution, and downstream deliveries. Establish rollback conditions for privacy, identity, financial, or severe data-quality regressions.

## Deprecation

After the agreed observation window, stop old producers, remove dual-write, archive or annotate obsolete consumers, update contracts/tests, and communicate the last reliable historical date. Preserve definitions needed to interpret old data. Confirm no active dependency remains before deletion.

## Manual checklist when access is unavailable

Ask an authorized owner to export or inspect: event/property usage, saved insights, funnels, retention, cohorts, dashboards, flags, experiments, surveys, alerts, data pipelines, forwarding destinations, and recent volume. Request definitions or screenshots rather than credentials. Label all conclusions pending until evidence is returned.
