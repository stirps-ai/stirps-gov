# ADR-005: Concern-to-Tool Mapping

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

The project uses multiple tools, each serving a specific concern. Without a
canonical record of which tool serves which function, concerns accumulate
implicit tool assignments that are never evaluated and difficult to audit.

Embedding a mapping table inside an ADR body forces a full supersession for
every new row — a pattern that produces unnecessary supersession chains for
what is essentially a growing lookup table.

---

## Decision

Each concern in the project maps to a single designated tool. The mapping is
maintained as a governed reference file.

**Mapping model.** Each row records: concern → tool → governing ADR →
responsible participant.

**Reference file.** The mapping table lives in `mappings/concern-to-tool.md`,
not inline in this ADR. This ADR governs the mapping *model* — what the table
means, how it's structured, what consistency rules it must satisfy. Subsequent
ADRs that adopt new tools or introduce new concerns add rows to the reference
file and cite this ADR as the governing authority.

**Consistency rules:**

- Every tool in the mapping must be governed by an accepted ADR.
- Every participant in the mapping must be declared in ADR-003.
- No speculative rows. The mapping reflects current reality at the time of
  each update.
- One concern, one tool. If two tools serve the same concern, one must be
  designated primary and the other noted as an exception with rationale.

**Extensibility.** Adding a new tool to the mapping requires: (1) an adoption
ADR for the tool, (2) a row added to the reference file citing both the
adoption ADR and this ADR. No supersession of this ADR is needed.

---

## Options Considered

### Mapping table inline in this ADR

Rejected: every new row requires a superseding ADR, which
is heavyweight for what is essentially a lookup table update.

### Mapping model in ADR, table in reference file

Chosen for: the model (which changes rarely) is governed by an immutable ADR;
the table (which grows) is a Gardener-maintained file governed by that ADR.

---

## Consequences

- New tool adoptions extend the mapping without superseding this ADR.
- The reference file is auditable: every row must trace to an accepted ADR.
- The mapping provides a single place to answer "what tool do we use for X?"
- The consistency rules make the mapping mechanically verifiable.

---

## Failure Criteria

- Tools are adopted and used without a corresponding row in the mapping.
- The reference file grows rows that have no governing ADR.
- This ADR requires supersession to accommodate a new tool — indicating the
  extensibility mechanism has failed.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] `mappings/concern-to-tool.md` created with initial rows for all
      currently governed tools
- [ ] Consistency rules are mechanically verifiable against the reference file
