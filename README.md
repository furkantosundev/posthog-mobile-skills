# PostHog Mobile Skills

Portable Agent Skills for designing, implementing, and auditing trustworthy PostHog analytics in mobile applications.

The suite follows one governing principle: build the smallest trustworthy measurement system that can answer the product's next important growth decisions. It supports React Native, Expo, native iOS, native Android, and Flutter while requiring the active agent to discover the actual stack and verify version-sensitive guidance against current official PostHog documentation.

## Skills

| Skill | Purpose | Mutability |
|---|---|---|
| `posthog-mobile` | Orchestrate setup, improvement, remediation, and implementation | May write after material approval gates |
| `posthog-mobile-init` | Initialize a minimum viable growth measurement system | May write after product, identity, privacy, and schema decisions are agreed |
| `posthog-mobile-audit` | Audit growth coverage and technical trustworthiness | Strictly read-only |

No review skill is included.

## Install

Install all skills with the open Skills CLI:

```bash
npx skills add furkantosundev/posthog-mobile-skills
```

Install one skill:

```bash
npx skills add furkantosundev/posthog-mobile-skills --skill posthog-mobile
npx skills add furkantosundev/posthog-mobile-skills --skill posthog-mobile-init
npx skills add furkantosundev/posthog-mobile-skills --skill posthog-mobile-audit
```

You can also copy or symlink each directory under `skills/` into any Agent Skills-compatible client's discovery directory. The canonical instructions do not depend on a particular client, invocation syntax, connector, CLI, framework, or installation location.

## Design

All workflows reason from decisions to instrumentation:

```text
Business question
→ product decision
→ metric
→ observable behavior
→ event/property
→ analysis
→ validation
```

Instrumentation expands progressively through Foundation, Growth, Experimentation, and Scale maturity only when evidence and product needs justify it.

## Validation

Each skill follows the [Agent Skills specification](https://agentskills.io/specification). Pull requests run the reference validator against every skill package.

## License

[MIT](LICENSE)
