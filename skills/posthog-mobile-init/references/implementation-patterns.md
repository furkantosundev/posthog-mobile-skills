# Portable Implementation Patterns

Verify every version-sensitive API and default against current official PostHog documentation for the installed SDK and target platform before writing code. Examples here are architectural, not method-name prescriptions.

## Initialization and environments

- Discover the actual framework, native targets, build system, and installed SDK/version.
- Keep project keys/hosts in environment-specific configuration. Separate development, staging, and production data by distinct projects or an explicitly governed environment dimension.
- Initialize once at the application composition root, after required consent decisions and before dependent tracking. Avoid secrets in mobile binaries; ingestion keys intended for clients are configuration, while administrative keys remain server-only.
- Explicitly decide native lifecycle/screen capture, autocapture, session replay, persistence, queue, and flush behavior. Do not enable optional capture by default.

## Adapter and typed contract

Expose one application-owned analytics boundary rather than scattering raw SDK calls. Keep vendor translation, environment filtering, consent, common context, payload validation, and test substitution there. Audit for bypasses.

Use typed event/property contracts when the language and project benefit: bounded event names, per-event payload types, shared enum definitions, runtime validation at trust boundaries, and compile-time prevention of sensitive/unbounded fields. Do not create a complex schema framework for a tiny product.

## Identity lifecycle

Model states and transitions explicitly:

1. Fresh anonymous install/session uses an SDK-supported anonymous identifier or a privacy-safe app identifier.
2. Authentication binds future activity to the product's canonical stable account identifier using the installed SDK's documented transition semantics.
3. Account switching clears user-scoped super-properties and prevents the next account inheriting prior context.
4. Logout/reset follows the product's desired anonymous continuity semantics; verify behavior rather than assuming it.
5. Reinstall may create a new anonymous identity unless product authentication reconnects it. Document limitations.
6. Deletion stops or removes collection as policy requires, requests backend/vendor deletion through approved systems, clears local analytics state, and creates a fresh identity only if later use is allowed.

Use the same canonical identifier on client and server. Never log raw device identifiers or document real identifiers.

## Server truth and duplicate prevention

Emit authoritative financial and backend outcomes at the system that commits them. Attach a stable idempotency key for retryable outcomes and enforce deduplication at ingestion or producer storage where possible. Keep client intent and server result semantically distinct. Reconcile counts, values, currencies, statuses, and delayed outcomes against the source system.

## Offline queues, retries, and time

Inspect SDK defaults for persistence, batching, retry, queue limits, and data loss. Test process termination and connectivity transitions. Ensure retries do not create new logical IDs for idempotent outcomes.

Record occurrence time only when the event can be delayed; preserve timezone/UTC conventions and clock provenance. Detect unreasonable client clock skew. Server receipt time cannot always substitute for offline occurrence time, but client time is not inherently authoritative.

## Payload QA and testing

Layer validation proportionately:

- Contract/unit tests: accepted/rejected names, types, enums, null behavior, privacy filtering.
- Adapter tests: environment, consent, identity, common context, reset, super-property removal.
- Integration tests: navigation/lifecycle frequency, critical journey ordering, offline/retry, account switching and deletion.
- Server tests: idempotency, authentication, ownership, reconciliation, retry.
- Payload inspection: use an authenticated live debugger or equivalent only when available; verify actual names, types, distinct identity, timestamps, duplicates, and environment.

Never claim dashboard or live payload validation from code inspection alone. Use synthetic/test users and exclude them through a documented mechanism.

## Migration

Inventory producers and consumers before changing established semantics. Prefer fixing future data plus documenting the discontinuity when history cannot be safely transformed. Choose dual-write only when consumers need an overlap window and duplicate interpretation is controlled. Backfills cannot reconstruct unobserved client context and should not falsify occurrence time or identity.

## Cost, volume, and sampling

Estimate events per active user, retry amplification, property size/cardinality, optional autocapture/replay volume, and server duplication. Remove signals with no decision consumer before sampling. Sample only when volume is operationally meaningful and the analysis remains statistically interpretable; never sample rare conversions or financial truth casually. Document sampling unit, rate, stability, and weighting.

## Framework adaptation

- **React Native/Expo:** inspect managed vs native configuration, navigation integration, development reload behavior, and SDK compatibility with the installed Expo/React Native versions.
- **Native iOS:** inspect application/scene lifecycle, Swift/Objective-C integration, ATT boundaries, and background delivery.
- **Native Android:** inspect application/activity lifecycle, process recreation, consent, install/referrer sources, and background delivery.
- **Flutter:** inspect application lifecycle, navigator/route observation, platform channels, and plugin version compatibility.

Keep framework glue thin. Derive exact setup from current official PostHog documentation and the installed package manifest/lockfile.
