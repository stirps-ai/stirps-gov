# ADR-002: Repository Hosting Platform

| Field             | Value        |
|-------------------|--------------|
| **Status**        | Proposed     |
| **Date**          | YYYY-MM-DD   |
| **Author**        | [Gardener]   |
| **Supersedes**    | —            |
| **Superseded by** | —            |

---

## Context

Both repositories require a hosting platform that supports Git version control,
is accessible to all participants (human and AI), and provides integration
points for evaluation and delivery workflows. The governance repository is the
project's institutional memory — its hosting must be reliable, widely
accessible, and not dependent on infrastructure the project itself manages.

---

## Decision

Both repositories are hosted on a chosen Git platform.

<!-- Replace with your platform: GitHub, GitLab, Gitea, etc. -->

**Accessibility.** The platform must be accessible from all environments where
participants operate — browser-based interfaces, API access for AI tooling,
and command-line Git.

**External dependency.** The hosting platform is an external point of failure
acknowledged by this ADR. The governance framework depends on a service the
project does not control. This is acceptable at bootstrap; self-hosted Git
may become a deliberate infrastructure goal as the project matures.

**Migration trigger.** If the platform becomes inaccessible, unreliable, or
introduces constraints that conflict with the governance model, migration to
an alternative platform is triggered. The ADR chain, principles, and all
governance artefacts are plain files in Git — platform migration is a
hosting change, not a governance change.

---

## Options Considered

### Self-hosted Git from the start

Host repositories on project-managed infrastructure. Rejected at bootstrap:
this creates a circular dependency — the governance framework would depend on
infrastructure that the governance framework is used to build. Violates the
"bootstrap layer is dependency-free" principle.

### External hosted platform

Chosen for: availability before any infrastructure exists, accessibility from
all environments, and zero operational burden at bootstrap.

---

## Consequences

- The governance layer is operational before any project infrastructure exists.
- All artefacts are plain Git — no platform lock-in beyond hosting convenience.
- AI participants with platform integrations can read repositories directly.
- The external hosting dependency is declared, not hidden.

---

## Failure Criteria

- The platform introduces access restrictions that prevent AI participants
  from reading the governance repository.
- Platform-specific features (issues, wikis, CI) become load-bearing
  governance artefacts that cannot be migrated with Git alone.
- Self-hosted Git becomes available but migration is deferred indefinitely,
  leaving the external dependency unresolved.

---

## Definition of Done

- [ ] Evaluation pass with no unresolved blocking findings
- [ ] Gardener commit to the governance repository
- [ ] Both repositories created on the chosen platform
- [ ] README updated with repository URLs
