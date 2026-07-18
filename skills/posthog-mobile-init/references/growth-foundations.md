# Growth Foundations

Use this reference to turn product context into a small, decision-worthy measurement system.

## Product value and behavior

Start with the user's desired progress, not product features. Express value as: “For [user/context], the product helps [outcome] by [mechanism].” Then identify:

- **Critical user journey:** the shortest coherent path from entry to experienced value.
- **Activation/aha:** observable behavior indicating the user likely experienced initial value—not merely registered or opened the app.
- **Repeated value/habit:** a behavior whose recurrence demonstrates continuing benefit.
- **Retention loop:** trigger -> return -> valuable action -> reward or renewed trigger.

Treat activation as a hypothesis until cohort evidence shows that activated users retain or monetize better. When context is weak, state competing definitions and the evidence that would distinguish them.

## Metric hierarchy

- **North Star candidate:** a durable measure of customer value delivered that can align teams. Propose at most one candidate when context supports it; never force one.
- **Outcome metrics:** results the product seeks, often lagging.
- **Leading/input metrics:** controllable behaviors likely to influence outcomes.
- **Diagnostic metrics:** explain why an outcome moved.
- **Guardrails:** detect unacceptable harm to quality, trust, revenue, reliability, or user welfare.

A good metric has a clear unit, population, time window, inclusion/exclusion rules, source of truth, and decision threshold. Counts without denominators or value context are often vanity metrics.

## Coverage without ceremony

Use AARRR—acquisition, activation, retention, referral, revenue—as a gap check, not a required taxonomy. Also inspect:

- Acquisition loop: source -> qualified arrival -> first value -> learning that improves acquisition.
- Referral/invite loop: valuable user -> share/invite -> qualified recipient -> value -> new sharer.
- Content loop: creation -> distribution/discovery -> consumption/value -> creation or sharing.
- Monetization lifecycle: intent -> checkout -> authoritative purchase -> renewal, failure, cancellation, refund, recovery.
- Resurrection: previously inactive user returns and completes a value event. Define the inactivity window explicitly.

Measure loops only when they exist in the product strategy. “Invite tapped” is not proof of a successful referral; “payment screen viewed” is not revenue.

## Maturity levels

Choose the lowest sufficient scope:

1. **Foundation:** environments, identity/privacy, lifecycle/screens, critical journey, activation, small high-value contract, segmentation, QA.
2. **Growth:** acquisition, funnels, retention, monetization, loops, reactivation, campaign analysis, client/server ownership.
3. **Experimentation:** only with a real decision, meaningful traffic, stable metrics, eligibility/exposure integrity, guardrails, rollout controls.
4. **Scale:** governance, migrations, warehouse/reconciliation, sampling/budgets, advanced attribution/groups, organization ownership.

Capability availability is not justification. Evidence, decision frequency, data volume, and operational cost determine maturity.

## Disciplined experimentation

Define hypothesis, eligibility, assignment unit, exposure moment, primary metric, secondary metrics, guardrails, expected direction, minimum runtime considerations, contamination risks, and rollout/rollback before launch. Record exposure only after eligibility and actual exposure. Avoid repeatedly evaluating flags in ways that inflate exposure. Use safe fallbacks, progressive rollout and kill switches where risk warrants them, and remove stale flags after decisions.

Do not experiment when the change is mandatory, traffic cannot support useful inference, instrumentation is unstable, or qualitative research is the faster decision tool.

## Avoid vanity metrics

Reject a proposed signal when nobody can name the decision it changes, its causal interpretation is implausible, it duplicates a reliable signal, or it rewards low-value activity. Prefer rates, cohorts, completed state transitions, and value-qualified outcomes over raw activity volume.
