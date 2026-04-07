# Bootstrap Guide

*How to initialise governance for your project using this framework.
Follow these steps in order. Each step depends on the ones before it.*

For the reasoning behind this sequence, see
[gov-bootstrap-lessons.md](gov-bootstrap-lessons.md).

---

## Prerequisites

You need:

- Two Git repositories: one for governance (the map), one for implementation
  (the territory). Create both before you begin.
- A human with commit authority — the Gardener. This is you.
- An AI environment for the Generate participant (e.g. a Claude Project with
  access to the governance repo).
- A separate AI environment for the Evaluate participant. Separate means
  separate context — a different project, different system prompt, different
  conversation. The evaluator must arrive cold to every proposal.

The Coordinate and Observe participants begin dormant. You will activate them
later. Declare them now so you don't have to amend the architecture later.

---

## Phase 1 — Founding Commit

**Do all of these before writing ADR-000.** They are the ground truth that
ADRs are evaluated against.

### Step 1: Settle canonical names

Choose permanent names for:

- Both repositories
- The Gardener (your name or handle)
- Your project's participants (the Generate, Evaluate, Coordinate, and
  Observe roles — give them names or use the mode names directly)
- Any sites, environments, or domains your project will reference

Write these into `README.md`. Use the provided README template as a starting
point. Naming inconsistencies in the founding artefacts are disproportionately
expensive to fix later — every future artefact references these names.

### Step 2: Populate the glossary

Copy `glossary-template.md` to `glossary.md`. Fill in:

- Your participant names in the role definitions
- Your theoretical framework mapping (if using one)
- Any domain terms your first ADRs will reference

Every term that appears in a governance artefact must be defined here first.
Undefined terms generate blocking evaluation findings.

### Step 3: Populate the principles

Copy `principles-template.md` to `principles.md`. The foundational principles
are already stated. Add your project-specific expression of each one where
the template indicates.

Do not add principles that don't yet have three instances of practice behind
them. Let them emerge from ADR work. When an ADR introduces a new principle,
add it to the "ADR-Introduced Principles" section with the ADR reference.

### Step 4: Copy the ADR template

The file `decisions/_template.md` is already in place. Review it. Ensure the
sections match your project's needs. The template is a Gardener-maintained
file — it can evolve without ADR supersession.

### Step 5: Commit the founding set

Commit these together as the founding commit:

- `README.md`
- `glossary.md`
- `principles.md`
- `decisions/_template.md`
- `architecture-schema.json`
- Empty directories: `decisions/evals/`, `mappings/`, `specs/`

This is your ground truth. Everything that follows is evaluated against it.

---

## Phase 2 — The ADR Chain

### Step 6: Commit ADR-000

Use `decisions/ADR-000-record-decisions.md` as your starting point. Adapt it
to your project:

- Set the date and author
- Adjust the evaluation record path convention if needed
- Mark the Definition of Done items as complete

ADR-000 is grandfathered — it defines the evaluation gate, so it cannot itself
pass through the gate. Commit it directly.

### Step 7: Initialise the Evaluate participant

Set up the Evaluate participant's environment now. It needs:

- Read access to the governance repository
- A system prompt that explains its constitutional role — not just "you are
  the evaluator" but why the role is structurally separate and what breaks
  if it shares context with the generator
- Access to the committed artefacts: principles, glossary, ADR-000, template

The evaluator's quality scales with the richness of the ground truth it can
reason against. The more committed artefacts it has, the more precise its
findings.

### Step 8: Commit structural ADRs

Write and submit the framework-layer ADRs in dependency order. The recommended
sequence (adapt to your project):

1. **Two-repository structure** — establishes the map/territory separation
2. **Repository hosting** — where the repos live, migration triggers
3. **Participant architecture** — all four modes declared, dormancy states
   for inactive roles, activation triggers named
4. **Analytical framework** (if applicable) — e.g. VSM as a lens, with
   scope and limits stated
5. **Concern-to-tool mapping** — which tool serves which function; the
   mapping table lives in a reference file (`mappings/concern-to-tool.md`),
   not inline in the ADR
6. **Infrastructure manifest** — where instance facts live (the implementation
   repo, not governance)
7. **Delivery lifecycle** — the five-phase handoff from governance to
   implementation: scope → spec → contract → execute → accept
8. **Automated compliance gate** — intent for automated checking, activated
   when execution tooling is ready

Submit co-dependent ADRs as a batch. The Evaluate participant can resolve
forward references between co-dependent artefacts when it sees them together.
The two-round evaluation cycle (first pass → fixes → second pass) is standard.

**At bootstrap,** the structural ADRs (Step 8) and principle ADRs (Step 9)
may be submitted as a single batch — the distinction between them is
conceptual (framework structure vs. discovered principles), not procedural.
Separate evaluation rounds are not required.

### Step 9: Commit principle ADRs

After the structural framework is in place, commit ADRs for principles
discovered through practice:

- **Information architecture principles** — resist structural accumulation;
  cold for mass, hot for essence
- **Governance dependency sequencing** — govern the dependency first; silent
  reliance on ungoverned concepts is a drafting error
- **Seed principle amendment** (if the founding `principles.md` needs
  refinement based on practice)

Each of these adds its principle to `principles.md` with the ADR reference.

---

## Phase 3 — Derived Artefacts

### Step 10: Populate the registry

Create `architecture.json` using the schema in `architecture-schema.json`.
The registry is derived from committed ADRs — do not populate it before the
structural ADRs that govern its entries are accepted.

For components that predate governance, use `governance_status: "pre_governance"`.
These are declared gaps, not invisible ones. Each one is a candidate for a
retroactive ADR.

### Step 11: Populate the concern-to-tool mapping

Create `mappings/concern-to-tool.md` with an entry for every tool governed
by an accepted ADR. The mapping model is governed by the concern-to-tool ADR;
subsequent tool adoptions add rows and cite that ADR.

---

## Phase 4 — First Delivery

### Step 12: Write your first Gov spec

Pick a component and write its specification in `specs/`. The spec describes
enduring requirements — what the component must guarantee, not how to
configure it. Submit it to the Evaluate participant.

### Step 13: Draft the implementation contract

Activate the Coordinate participant (or perform coordination yourself).
The contract translates the Gov spec into a delivery-scoped commitment:
what will be built, what tasks are involved, what constraints apply.

### Step 14: Execute and evaluate

Run the delivery on a branch. When complete, submit the branch output to the
Evaluate participant for branch evaluation. The Gardener merges or rejects.

---

## After Bootstrap

Your governance framework is now operational. From here:

- **Domain ADRs** govern your project-specific concerns in dependency order
- **Retroactive ADRs** bring pre-governance components into the governed registry
- **The Observe participant** activates when you want meta-analysis across
  sessions — patterns, fragilities, transferable insights
- **gov-bootstrap-lessons.md** documents the reasoning behind every choice
  you just made, and the failure modes to watch for

The framework's maturity signals: past mistakes prevent future ones, the
framework tells you what it needs (role discomfort, clustering evaluation
findings), and tension between participants is productive.
