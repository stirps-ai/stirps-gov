# ADR-007: Implementation Delivery Lifecycle

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The governance repository produces specifications. The implementation
repository produces running systems. The interface between them — how
architectural intent becomes executable work — must be committed as a
governance artefact before the first delivery crosses it.

Without a committed lifecycle protocol, the first delivery invents its own
protocol ad hoc. That protocol becomes implicit convention — never evaluated,
difficult to supersede because it was never committed.

---

## Decision

The delivery lifecycle follows five phases, evaluated at three gates:

```
Scope → Spec → Contract → Execute → Accept
```

**Phase 1 — Scope.** The Gardener identifies a delivery need and selects a
component.

**Phase 2 — Spec.** The Generate participant produces a Gov spec: enduring
requirements for the component. The spec describes what the component must
guarantee, not how to configure it. Evaluated by the Evaluate participant
(Gate 1).

**Phase 3 — Contract.** The Coordinate participant (or the Gardener, if
coordination is dormant) translates the Gov spec into a delivery-scoped
commitment: a specification scoped to this delivery, a task plan, and an
execution prompt. Evaluated by the Evaluate participant (Gate 2).

**Phase 4 — Execute.** Autonomous execution runs on a branch. The execution
agent commits freely on the branch. The governance boundary is the branch —
the agent has full velocity within it.

**Phase 5 — Accept.** The Evaluate participant reviews the branch output
against the Gov spec and contract (Gate 3). The Gardener merges or rejects.

**Specs outlive deliveries.** A Gov spec may produce multiple deliveries as
requirements evolve or new sites come online. The spec is the enduring anchor;
the contract is the scoped commitment to satisfy it at a point in time.

**The adoption-ADR-plus-spec pattern.** When a new tool is adopted, two
artefacts are required: an ADR (why this tool — a reasoning act) and a spec
(what it must guarantee — a specification act). Collapsing them into a single
artefact embeds alternatives-reasoning into an operational contract, which is
a category error.

**Three-layer separation within artefacts.** Separate what was decided (ADRs —
immutable, slow) from how it's practised (conventions — revisable, medium)
from what craft knowledge accumulates (guidelines — freely evolving, fast).
Coupling fast-changing conventions to slow-changing governance decisions is the
most common source of unnecessary supersession chains.

---

## Options Considered

### Ad hoc delivery protocol per component

Let each delivery define its own handoff. Rejected: produces inconsistent
interfaces that are never evaluated and cannot be audited.

### Committed five-phase lifecycle with three evaluation gates

Chosen for: consistent interface, mandatory adversarial review at each
boundary, and clear separation between enduring specs and scoped contracts.

---

## Consequences

- Every delivery follows the same protocol, making the process auditable.
- The branch is the governance boundary for autonomous agents — execution
  velocity and governance integrity coexist without conflict.
- The Evaluate participant reviews at three distinct gates, each with a
  different concern: spec quality, contract quality, implementation quality.
- The Coordinate participant has a defined role in Phase 3, even if dormant
  at bootstrap.
- Conventions and guidelines iterate without ADR supersession.

---

## Failure Criteria

- Deliveries bypass the evaluation gates "just this once."
- The Gov spec and implementation contract are collapsed into a single
  artefact, losing the distinction between enduring requirements and
  scoped commitments.
- The branch boundary is not respected — autonomous agents commit to main
  directly.
- Conventions are embedded in this ADR rather than maintained as separate
  craft artefacts.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] Evaluation record convention stated: `decisions/evals/eval-YYYYMMDD-HHMM-<subject>.md`
- [ ] The three evaluation gates are named and their concerns distinguished
- [ ] This ADR does not embed convention or guideline content that should
      iterate independently
