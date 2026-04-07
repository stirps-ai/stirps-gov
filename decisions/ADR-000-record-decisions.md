# ADR-000: Record Architectural Decisions

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Accepted     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

This project requires a durable record of architectural decisions that persists
across contributors, tools, and time. AI participants are stateless — they
reconstruct context from committed artefacts, not from conversational memory.
Without a structured decision record, each session reasons from an incomplete
and potentially inconsistent understanding of prior choices.

Architecture Decision Records (ADRs) provide this record. Each ADR captures the
context, decision, alternatives, consequences, failure criteria, and definition
of done for a single architectural choice.

---

## Decision

All significant architectural decisions are recorded as Architecture Decision
Records in the `decisions/` directory of the governance repository.

**Template.** The canonical ADR template is `decisions/_template.md`. It is a
standalone file, not embedded in this ADR. The template may evolve through
Gardener commits without requiring this ADR to be superseded.

**Immutability.** An accepted ADR is never edited except to add a `Superseded by`
reference. When a decision changes, a new ADR supersedes the original. The
original remains in the repository as the historical record of why the prior
decision was made.

**Append-only model.** ADRs are sequentially numbered (ADR-000, ADR-001, ...).
Numbers are never reused. Gaps in numbering are permitted if a proposed ADR is
withdrawn before acceptance.

**Lifecycle.** An ADR moves through three states:

| State | Meaning |
|---|---|
| Proposed | Drafted, awaiting adversarial evaluation |
| Accepted | Evaluation passed, Gardener committed |
| Superseded | Replaced by a later ADR (referenced in header) |

**Evaluation gate.** Transition from Proposed to Accepted requires adversarial
evaluation by the Evaluate participant. All blocking findings must be resolved
before the Gardener commits. The evaluation record is stored at
`decisions/evals/eval-YYYYMMDD-HHMM-<subject>.md`.

**Grandfathering.** This ADR is accepted by declaration — it defines the gate
that all subsequent ADRs must pass through. It cannot itself be the first
artefact through a gate that does not yet exist.

---

## Options Considered

### Informal decision log

A running document or wiki page recording decisions in prose. Rejected:
informal logs lack the structured sections (failure criteria, definition of
done) that make decisions mechanically verifiable. They also tend toward
editing-in-place rather than append-only, destroying the historical record.

### ADRs as described above

Chosen for: immutability, structured evaluation, compatibility with Git
version control, and alignment with the principle that committed artefacts
carry authority while conversations do not.

---

## Consequences

- Every significant architectural choice produces a committed, immutable record.
- AI participants can reconstruct decision context from the ADR chain without
  access to prior conversations.
- The evaluation gate introduces a mandatory adversarial review step, which
  adds latency to decision acceptance but catches structural defects before
  they compound.
- The template is decoupled from this ADR — template evolution does not require
  superseding the foundational governance decision.

---

## Failure Criteria

- ADRs are routinely edited after acceptance rather than superseded.
- The evaluation gate is bypassed for convenience without recording the
  exception.
- Decision context is routinely reconstructed from conversations rather
  than from committed ADRs, indicating the records are not serving their
  purpose.

---

## Definition of Done

- [x] This ADR is committed to the governance repository (grandfathered)
- [x] `decisions/_template.md` exists as a standalone file
- [x] `decisions/evals/` directory exists for evaluation records
- [x] `glossary.md` defines "ADR", "Gardener", and "Evaluate" terms

**Note:** This repository ships `glossary-template.md`. References to
`glossary.md` in DoD items are satisfied after the forker copies the
template to `glossary.md` per BOOTSTRAP.md Step 2.
