# ADR-003: Participant Architecture

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The project requires multiple modes of reasoning — generative, evaluative,
coordinative, and observational — that must be structurally separated to
function correctly. A single AI context handling all modes tends toward
self-confirmation (when generating and evaluating) and scope creep (when
coordinating and deciding).

Declaring participants incrementally as they are needed risks a supersession
chain — each new role requires amending the architecture ADR, producing
partial supersessions that fragment the participant record. Declaring all
participants simultaneously, with dormancy states for roles not yet active,
eliminates this risk at the cost of one glossary entry per dormant role.

---

## Decision

The project operates with four AI participant roles and one human role,
declared here in full. All participant terms are defined in `glossary.md`.

| Role | Cognitive Mode | Status at Bootstrap | Activation Trigger |
|---|---|---|---|
| Gardener | Human authority (S5) | Active | Always present |
| Generate | Generative (S4) | Active | Reasoning begins at ADR-000 |
| Evaluate | Adversarial audit (S3*) | Active | Evaluation gate defined in ADR-000 |
| Coordinate | Coordination (S2) | Dormant | First delivery lifecycle completion |
| Observe | Meta-observation | Dormant | Framework structurally complete; Gardener discretion |

**Note:** VSM positions (S5, S4, S3*, S2) in this table are a forward
reference to ADR-004, which adopts the analytical framework. Both ADRs
are co-dependent within the bootstrap batch.

**The Gardener** holds sole commit authority. All AI participants are advisory.
The Gardener approves, commits, merges, or rejects at every boundary.

**The Generate participant** reasons forward from committed decisions. Proposes
ADRs and specifications. Owns the architectural reasoning record. Its identity
is "the reasoning record that shapes future reconstructions" — not "the map."
The distinction prevents the generative layer from absorbing implementation
concerns.

**The Evaluate participant** evaluates adversarially against the committed
record. Never proposes, only judges. Must never share a reasoning context with
the Generate participant — the separation is enforced by separate environments
(separate projects, separate system prompts, separate conversations), not by
instruction.

**The Coordinate participant** translates committed architectural intent into
executable delivery contracts. Maintains no artefacts. A pure function:
repositories in, drafts out. The moment a coordination participant starts
maintaining its own artefacts, it acquires governance weight that defeats its
purpose. Begins dormant; activated when the delivery lifecycle needs
coordination.

**The Observe participant** surfaces patterns, fragilities, and transferable
insights across sessions. Excluded from governance decisions. Its channel is
observation files that accumulate slowly and accurately. Begins dormant;
activated at the Gardener's discretion when there is enough framework history
to observe.

**Dormancy.** A dormant participant is declared in this ADR and defined in
the glossary, but has no active environment (no Claude Project, no system
prompt in use). Activation is an operational event — the Gardener sets up
the environment — not a governance event requiring a new ADR.

**System prompts.** Each participant's system prompt must carry constitutional
reasoning: not just what the role does, but why it is structurally separate
and what breaks if roles collapse. System prompts are Gardener-maintained
craft artefacts, not governance artefacts — they iterate freely.

---

## Options Considered

### Incremental participant declaration

Declare participants as they are needed. Rejected: incremental declaration
tends to require partial supersessions as new roles emerge — each new
participant amends the architecture ADR. The cost of declaring a dormant
participant is one glossary entry and one row in this ADR. The cost of
retroactive declaration is a supersession chain.

### Full declaration with dormancy states

Chosen for: architectural completeness from day one, elimination of
supersession chains, and explicit activation triggers that make dormancy
a designed state rather than an omission.

---

## Consequences

- The participant architecture is complete at bootstrap. No structural ADR
  amendments are needed when dormant roles activate.
- Each role has a defined cognitive mode and a clear rejection criterion
  for reasoning that belongs elsewhere.
- The generator/evaluator separation is enforced by environment boundaries,
  not by instruction — this is a structural commitment, not a convention.
- If a dormant role's design changes significantly before activation, this
  ADR may need amendment. This is a small risk traded against the v1 cost
  of incremental declaration.

---

## Failure Criteria

- The Generate and Evaluate participants share a reasoning context (same
  project, same conversation, same system prompt).
- The Coordinate participant begins maintaining persistent artefacts.
- A new participant role emerges that cannot be mapped to one of the four
  cognitive modes — suggesting the mode model is incomplete.
- Role discomfort is ignored rather than treated as a signal of a missing
  or misconfigured participant.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `glossary.md` updated with all participant definitions
- [ ] All participant terms used in prior ADRs are consistent with this declaration
