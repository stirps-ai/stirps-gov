# ADR-010: Governance Dependency Sequencing

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

Every governance artefact rests on assumptions about concepts it does not
itself govern. A component spec assumes a network fabric exists. A delivery
contract assumes a lifecycle protocol exists. An adoption ADR assumes the
concern-to-tool mapping model exists.

When these assumptions are satisfied by committed artefacts, the dependency
is explicit and verifiable. When they are not — when an artefact silently
relies on an ungoverned concept — the dependency is invisible. Invisible
dependencies compound: each new artefact that touches the ungoverned concept
carries its own silent assumption, and the cost of eventually governing the
concept grows with every artefact that assumed it.

The infrastructure manifest (ADR-006) established the governance/implementation
boundary — the first context where silent assumptions about instance facts
became visible. The delivery lifecycle (ADR-007) created the first specs that
could assume ungoverned upstream concepts. Both demonstrated the need for an
explicit sequencing principle.

---

## Decision

One principle is introduced to `principles.md`:

### Govern the dependency first

Every governance artefact rests on assumptions about concepts it does not
itself govern. Each assumption must either:

1. **Be governed** by an existing committed artefact — an ADR, a principle,
   a glossary entry, or a spec that establishes the concept, or
2. **Be declared explicitly** as acknowledged provisional debt — named in the
   artefact with a reference to the ungoverned concept and a note that
   governance is pending.

Silent reliance on an ungoverned concept is a drafting error. The Evaluate
participant should flag undeclared dependencies as blocking findings.

**Cost inversion.** This principle creates a gravitational pull toward debt
resolution. Each new artefact that touches an ungoverned concept must carry
its own debt declaration, making deferral progressively more expensive.
Resolution is bounded — one ADR closes the gap. This cost inversion is
emergent, not designed, and is one of the framework's most powerful
properties.

---

## Options Considered

### Informal sequencing discipline

Trust the Gardener and Generate participant to sequence artefacts correctly
without a committed principle. Rejected: silent dependencies are invisible
by definition — they are the class of error that discipline alone cannot
catch. A committed principle gives the Evaluate participant an explicit
criterion to flag them.

### Committed sequencing principle

Chosen for: makes invisible dependencies a detectable defect class, creates
the cost-inversion dynamic that pulls toward debt resolution, and gives the
Evaluate participant a clear evaluation criterion.

---

## Consequences

- Every artefact must either satisfy its dependencies or declare them as
  provisional debt. There is no third option.
- The Evaluate participant gains a powerful evaluation criterion: "does this
  artefact silently assume a concept that no committed artefact governs?"
- Provisional debt declarations are visible in the governance record,
  making the project's governance gaps an explicit, auditable inventory.
- The cost-inversion dynamic means governance gaps become progressively
  more expensive to defer — each new artefact touching the gap adds a
  debt declaration.
- Retroactive ADRs (for pre-governance components) are the resolution
  mechanism: one ADR closes the gap and retires all associated debt
  declarations.

---

## Failure Criteria

- The principle is applied so rigidly that no artefact can be committed
  until every transitive dependency is governed — producing deadlock rather
  than sequenced progress.
- Provisional debt declarations become permanent fixtures rather than
  triggers for resolution.
- The Evaluate participant flags dependencies that are genuinely out of
  scope for the project, applying the principle beyond its useful boundary.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `principles.md` updated with the "Govern the dependency first"
      principle under the ADR-Introduced section, referencing this ADR
