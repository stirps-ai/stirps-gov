# ADR-008: Automated Compliance Gate

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The delivery lifecycle (ADR-007) defines three evaluation gates where the
Evaluate participant reviews artefacts adversarially. These gates currently
operate manually — the Gardener submits artefacts, the Evaluate participant
reviews, findings are resolved, and the Gardener commits.

As the project matures, some compliance checks become mechanical: does the
registry entry match the spec? Does the contract reference the correct spec
version? Are all required artefact sections present? These checks can be
automated without replacing the Evaluate participant's adversarial judgment.

---

## Decision

Automated compliance checking of implementation artefacts against governance
constraints is adopted as an intent.

**Position in the lifecycle.** The automated gate sits between contract
acceptance and execution in the delivery lifecycle (between Gate 2 and
Phase 4 of ADR-007). It verifies mechanical compliance before autonomous
execution begins.

**Scope.** The automated gate checks structural compliance: required fields
present, references valid, naming conventions followed, registry consistency
maintained. It does not replace the Evaluate participant's adversarial review
of architectural quality, reasoning coherence, or governance integrity.

**Implementation deferred.** This ADR records the architectural intent. The
gate is activated when the execution tooling is operational and the first
delivery lifecycle has been exercised manually. Premature automation of a
process that hasn't been practised manually produces brittle checks against
poorly understood requirements.

**No mapping table update.** The compliance gate's position in the
concern-to-tool mapping (ADR-005) is established when the gate is activated
and a specific tool is chosen.

---

## Options Considered

### Manual compliance only

Rely entirely on the Evaluate participant for all compliance checking.
Viable indefinitely for small projects. Rejected as a permanent state because
mechanical checks consume evaluation context that would be better spent on
architectural judgment.

### Automated compliance gate as described above

Chosen for: separation of mechanical checks from adversarial judgment,
reduced evaluation round-trips for structural defects, and clear activation
trigger (first manual lifecycle completion).

---

## Consequences

- Mechanical compliance defects are caught before they reach the Evaluate
  participant, allowing adversarial review to focus on architectural quality.
- The gate is inert until activated — no tooling dependency at bootstrap.
- Activation requires choosing a tool, which will produce a row in the
  concern-to-tool mapping and potentially an adoption ADR.
- The Evaluate participant's role is preserved: automated compliance is
  a filter, not a replacement.

---

## Failure Criteria

- The automated gate is activated before the manual lifecycle has been
  exercised at least once — producing checks against untested assumptions.
- Automated checks expand to cover architectural judgment, displacing the
  Evaluate participant's adversarial role.
- The gate becomes a bottleneck rather than an accelerant — indicating the
  checks are too broad or too brittle.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] The gate's position in the delivery lifecycle is stated relative to
      ADR-007's phases
- [ ] Activation trigger is explicit: first manual lifecycle completion
- [ ] No tooling commitment is made in this ADR
