# Measurement Model

## Decision-first chain

For every measurement, complete:

1. **Business question:** what uncertainty matters?
2. **Product decision:** what action changes for each plausible answer?
3. **Metric:** what quantitative definition distinguishes the answers?
4. **Observable behavior/state:** what can reliably be observed?
5. **Signal:** native event, custom event, property, or authoritative server record.
6. **Analysis:** funnel, trend, cohort, retention, path, experiment, or reconciliation.
7. **Validation:** how payload and interpretation will be proven.

If the decision is vague or no action changes, defer the event.

## Signal boundaries

- **Native lifecycle event:** SDK/platform-generated app lifecycle signal. Do not recreate it unless reliability or semantics are inadequate and documented.
- **Native screen event:** navigation/screen signal. Avoid parallel custom screen events.
- **Custom event:** meaningful behavior, state transition, milestone, or intra-screen action not reliably answered otherwise.
- **Event property:** context unique to one occurrence, including result, source, or bounded state at that moment.
- **Super-property:** persistent state required to segment subsequent events. Define registration, update, and removal behavior to prevent stale values.
- **Mutable person property:** meaningful current person/install attribute used across analyses.
- **Immutable person property:** a truly first-write-only attribute. Never use immutable defaults for facts that can be corrected or change.

Do not mirror a concept across event, super-, and person properties without a demonstrated query need. Avoid profile updates from renders, routine refreshes, or every activation.

## Lifecycle and timestamps

Define “install,” “first seen,” “account created,” “first value,” subscription start, and other lifecycle concepts independently before creating fields. Use `_at` for explicit timestamps and one canonical timestamp per defined concept. Prefer ingestion time when event occurrence is immediate; send occurrence time when delayed/offline/server processing requires it and validate clock provenance.

Do not store elapsed-day or derived cohort fields unless a query or operational constraint requires them; derive them in analysis when possible.

## Values and cardinality

For every property define type, unit, allowed values, required/optional status, and absent behavior:

- Use bounded enums with documented fallback values.
- Use `unknown` only when the concept exists but cannot be determined; use null or omission according to the query contract, consistently.
- Do not use empty strings as unknown.
- Distinguish “not applicable,” “not yet known,” and “collection prohibited” when decisions require it.
- Avoid free-form text, URLs with query values, raw errors, identifiers, and sensitive content unless minimized and justified.

## Client/server ownership

Choose a single owner for each outcome. The client may own observable intent and UI state; the server should own authoritative purchases, renewals, refunds, balances, subscription state, financial transactions, and completed backend work. When both are useful, name distinct intent and outcome semantics rather than emitting the same event twice. Reconcile using non-sensitive correlation/idempotency keys where appropriate.

## Measurement-plan template

| Field | Required decision |
|---|---|
| Business question | Uncertainty being reduced |
| Product decision | Action changed by the answer |
| Metric | Formula, unit, population, window |
| Signal | Native/custom event or state |
| Trigger | Exact observable moment and success/failure semantics |
| Owner | Team/system and source of truth |
| Properties | Types, enums, requiredness, sensitivity |
| Cardinality | Expected bounds and risky dimensions |
| Execution | Client, server, or both with distinct semantics |
| Validation | Unit/integration/payload/reconciliation evidence |
| Analysis | Intended report and segmentation |

## Minimum viable contract

Include only signals required for the critical journey, activation hypothesis, repeated value, relevant monetization truth, essential segmentation, and data-quality diagnosis. A fixed event count is inappropriate; scope follows decisions.

For each signal document name, semantic definition, trigger/non-trigger examples, owner, properties, identity state, consent behavior, deduplication expectations, and tests.

## Evolution and migration

Prefer additive correction when semantics remain valid. Do not version events merely because implementation changes. Version or rename only when meaning changes materially and historical comparison would mislead. Before any breaking change inventory dashboard and pipeline dependencies, choose cutover/dual-write/derived-property treatment based on historical needs, define overlap and deprecation dates, and document comparability limits. Never silently repurpose an existing name.
