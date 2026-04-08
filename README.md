# Stirps — Governance Framework

A recursively self-modifying, memory-preserving, adversarially-evaluated institution for governing AI-participant infrastructure that produces functioning systems.

A forkable governance framework for long-lived, self-governing technical projects.

Stirps provides a complete governance architecture built on four premises:

- **The system remembers, not the AI.** Coherence across time comes from committed, versioned artefacts — not conversational memory.
- **Governance precedes the thing it governs.** The governance record for a decision must exist before the decision takes effect.
- **Roles are constitutions, not instances.** Participant roles are defined by their structural concern, not by who or what occupies them. Humans and AI models are interchangeable occupants.
- **Exploration is disposable; commitment is irreversible.** ADRs are append-only and immutable. When a decision changes, the original is superseded, not edited.

## Who This Is For

You are building a project that needs durable architectural governance — infrastructure, a platform, a system that will outlive any individual contributor or tool. You want AI participants to reason about architecture without becoming a single point of failure. You want decisions to compound forward rather than decay.

Fork this repository and follow [BOOTSTRAP.md](BOOTSTRAP.md) to initialise governance for your project.

## Repository Structure

*After completing [BOOTSTRAP.md](BOOTSTRAP.md). The template repo ships
`principles-template.md` and `glossary-template.md` — you copy and populate
them during bootstrap.*

```
├── README.md                  # This file
├── BOOTSTRAP.md               # Step-by-step initialisation guide
├── gov-bootstrap-lessons.md   # Reasoning behind the bootstrap sequence
├── principles.md              # Standing constraints (copied from principles-template.md)
├── glossary.md                # Canonical terms (copied from glossary-template.md)
├── architecture.json          # Component registry (created at Step 10)
├── architecture-schema.json   # JSON Schema for the registry
├── mappings/
│   └── concern-to-tool.md     # Which tool serves which concern
├── decisions/
│   ├── _template.md           # ADR template
│   ├── evals/                 # Evaluation records
│   └── ADR-NNN-*.md           # Architectural Decision Records
└── specs/                     # Component specifications (created when needed)
```

## The Four Cognitive Modes

The framework operates through four structural concerns. Every governance architecture needs all four; simpler projects may combine them into fewer named participants.

| Mode | Concern | Question |
|---|---|---|
| **Generate** | Architectural intent | *What must be true?* |
| **Evaluate** | Adversarial compliance | *Is this actually true?* |
| **Coordinate** | Intent-to-execution translation | *How do we make this true?* |
| **Observe** | Pattern recognition and transferable insight | *What are we learning?* |

The **Gardener** is the human authority — sole commit power, final judgment, the role that cannot be delegated to AI.

## Reference Implementation

The framework was developed and proven across a homelab infrastructure project:

- **Governance repo (map):** [stirps-ai/homelab-seed-gov](https://github.com/stirps-ai/homelab-seed-gov)
- **Implementation repo (territory):** [stirps-ai/homelab-seed](https://github.com/stirps-ai/homelab-seed)

These repositories demonstrate the framework in use with real infrastructure decisions, evaluation cycles, and delivery lifecycles.

## More Information

- [stirps.ai](https://stirps.ai) — project home
- [gov-bootstrap-lessons.md](gov-bootstrap-lessons.md) — the reasoning behind every sequencing decision in the bootstrap
- [BOOTSTRAP.md](BOOTSTRAP.md) — start here when you fork

## Licence

MIT
