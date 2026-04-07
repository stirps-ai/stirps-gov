# ADR-006: Infrastructure Manifest

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The project manages physical or virtual infrastructure with concrete instance
facts: node names, IP addresses, hardware specifications, OS versions, domain
assignments. These facts change at operational speed and belong in a different
artefact from architectural decisions, which change at governance speed.

Governance artefacts describe structural identity — what a node must be, what
a service must guarantee. The manifest records what currently satisfies those
roles. Mixing them creates a maintenance burden that scales with infrastructure
growth.

---

## Decision

The infrastructure manifest is the authoritative record of instance facts.

**Location.** The manifest lives in the implementation repository. Governance
artefacts reference roles and constraints; the manifest names the instances
that satisfy them.

**Content.** The manifest records: node identifiers, network addresses,
hardware specifications, OS versions, site assignments, and any other
instance-specific facts that governance artefacts must not contain.

**Boundary.** Governance documents describe what a node role requires.
The manifest records which specific nodes currently fill those roles. This
is the operational expression of the one-way reference principle: governance
describes the structural identity; the manifest describes the concrete
instances.

---

## Options Considered

### Instance facts in governance documents

Include IPs, hardware specs, and node names in Gov specs or ADRs. Rejected:
every hardware change or IP reassignment would require governance artefact
updates, coupling governance cadence to operational cadence.

### Separate manifest in the implementation repository

Chosen for: clean separation of concerns between structural identity
(governance) and concrete instances (manifest), with different rates of
change respected.

---

## Consequences

- Governance artefacts remain stable as infrastructure scales or changes.
- The manifest is the single place to look up "what is currently deployed."
- AI participants reasoning about architecture load governance artefacts
  without operational noise; those reasoning about deployment load the
  manifest.
- The Coordinate participant uses both — the spec (from governance) and the
  manifest (from implementation) — to draft delivery contracts.

---

## Failure Criteria

- Governance artefacts accumulate IP addresses, node names, or OS versions.
- The manifest falls out of sync with deployed reality and no process
  corrects the drift.
- Multiple artefacts claim to be the authoritative source of instance facts.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] Manifest location in the implementation repository is stated
- [ ] No instance facts appear in any governance artefact
