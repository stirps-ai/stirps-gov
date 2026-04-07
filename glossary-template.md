# Glossary

*Canonical terms for this project. Every term that carries governance authority
must be defined here before it appears in an ADR, spec, or evaluation.*

Undefined terms in governance records are a persistent source of blocking
evaluation findings. Define terms at bootstrap — even for roles that are
dormant — to avoid retroactive definition chains.

---

## Roles and Participants

### Gardener

The human authority. Holds sole commit power across the entire project
lifecycle. All AI participants are advisory; the Gardener decides and commits.
The Gardener role cannot be delegated to an AI participant.

### Generate

The generative cognitive mode. Produces architectural intent: ADRs, specs,
and the governance reasoning record. Asks: *what must be true?*

<!-- In the reference implementation, this role is named "Gov" and occupies
     VSM position S4. Name your project's generative participant here. -->

### Evaluate

The adversarial evaluation mode. Verifies proposals against the committed
governance record. Asks: *is this actually true?* The evaluator arrives cold
to every proposal — the value of this role depends on independence from the
generative context.

<!-- In the reference implementation, this role is named "Eva" and occupies
     VSM position S3*. Name your project's evaluator here. -->

### Coordinate

The coordination mode. Translates committed architectural intent into
executable delivery contracts. A pure function: repositories in, drafts out.
No persistent state, no maintained artefacts. Asks: *how do we make this true?*

<!-- In the reference implementation, this role is named "Nav" and occupies
     VSM position S2. This role may begin dormant — declare it now, activate
     it when the first delivery lifecycle needs coordination. -->

### Observe

The meta-observation mode. Surfaces patterns, fragilities, and transferable
insights across sessions. Does not participate in governance decisions. Asks:
*what are we learning about how we make things true?*

<!-- In the reference implementation, this role is named "Adi" and sits outside
     the VSM stack. This role may begin dormant — declare it now, activate it
     when the framework is structurally complete. -->

---

## Architecture Terms

### Map

The governance repository. Contains ADRs, principles, specs, glossary, and
the component registry. Describes what must be true.

### Territory

The implementation repository. Contains playbooks, configurations, contracts,
and operational artefacts. Satisfies what the map requires.

### Seed

The minimal set of artefacts and infrastructure required to reconstruct the
running system: the implementation repository, the bootstrap secret, and the
hardware. The governance repository is necessary for the *project* but not for
*reconstruction*.

---

## Governance Terms

### ADR (Architecture Decision Record)

An immutable record of a single architectural decision. Once accepted, never
edited except to add a supersession reference. See `decisions/_template.md`.

### Governance Status

The status of a component in the architecture registry:

| Status | Meaning |
|---|---|
| `governed` | Has a governing ADR and (if applicable) a Gov spec |
| `pre_governance` | Predates the governance framework; operates without a governing record |
| `pending` | Governance artefacts are in progress |

### Evaluation Record

The written output of the Evaluate participant's adversarial review.
Stored at `decisions/evals/eval-YYYYMMDD-HHMM-<subject>.md`.

### Blocking Finding

An evaluation finding that must be resolved before the Gardener can accept
the artefact. Contrast with advisory findings, which are noted but do not
prevent acceptance.

---

## Theoretical Anchors

<!-- If your project uses an analytical framework (VSM, DDD, etc.), define
     the mapping here. This is the single canonical record — no other artefact
     duplicates this mapping.

     Example from the reference implementation:

     ### Viable System Model (VSM)
     | VSM Position | Project Role |
     |---|---|
     | S5 (policy) | Gardener |
     | S4 (intelligence) | Generate participant |
     | S3* (audit) | Evaluate participant |
     | S2 (coordination) | Coordinate participant |
     | Meta-observer | Observe participant |
-->

---

## Domain Terms

<!-- Add project-specific terms as your domain ADRs introduce them.
     Examples: site names, component categories, deployment concepts. -->
