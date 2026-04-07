# Governance Bootstrap Lessons — v2

*A retrospective on bootstrapping a governance framework from scratch, refined across twenty-six sessions of practice. Written for a future Gardener initialising a new project that follows the map/territory/AI-reasoning model.*

---

> **A note on naming.** This document uses the reference implementation's
> participant names — Gov, Eva, Nav, Adi — rather than the generalised
> cognitive mode names (Generate, Evaluate, Coordinate, Observe) used
> throughout the rest of this repository. This is a deliberate choice.
> The lessons here were learned through specific practice with specific
> participants, and generalising the names would strip the specificity
> that makes the lessons authentic. Where you read "Gov," think "your
> generative participant." Where you read "Eva," think "your evaluator."
> The patterns transfer; the names are the reference implementation's.

---

## What This Document Is

This is a meta-document. It records what was learned — and what was learned about what was learned — during the creation, exercise, and maturation of a governance framework for self-governing infrastructure. It is not a governance artefact; it carries no authority. It is the distilled experience of one project, offered so that the next project starts cleaner.

The document has three audiences: a Gardener bootstrapping a new deployment of this framework, a team evaluating the framework for adoption, and a future version of the project's own participants encountering it for the first time.

---

## The Foundational Commitments

Before the bootstrap sequence, understand what the framework assumes. These are not configurable options — they are the load-bearing premises. If any feels wrong for your project, this may not be the right framework.

**The system remembers, not the AI.** AI participants are stateless across sessions. Coherence across time comes from committed, versioned artefacts — not conversational memory, not prompt accumulation, not fine-tuning. Authority derives from what is committed, not what was discussed.

**Governance precedes the thing it governs.** The governance record for a decision must exist before the decision takes effect. The interface must be defined before the first message crosses it. The participant must be declared before it appears in the mapping. This sequencing principle is the single most consequential design commitment in the framework, and the one most tempting to defer.

**Roles are constitutions, not instances.** A participant role (Gov, Eva, Nav, Adi) is defined by its constitutional concern and cognitive mode, not by who or what occupies it. A human, a Claude Project, a different model, or a future tool can fill any role. The governance record remains durable across occupant changes because the record describes the role, not the occupant.

**Exploration is disposable; commitment is irreversible.** The framework maintains a strict boundary between pre-commitment reasoning (conversations, drafts, exploration notes) and governance artefacts (committed ADRs, specs, evaluations). ADRs are append-only and immutable. When a decision changes, the original record is superseded, not edited.

---

## The Bootstrap Sequence

The correct order for initialising a governance project of this type:

### Phase 1 — Foundations (before any ADR)

Prepare the ground truth that everything else is evaluated against.

1. **Settle canonical names** for all repositories, roles, and named components. Commit these to the README before writing ADR-000. Naming inconsistencies in the founding artefacts generate persistent noise in every future reasoning session and every future evaluation — they are disproportionately expensive to fix later.

2. **Draft `principles.md`** with at least the core invariants. Principles are what ADRs are evaluated against. Without them, early evaluations have no stable anchor and produce noisy findings.

3. **Draft `glossary.md`** defining all role terms (Gardener, Gov, Eva, Nav, Adi, Imp — or your project's equivalents). Role terms carry governance authority; undefined terms in governance records are a persistent source of blocking findings.

4. **Declare all participants at bootstrap — including dormant ones.** If you know you will eventually need a coordination role (Nav) or an observation role (Adi), name them now as dormant. The cost is one line in the glossary. The alternative is a partial supersession chain later when the role emerges from practice and must be retroactively declared, anchored, and mapped — a pattern this project repeated twice.

### Phase 2 — The ADR Chain

5. **Commit ADR-000** — the decision to use ADRs. Rationale only; the template lives in its own file (`decisions/_template.md`). The template should include Failure Criteria and Definition of Done sections from the start — retrofitting them later requires grandfathering decisions.

6. **Commit structural ADRs** (repo structure, hosting, tooling map, AI participant architecture) in dependency order. Co-dependent ADRs should be committed as a batch. Forward references between co-dependent ADRs are unavoidable during bootstrapping; batch acceptance resolves them.

7. **Commit the lifecycle ADR** (ADR-005 equivalent) before accepting any ADR through the evaluator. This ADR should itself be the first to pass through the gate it defines. The evaluation record convention (where Eva's evaluations are stored) must be stated explicitly in this ADR — leaving it unspecified makes the Definition of Done mechanically unverifiable.

### Phase 3 — The Evaluator

8. **Initialise Eva** only after ADR-000, `principles.md`, and the glossary are committed. Eva needs stable ground truth before evaluation is useful. Eva's value increases with richer ground truth — the more committed artefacts she can reason against, the more precise her findings.

9. **Run the lifecycle ADR through Eva first.** Then submit the structural ADR batch. The two-round evaluation cycle (first pass → targeted fixes → second pass) is the standard pattern for revision-heavy batches.

### Phase 4 — Derived Artefacts

10. **Commit `architecture.json`** (or equivalent registry) after structural ADRs are accepted. The registry is derived from decisions, not prior to them. Include a `governance_status` field with at least three states: `governed`, `pre_governance`, `pending`.

11. **Commit `roadmap.md`** after the first implementation phase is scoped. The roadmap's only genuine function is strategic orientation — task tracking, completion records, and pending-role tables all have better homes elsewhere.

---

## The Participant Architecture

The framework operates with four cognitive modes. These modes are more transferable than the specific participant names — a simpler project might need fewer named participants, but the modes themselves are the minimum viable governance architecture.

**Generate** (Gov / S4) — Produces architectural intent. Asks: *what must be true?* Owns ADRs, specs, and the governance reasoning record. The generative layer's identity is "the reasoning record that shapes future reconstructions" — not "the map." The distinction matters: a layer that understands itself as "the map" gradually absorbs territory concerns; a layer that understands itself as "the reasoning record" has a clearer rejection criterion for what doesn't belong.

**Evaluate** (Eva / S3*) — Adversarial compliance verification. Asks: *is this actually true? Is this what we said we would do?* Eva is not a code reviewer or a QA layer. Eva is a governance auditor. Her question at every boundary is whether the output honours the commitments made before implementation began. Eva's most productive findings cluster at the interfaces between artefact types, not within them — a structural property of adversarial evaluation that the generative layer cannot replicate.

**Coordinate** (Nav / S2) — Translates intent into executable delivery contracts. Asks: *how do we make this true?* Nav should be a pure function: repos in, drafts out. No persistent state, no maintained artefacts, no governance overhead beyond the initial declaration ADR. The moment a coordination participant starts maintaining its own artefacts, it acquires governance weight that defeats its purpose.

**Observe** (Adi / outside the VSM stack) — Surfaces patterns, fragilities, and transferable insights. Asks: *what are we learning about how we make things true?* Adi does not participate in governance decisions. Adi's channel is observation files; they accumulate slowly and accurately.

### The generator/evaluator separation is load-bearing

The temptation to use a single AI context for both drafting and evaluating is real, especially early when the project is small. Resist it. Eva's value comes from arriving cold to every proposal. A generator asked to critique its own output will tend toward self-confirmation. The separation is enforced by project boundaries (separate Claude Projects, separate system prompts, separate context), not by instruction.

### Participant system prompts must carry constitutional reasoning

Each participant's system prompt should explain not just what the role does, but why it is structurally separate and what breaks if roles collapse. A prompt that says "you are the evaluator" is weaker than one that says "you are the evaluator because a generator asked to critique its own output tends toward self-confirmation, and the governance gate's value depends on you arriving cold to every proposal."

### Role discomfort is the leading indicator of a missing participant

If reasoning consistently feels uncomfortable in a role — if Gov feels "out of character" doing translation work, or if the Gardener is performing coordination that no participant owns — the framework is telling you a new role exists. The path is: feel the misfit → name the concern → locate it in the VSM → declare the participant. This is how Nav was discovered.

---

## The Two-Repo Architecture

The framework separates a governance repository (Gov, the map) from an implementation repository (Imp, the territory). This separation is not organisational convenience — it is the mechanism that keeps the reasoning record stable as the implementation evolves.

**The one-way reference direction is the structural invariant.** Imp artefacts accumulate references to Gov; Gov never accumulates references to Imp. This holds at every phase of the lifecycle without exception. It is what keeps the map stable as the territory grows.

**Gov describes roles; Imp names instances.** Gov documents describe what a node must be, what a service must guarantee, what constraints apply. The Imp manifest records what currently satisfies those roles — specific hardware, current IPs, OS versions. These are different kinds of facts with different rates of change. Mixing them in Gov documents creates a maintenance burden that scales with infrastructure growth.

**Reproducibility and evolvability are different properties.** Imp + hardware + the bootstrap spark = reproducibility (the system can be rebuilt). Gov = evolvability (the next rebuild can be better than the last). Both are necessary; only the first set is necessary to reconstruct the running system. Any project that conflates "what do you need to run this" with "what do you need to improve this" will produce governance artefacts that over-specify operational dependencies.

---

## The Delivery Lifecycle

The Gov→Imp handoff follows a three-artefact pattern, evaluated at three gates:

**Gov spec** (enduring requirements) → **Eva gate 1** → **Imp contract** (delivery-scoped commitment: spec + plan + prompt) → **Eva gate 2** → **Autonomous execution on branch** → **Eva gate 3** → **Gardener merge**

### Key principles

**Define the interface before the first delivery crosses it.** The delivery lifecycle protocol must be committed (as an ADR) before the first component spec is written. If the first delivery invents its own protocol ad hoc, that protocol becomes implicit convention — never evaluated, difficult to supersede.

**Specs outlive deliveries.** A Gov spec for a component might produce an initial delivery, then another when requirements change, then another when a new site comes online. The spec is the enduring anchor; the contract is the scoped commitment to satisfy it at a point in time.

**The adoption-ADR-plus-spec pattern is a required two-artefact convention.** The ADR records the choice (why this tool over alternatives — a reasoning act). The spec records the contract (what the tool must guarantee — a specification act). Collapsing them into a single artefact embeds alternatives-reasoning into an operational contract, which is a category error.

**The branch is the governance boundary for autonomous agents.** Autonomous execution (RWL or any agentic loop) commits freely on a branch. The governance gate fires at merge. The Gardener merges or doesn't. This is how you get execution velocity and governance integrity without forcing them into conflict.

### The three-layer separation

Within artefacts, separate what was decided (ADRs — immutable, slow) from how it's practised (conventions — revisable, medium) from what craft knowledge accumulates (guidelines — freely evolving, fast). Coupling fast-changing conventions to slow-changing governance decisions is the most common source of unnecessary supersession chains.

---

## Eva: Patterns and Anti-Patterns

### What works

**Pre-empting Eva's likely findings before submission.** Reading a draft adversarially for split records, prescriptive framing, untestable DoD items, and implicit assumptions before submitting reduces round-trips. This is not gaming the evaluation — it is exactly what the evaluation is designed to encourage. Eva's value is in catching what the drafter missed, not what the drafter already knew.

**Submitting co-dependent ADRs as a batch.** Isolated submission of co-dependent artefacts generates blocking findings (forward references) that dissolve immediately under batch evaluation.

**The two-round evaluation cycle as standard.** First pass → targeted fixes → second pass. Multiple blocking findings on first pass is the gate working correctly, not a signal that the artefacts weren't ready.

**Eva's evaluation quality scales with artefact quality.** As the Gardener internalises Eva's patterns, pre-submission quality rises, findings become more advisory than blocking, and cycle velocity increases.

### What to watch

**Eva-predictability risk.** The feedback loop between Gardener learning and Eva patterns can become a game of "pass Eva" rather than genuine quality improvement. The check is the delivery itself — does the governed artefact produce a working system?

**Cross-spec consistency is an open problem.** Eva evaluates proposals against a Gardener-curated context set. If the Gardener doesn't include related specs, Eva can't catch contradictions between them. The risk scales with spec count.

**Eva finds interfaces, not internals.** Eva's most productive findings consistently cluster at the boundaries between artefact types — where a spec meets the registry, where a version field meets the compliance gate. Expect this and value it.

### Eva placement

Eva occupies S3* in the VSM — Beer's independent audit channel, not S3 (operational control). The distinction is non-obvious but structurally important: S3 is health checks and local logic; S3* bypasses the normal hierarchy to provide unbiased verification. Eva's constitutional adversarialism is an S3* property.

---

## Brownfield Adoption

Every real deployment arrives onto terrain that already has tools, networks, and services in place. The framework handles greenfield elegantly (spec first, ADR first). Brownfield requires a retroactive registration path.

**The `pre_governance` status** makes ungoverned components a declared condition rather than a silent gap. The registry's `governance_status` field (`governed`, `pre_governance`, `pending`) is the entry point. A retroactive ADR is the path from `pre_governance` to `governed`.

**Retroactive ADRs are structurally distinct from forward-looking ADRs.** The options-considered section requires particular care — for a tool already in production, the alternatives were often not evaluated at all, and the ADR must be honest about that rather than fabricating a selection rationale. An "adoption context" section may be more appropriate than "options considered."

**The framework exerts a gravitational pull toward debt resolution.** When a sequencing principle (such as "govern the dependency first") requires every artefact to reference governing artefacts or declare debt explicitly, deferral becomes progressively more expensive — each new artefact that touches an ungoverned concept carries its own debt declaration. Resolution is bounded (one ADR closes the gap). This cost inversion is emergent, not designed, and is one of the framework's most powerful properties.

---

## Governance Patterns Worth Naming

### Governance failures are silent; execution failures are loud

This explains why execution tooling (CI/CD, orchestration, deployment automation) has broad adoption while governance-layer tooling remains rare. A missing test breaks the build. A missing ADR breaks nothing — until it breaks everything, months later, when nobody can reconstruct why a decision was made. The framework's primary value is making governance failures visible before they compound.

### The split-record rule

Any time a governance artefact declares another document as authoritative for a piece of information, that information must not also appear in the declaring artefact. The declaration is the pointer; duplicating the content creates a split record. This recurs whenever mapping tables, principles, or lifecycle definitions are referenced across artefacts. Supersede rather than forward-reference.

### Analytical framework vs. design methodology

When adopting a theoretical framework (VSM, Domain-Driven Design, etc.) as a lens for reasoning, commit a decision that names its scope and its limits. Analytical frameworks provide vocabulary and diagnostics; they do not generate prescriptive authority. The failure mode is decisions justified by "VSM requires" rather than by project-specific reasoning through the VSM lens.

### The lifecycle walkthrough as audit instrument

Before deploying this framework in a new context, walk a hypothetical feature through all lifecycle phases and check whether every phase produces a committable artefact in the right repo. Phases that produce nothing, or touch the wrong layer, are gaps before implementation begins.

### Document identity crisis as a design smell

A document trying to serve multiple concerns will grow unwieldy. The resolution is not better organisation — it is asking which functions have better homes elsewhere. The roadmap's identity crisis (task tracking + completion records + strategic orientation) resolved by routing each function to its natural home. What remained was thin and stable.

### Practice-first, convention-second

A framework observation that doesn't yet have three instances is a hypothesis, not a pattern. Filing it is appropriate. Building convention around it is premature. Let friction accumulate rather than pre-building structure for friction you haven't felt yet.

### The complexity test

Both the governance layer and the execution layer, when understood correctly, resolve to something embarrassingly simple. ADRs in Git, a Claude Project connected via GitHub, a human with commit authority. A bash while-loop and three markdown files. If your implementation of this framework feels complex, you are probably solving a problem the framework was designed to make unnecessary. The complexity of a solution is inversely correlated with how correctly the problem was framed.

---

## The Bootstrap Checklist

### Before writing ADR-000

- [ ] Canonical names for all repositories committed to README
- [ ] Glossary stub defining all role terms including dormant participants
- [ ] `principles.md` stub with core invariants
- [ ] `decisions/_template.md` — standalone template with Failure Criteria and Definition of Done

### On first commit

- [ ] `README.md` with correct repo name, directory structure, and naming conventions
- [ ] `decisions/_template.md` — the template is a file, not a code block inside ADR-000
- [ ] `decisions/ADR-000-record-decisions.md` — rationale only, no embedded template
- [ ] `principles.md` — standing constraints including Gardener role definition
- [ ] `glossary.md` — canonical terms, abbreviations, all participant roles (active and dormant)

### Before initialising Eva

- [ ] At least ADR-000 and `principles.md` are committed
- [ ] Eva's evaluation record convention is stated in the lifecycle ADR
- [ ] Eva's system prompt carries constitutional reasoning, not just instructions

### Before the first delivery

- [ ] Delivery lifecycle protocol committed as an ADR (the Gov→Imp interface)
- [ ] Three-artefact convention defined (spec, plan, prompt) with naming that makes boundary provenance self-evident
- [ ] Evaluation gates defined: artefact evaluation, contract evaluation, branch evaluation
- [ ] The registry supports `governance_status` for brownfield components

### Before publication

- [ ] At least two complete deliveries demonstrating the full lifecycle
- [ ] Navigation participant operational (or the coordination function exercised)
- [ ] Compliance gate active
- [ ] Bootstrap lessons document reflects actual practice, not aspirational practice

---

## What Can Be Deferred

These were referenced in early artefacts but should not block the bootstrap:

- `architecture.json` — commit after structural ADRs are accepted
- `roadmap.md` — commit after the first implementation phase is scoped
- `specs/` directory — create when the first component spec is needed
- `exploring/` directory — create when the first exploration note is worth preserving
- Automated compliance (SemaphoreUI + Claude API or equivalent) — defer until Imp is operational
- The immune system / drift detection — defer until the compliance gate has exercised at least once
- GitHub Projects or equivalent task surface — defer until the wup-based workflow feels insufficient
- The reverse arrow (Imp→Gov signal path) — acknowledge but don't formalise until you have three concrete instances

---

## The Maturity Signals

How to know the framework is working:

**Past mistakes prevent future ones, not just record them.** The framework is compounding forward when a design heuristic learned from an early error ("will this convention need to evolve faster than the ADR?") is applied proactively to prevent the same error in a new context.

**The framework tells you what it needs.** Role discomfort signals a missing participant. Repeated debt declarations signal a governance gap that's cheaper to resolve than to keep carrying. Evaluation findings cluster at a boundary that hasn't been committed yet. The framework's feedback is structural, not conversational.

**Sessions that honour the process when it's inconvenient produce better artefacts.** The framework's value is most visible when it's most inconvenient. A framework that only governs easy decisions isn't governing — it's decorating. The quality of a governance framework is measured by the decisions it prevents you from deferring, not by the decisions it automates.

**Tension between participants is productive, not pathological.** When the generative layer proposes and the evaluator blocks, when the observer recommends and the generator pushes back, when the Gardener sides with restraint over action — these are the framework's multi-participant model working as designed. A single participant handling all perspectives would collapse to one side.

**Convergence with independently derived systems is a validation signal.** If your governance framework fits naturally with an execution pattern you had never seen, you were probably reasoning from the right foundations. Convergence of independently derived primitives is stronger evidence than any internal consistency check.
