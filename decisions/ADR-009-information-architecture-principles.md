# ADR-009: Information Architecture Principles

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

As the framework matures, two failure modes become visible:

**Structural accumulation.** Each new folder, artefact type, governance layer,
or participant adds structural weight. Content accumulation in established
artefacts is healthy — the glossary gains terms, the registry gains components.
But structural accumulation — new categories of things — is the failure mode
that makes governance feel heavy. Embedding a growing lookup table in an
ADR body — the anti-pattern ADR-005 is designed to prevent — produces
unnecessary supersession chains because the structure can't accommodate
growth.

**Information temperature mismatch.** The infrastructure manifest (ADR-006)
demonstrated a second pattern: some facts change at operational speed (IP
addresses, OS versions) while others change at governance speed (architectural
roles, constraints). Mixing them in a single artefact couples their rates of
change. The general form: artefacts that hold both "what you need right now"
and "the full historical record" serve neither function well.

These patterns are general enough to warrant standing principles.

---

## Decision

Two principles are introduced to `principles.md`:

### Resist structural accumulation

Every new structural element (folder, artefact type, governance layer,
participant) must justify its existence against the framework's complexity
budget. The question is not "would this be useful?" but "does the value of
this new structure exceed the cost of every future participant having to
understand it?"

Content accumulation in cold storage is healthy. Structural accumulation is
the failure mode.

### Cold for mass; hot for essence

Hot artefacts hold only what the next action requires. Cold storage absorbs
the full record. A cache draws from cold into hot for a session and releases
on exit.

Applied to the framework: Git history is cold (the full record). The current
state of any artefact is hot (what the next session needs). Session wrap-ups
and evaluation records are warm (referenced when relevant, not loaded by
default). An artefact trying to serve both hot and cold functions will grow
unwieldy — the resolution is asking which functions have better homes
elsewhere.

---

## Options Considered

### Leave these as informal heuristics

Note the patterns in session records without committing them as principles.
Rejected: both patterns recur frequently enough (three or more instances each
in the reference implementation) to warrant standing constraints. Informal
heuristics decay across sessions; committed principles persist.

### Commit as standing principles via this ADR

Chosen for: these are genuine constraints that ADRs and specs should be
evaluated against, not just observations.

---

## Consequences

- Future proposals for new artefact types, directories, or governance layers
  must justify themselves against the structural accumulation principle.
- Artefacts that mix fast-changing and slow-changing information are
  identifiable as design smells.
- The Evaluate participant gains two additional principles to evaluate against.
- These principles apply retroactively as diagnostic lenses — existing
  artefacts that violate them are candidates for restructuring, not
  immediate defects.

---

## Failure Criteria

- The principles are cited to block useful structural additions, becoming
  a barrier rather than a filter.
- "Resist structural accumulation" is interpreted as "never add structure"
  rather than "justify every addition."
- The cold/hot distinction is applied so rigidly that useful context is
  excluded from hot artefacts, forcing participants to search cold storage
  for routine information.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `principles.md` updated with both principles under the ADR-Introduced
      section, referencing this ADR
