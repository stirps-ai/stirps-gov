# Principles

*Standing constraints for this project. Introduced and amended by ADR.*

Principles are the ground truth that ADRs are evaluated against. They are not
aspirational — they are load-bearing commitments that constrain all governance
and implementation decisions.

---

## Foundational Principles

*These predate all ADRs and require no ADR anchor.*

### Map before territory

Governance precedes the thing it governs. The governance record for a decision
must exist before the decision takes effect. The interface must be defined
before the first message crosses it. The participant must be declared before
it appears in the mapping.

<!-- Your project's specific expression of this principle. What does "governance
     precedes execution" mean for your domain? -->

### The seed principle

Both repositories are necessary to the project. Only the implementation
repository, the bootstrap secret, and the infrastructure are necessary to
reconstruct the running system. They operate at different layers of time.

Reproducibility (the implementation repository's property) and evolvability
(the governance repository's property) are different concerns. Any artefact
that conflates "what you need to run this" with "what you need to improve this"
is mixing layers of time.

### The bootstrap layer is dependency-free

No governance artefact may depend on infrastructure that the governance
framework is used to build. The governance layer must be operable even when
the governed system does not yet exist.

### One-way reference

The governance repository describes intent and constraints. The implementation
repository satisfies them. The governance repository never references
implementation artefacts by path or name. This is what keeps the map stable
as the territory grows.

---

## The Four Cognitive Modes

*The minimum viable governance architecture.*

Every governance system requires these four modes of reasoning. They may be
distributed across any number of participants (human or AI), but collapsing
them into fewer than four distinct concerns degrades governance quality.

| Mode | Concern | Structural question |
|---|---|---|
| **Generate** | Architectural intent | *What must be true?* |
| **Evaluate** | Adversarial compliance | *Is this actually true?* |
| **Coordinate** | Intent-to-execution translation | *How do we make this true?* |
| **Observe** | Pattern recognition | *What are we learning?* |

The generator/evaluator separation is load-bearing. A generator asked to
critique its own output tends toward self-confirmation. The separation must
be enforced by context boundaries (separate projects, separate prompts),
not by instruction.

---

## The Gardener

The Gardener is the human authority. The Gardener holds sole commit authority
across the entire project lifecycle. All AI participants are advisory — they
propose, evaluate, coordinate, and observe, but the Gardener decides and
commits.

The Gardener role cannot be delegated to an AI participant. The framework's
integrity depends on a human exercising judgment at every commit boundary.

---

## Append-Only Commitment

Accepted governance artefacts are never edited except to add supersession
references. When a decision changes, the original is superseded by a new
artefact. The original remains as the historical record of why the prior
decision was made.

This commitment is what makes the governance record trustworthy across time.
AI participants reconstructing context from committed artefacts must be able
to trust that accepted records reflect the state of reasoning at the time of
acceptance.

---

## ADR-Introduced Principles

*Added below by their governing ADRs as the framework matures.*

<!-- As you commit ADRs that introduce new principles, add them here with
     their ADR reference. Examples from the reference implementation:

     ### Resist structural accumulation (ADR-NNN)
     Every new structural element must justify its existence against the
     framework's complexity budget.

     ### Cold for mass; hot for essence (ADR-NNN)
     Hot artefacts hold only what the next action requires. Cold storage
     absorbs the full record.

     ### Govern the dependency first (ADR-NNN)
     Every governance artefact rests on assumptions about concepts it does
     not itself govern. Each assumption must be governed or declared as
     provisional debt. -->
