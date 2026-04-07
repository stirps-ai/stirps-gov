# ADR-001: Two-Repository Structure

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The project produces two fundamentally different kinds of artefacts:
governance artefacts (decisions, principles, specifications) and
implementation artefacts (configurations, playbooks, contracts). These have
different lifecycles, different rates of change, and different audiences.

Mixing them in a single repository creates coupling between the reasoning
record and the operational record. Changes to implementation details
appear in the same commit history as architectural decisions, making it
difficult for AI participants to reconstruct governance context without
parsing operational noise.

---

## Decision

The project maintains two repositories:

**Governance repository (the map).** Contains ADRs, principles, glossary,
component specifications, the architecture registry, and evaluation records.
Describes what must be true. Changes slowly. The Gardener is the sole
committer.

**Implementation repository (the territory).** Contains playbooks,
configurations, delivery contracts, operational manifests, and all artefacts
required to build and run the system. Satisfies what the governance
repository requires. Changes frequently.

**Reference direction.** Implementation artefacts reference governance
artefacts (e.g. a delivery contract references a Gov spec). Governance
artefacts never reference implementation artefacts by path or name. The
governance repository describes roles and constraints; the implementation
repository names the instances that satisfy them.

This separation is structural, not organisational. The two repositories
serve different functions at different layers of time.

---

## Options Considered

### Single repository with directory separation

Governance and implementation in one repo, separated by directories. Rejected:
Git history, branch policies, and access patterns differ between the two
concerns. A single repo forces shared branching strategy and makes it
impossible to grant AI execution agents write access to implementation
without exposing governance artefacts.

### Two repositories as described above

Chosen for: clean separation of concerns, independent lifecycles, and the
structural enforcement of one-way reference direction.

---

## Consequences

- AI participants reasoning about governance load only the governance
  repository — no implementation noise in context.
- The implementation repository can grant write access to autonomous
  execution agents (on branches) without risking governance artefacts.
- The one-way reference direction is now a verifiable invariant: any
  governance artefact that references an implementation path is a defect.
- Both repositories are necessary to the project. Only the implementation
  repository, the bootstrap secret, and the infrastructure are necessary
  to reconstruct the running system.

---

## Failure Criteria

- Governance artefacts accumulate implementation-specific paths, IPs, or
  version numbers.
- Implementation artefacts are committed to the governance repository
  "for convenience."
- The governance repository's commit frequency approaches the implementation
  repository's, suggesting operational content is leaking into governance.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `glossary.md` updated with "Map" and "Territory" definitions
- [ ] `principles.md` "One-way reference" principle confirmed present
