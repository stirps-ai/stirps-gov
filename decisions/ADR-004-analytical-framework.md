# ADR-004: Analytical Framework Adoption

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The participant architecture (ADR-003) defines four cognitive modes and a
human authority. These roles need a diagnostic vocabulary — a way to reason
about their relationships, boundaries, and failure modes. An analytical
framework provides this vocabulary without generating prescriptive authority.

The framework chosen must be adopted as a lens for reasoning, not as a
design methodology. The failure mode is decisions justified by "the framework
requires" rather than by project-specific reasoning through the framework's
lens.

<!-- Replace the framework below with your project's choice — VSM, DDD,
     TOGAF, or any other lens. The ADR structure is transferable; the
     specific framework is not. -->

---

## Decision

The Viable System Model (VSM) is adopted as the analytical framework for
reasoning about participant relationships and system structure.

**Scope.** VSM provides vocabulary and diagnostics. It does not generate
prescriptive authority. ADRs are justified by project-specific reasoning,
not by VSM prescription.

**Canonical record.** The glossary's Theoretical Anchors section is the
single authoritative VSM mapping. No mapping table appears in this ADR
or any other artefact — the glossary is the single source of truth. This
eliminates split-record risk.

**Re-expression corollary.** When drift is observed between the VSM mapping
and the project's actual structure, the correct response is to update the
mapping to reflect reality — not to remediate the running system to match
the theoretical model. The map serves the territory, not the reverse.

---

## Options Considered

### No analytical framework

Reason about participant relationships using project-specific vocabulary only.
Viable for simple projects. Rejected for this project because the four-mode
architecture benefits from a diagnostic vocabulary that helps identify
structural gaps (e.g. "this concern sits at S2, which is unoccupied").

### VSM as analytical lens

Chosen for: rich vocabulary for multi-participant systems, explicit attention
to audit channels (S3*), and alignment with the project's self-governing
architecture.

---

## Consequences

- Participants can be located in a theoretical structure, making structural
  gaps visible.
- The Evaluate participant's placement at S3* (independent audit) rather than
  S3 (operational control) is an explicit governance decision with clear
  rationale.
- The glossary's Theoretical Anchors section becomes the canonical mapping —
  all other references point there.
- VSM vocabulary enters the governance record but carries no prescriptive
  weight — it is always filtered through project-specific reasoning.

---

## Failure Criteria

- Decisions are justified by "VSM requires" rather than by project-specific
  reasoning.
- The VSM mapping in the glossary diverges from the project's actual structure
  without anyone noticing.
- The framework's vocabulary becomes jargon that obscures reasoning rather
  than clarifying it.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `glossary.md` Theoretical Anchors section populated with the VSM mapping
- [ ] No VSM mapping table exists outside the glossary
