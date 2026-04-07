# Concern-to-Tool Mapping

*Governed by ADR-005. Each row maps a project concern to the tool that serves
it, the ADR that governs the adoption, and the participant responsible.*

## Consistency Rules

- Every tool listed must be governed by an accepted ADR.
- Every participant listed must be declared in ADR-003.
- No speculative rows — the mapping reflects current reality at time of update.
- New rows are added as a consequence of the adopting ADR, citing ADR-005 as
  the governing authority for the mapping model.

---

## Mapping Table

| Concern | Tool | Governing ADR | Responsible Participant |
|---|---|---|---|
| Architectural decisions | ADR files in Git | ADR-000 | Generate |
| Version control hosting | *(your platform)* | ADR-002 | Gardener |
| Adversarial evaluation | *(your Evaluate environment)* | ADR-000, ADR-003 | Evaluate |

<!-- Add rows as you commit adoption ADRs for your project's tools.
     Examples from the reference implementation:

     | Configuration management | Ansible | ADR-018 | Coordinate |
     | Edge proxy | Traefik | ADR-022 | Generate |
     | Orchestration | SemaphoreUI | ADR-021 | Gardener |
     | Container runtime | Docker | ADR-017 | Coordinate |
-->
