# ADR-011: Seed Principle Amendment

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The founding `principles.md` includes the seed principle: both repositories
are necessary to the project; only the implementation repository, the
bootstrap secret, and the infrastructure are necessary to reconstruct the
running system.

This formulation is correct. However, the reasoning behind it — why
reproducibility and evolvability are different properties, and why confusing
them produces governance artefacts that over-specify operational dependencies
— is not recorded in any committed artefact. A forker reading the principle
cold has the conclusion but not the argument.

Without this separation, governance artefacts tend to carry both "what you
need to rebuild" and "what you need to improve" in the same documents —
producing artefacts that are too operational for governance and too
governance-heavy for operations.

---

## Decision

This ADR records the rationale for the seed principle's formulation. It does
not amend `principles.md` — the founding version already carries the correct
text.

**Reproducibility** is the implementation repository's property. Given the
implementation repository, the bootstrap secret, and the infrastructure, the
running system can be reconstructed. This is a reconstruction-level concern.

**Evolvability** is the governance repository's property. Given the governance
record, the next rebuild can be better than the last. Past mistakes prevent
future ones. Architectural decisions compound forward. This is a project-level
concern.

**Both are necessary; they operate at different layers of time.** Any project
that conflates "what do you need to run this" with "what do you need to
improve this" will produce:

- Governance artefacts that over-specify operational dependencies (because
  they're trying to be sufficient for reconstruction)
- Implementation artefacts that carry architectural reasoning (because
  they're trying to be sufficient for evolution)

The seed principle prevents this conflation by assigning each property to
its correct repository.

**For forkers.** If your project's founding `principles.md` uses the seed
principle text from this framework's template, this ADR provides the
reasoning. If you need to amend the seed principle for your domain, this ADR
is the supersession target — amend the principle via a new ADR that
supersedes this one.

---

## Options Considered

### Omit this ADR if the principle is already correct

The founding `principles.md` is correct; no amendment is needed. Argument
for omission: an ADR with no delta is unusual. Rejected: the ADR's value
is the reasoning record, not the delta. A forker encountering the seed
principle needs the argument, not just the conclusion. An ADR chain that
only records changes omits the rationale for the founding state.

### Rationale-only ADR with no amendment to principles.md

Chosen for: provides the reasoning record without an unnecessary edit to a
document that already says the right thing.

---

## Consequences

- The seed principle's rationale is committed and discoverable.
- Future amendments to the seed principle supersede this ADR, preserving
  the reasoning chain.
- Forkers have an explicit argument for why the two-repository separation
  is load-bearing, not just organisational.

---

## Failure Criteria

- The distinction between reproducibility and evolvability is treated as
  academic rather than operational — artefacts continue to mix
  reconstruction-level and project-level concerns despite the principle.
- This ADR is cited to prevent the governance repository from containing
  any operational context, when the actual principle is about not
  *over-specifying* operational dependencies.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `principles.md` confirmed to contain the correct seed principle
      formulation (no edit required if founding text is correct)
