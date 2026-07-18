# Attribution and Privacy

Treat attribution as evidence with confidence, not a single always-correct user property.

## Taxonomy and confidence

Keep dimensions distinct:

- **Channel:** broad class such as paid search, organic social, referral, direct/unknown.
- **Source:** platform, partner, referring domain, creator, or referrer mechanism.
- **Campaign:** marketer-controlled initiative identifier.
- **Content/creative/term:** optional bounded campaign detail when decisions require it.

Preserve raw permitted evidence separately from normalized classifications. Record evidence origin and confidence:

1. **Deterministic:** authenticated referral/invite code, campaign link parameters, or provider-confirmed user/session match within policy.
2. **Self-attributed:** user survey; valuable but subject to recall and response bias.
3. **Aggregate:** privacy-preserving campaign measurement such as SKAdNetwork/AdAttributionKit outputs; do not present as user-level truth.
4. **Unknown:** evidence unavailable, stripped, dark social, or collection prohibited. Never relabel as organic solely because paid evidence is absent.

Define first-touch, last-touch, and current-session semantics only when analyses require them. Avoid one mutable field that overwrites all attribution history.

## Link and platform mechanisms

- Use Universal Links/App Links for deterministic web-to-installed-app routing when configured and verified.
- Deferred deep links attempt to retain routing context across install; they do not bypass ATT, platform privacy rules, or attribution limits. Evaluate reliability, fallback, provider data use, and user experience.
- Support paid and organic campaign links with a controlled parameter schema and allowlisted destinations.
- Referral/creator/invite codes can provide deterministic product attribution when validated server-side and resistant to abuse.
- Self-attribution surveys help recover dark social and offline influence; keep “other/unknown” honest and avoid forcing an answer.

For Apple Ads/AdServices and SKAdNetwork or AdAttributionKit, inspect current Apple and PostHog documentation, platform availability, privacy thresholds, latency, and aggregation. Do not conflate these mechanisms or promise deterministic identity. On Android, likewise verify current install-referrer and privacy-platform behavior rather than assuming parity.

## Provider evaluation

Do not require a mobile measurement partner. Evaluate a provider only when acquisition spend, cross-channel normalization, deep-link reliability, fraud controls, or reporting operations justify cost and data sharing. Compare platform coverage, deterministic versus modeled outputs, privacy posture, SDK weight, raw-data access, deletion, forwarding, lock-in, and reconciliation.

## ATT, IDFA, and consent

ATT governs tracking across other companies' apps/sites and access to IDFA on Apple platforms; it is not a blanket analytics consent model. Map applicable laws, platform rules, product policy, and vendor configuration with qualified privacy/legal input. Do not access or forward advertising identifiers before the required authorization.

Define:

- What is collected before consent, after opt-in, after opt-out, and when status is unknown.
- Whether consent is device-, install-, or account-scoped and how it syncs.
- Safe defaults when consent state cannot be loaded.
- How queued events behave after opt-out.
- Which destinations receive each event and property.

## Data minimization and forwarding

Collect only fields tied to decisions, with retention and access appropriate to sensitivity. Avoid free text, precise location, contacts, health/financial content, raw tokens, device identifiers, and user-generated content by default. Hashing does not automatically make personal data anonymous.

Treat advertising forwarding as a separate disclosure and consent decision. Maintain allowlists for forwarded events/properties; do not forward product payloads wholesale.

## Deletion

Document the end-to-end deletion path: product database, PostHog/person data where applicable, server queues, exports/warehouse, attribution providers, advertising destinations, local SDK state, backups/retention limitations, and audit evidence. Prevent post-deletion events from reconnecting to the deleted identity; create a fresh identity only if later use and policy permit it.

## Validation

Test attribution links, cold/warm launches, installed/not-installed flows, stripped parameters, unknown evidence, consent transitions, ATT states, account changes, deletion, and provider callbacks using synthetic data. Report what was verified and what remains external.
