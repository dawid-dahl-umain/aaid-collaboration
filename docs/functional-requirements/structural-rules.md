# 📐 Structural Rules (Functional Requirements)

These rules define the observable architecture of `AAID` workflows, visible in rules files, workflow diagrams, and articles. They determine what makes a workflow structurally _be_ `AAID`. Without these, it's something else.

| Rule                                    | What It Defines                                                                           |
| --------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Rule 1: Stages vs Phases**            | Two operational modes: flexible collaboration vs strict discipline, with transition point |
| **Rule 2: Internal Phase Pattern**      | All phases within a workflow follow the same sequential steps                             |
| **Rule 3: Instruction Markdown Format** | All phases within a workflow use identical AI instruction format                          |

## Table of Contents

- [Rule 1: Stages vs Phases (Two Operational Modes)](#rule-1-stages-vs-phases-two-operational-modes)
- [Rule 2: Internal Phase Pattern (Within Each Workflow)](#rule-2-internal-phase-pattern-within-each-workflow)
- [Rule 3: Consistent Markdown Instruction Format (Within Each Workflow)](#rule-3-consistent-markdown-instruction-format-within-each-workflow)

## Rule 1: Stages vs Phases (Two Operational Modes)

When it comes to AI agent and human developer interactions, `AAID` workflows operate in two distinct modes:

| Mode       | Behavior                              | Purpose               | Codebase Mutations | Example                                         |
| ---------- | ------------------------------------- | --------------------- | ------------------ | ----------------------------------------------- |
| **Stages** | Flexible conversation, back-and-forth | Varies by workflow    | Not permitted      | Context Providing, Planning, TDD Initialization |
| **Phases** | Strict rules, mandatory sequence      | Disciplined execution | Permitted          | Red → Green → Refactor (in TDD)                 |

**Key Distinction:**

- **Stages**: AI interactions are more spontaneous and free-flowing. Natural dialogue, iteration, exploration. Codebase mutations not permitted.
- **Phases**: AI is instructed to follow hard rules, much like a state machine. Cannot skip steps, must stop for review. Codebase mutations permitted with mandatory supervision through review checkpoints.

**The Transition Point:**

The AI rules file must explicitly state when the mode switches:

```markdown
## The Full `AAID` Workflow Sequence

1. **Stage 1: [Name]** (normal conversation mode)
2. **Stage 2: [Name]** (normal conversation mode, optional)
3. **Stage 3: [Name]** (transition to [discipline mode])
   - **Enter [FIRST PHASE NAME] immediately**
4. **Stage 4: [Name]** (strict phase rules now apply)

Stages 1-3 use normal AI assistance. Stage 4 enforces strict discipline.
```

This explicit statement tells the AI exactly when to switch from collaborative to the state-machine-like mode.

---

## Rule 2: Internal Phase Pattern (Within Each Workflow)

**The Rule:** All phases within a single workflow must follow the same internal pattern of steps.

**What is "Internal Phase Pattern"?**

The sequential steps AI executes INSIDE each individual phase. These are the operational steps within a phase (visible as steps in workflow diagrams).

**Important Distinction:**

- **Phase Cycle**: The sequence of phases (e.g., Red → Green → Refactor)
- **Internal Phase Pattern**: The steps INSIDE each phase (e.g., Collaborate → Verify → Handle Issues → Review)

**Important:** Each workflow defines its own phase cycle AND its own internal pattern. The requirement is internal consistency: all phases in a workflow use the same internal pattern.

**Examples:**

**`AAID` TDD:**

_Phase Cycle_: Red → Green → Refactor (repeats for each test)

_Internal Pattern_ (same for all three phases):

```text
Collaborate → Verify → Handle Issues → Review
```

| Phase       | Collaborate          | Verify                            | Handle Issues                 | Review               |
| ----------- | -------------------- | --------------------------------- | ----------------------------- | -------------------- |
| 🔴 Red      | Write failing test   | Run test, confirm failure         | If passes unexpectedly → STOP | ⏸️ AWAIT USER REVIEW |
| 🟢 Green    | Write minimal code   | Run all tests, confirm pass       | If any fail → STOP            | ⏸️ AWAIT USER REVIEW |
| 🧼 Refactor | Improve code quality | Run all tests, confirm still pass | If any break → STOP           | ⏸️ AWAIT USER REVIEW |

**`AAID` AT (Acceptance Testing):**

_Phase Cycle_: Spec & DSL → Driver Implementation → Refactor

_Internal Pattern_ (same for all three phases):

```text
Collaborate → Verify → Handle Issues → Review
```

| Phase                    | Collaborate                 | Verify                        | Handle Issues                | Review               |
| ------------------------ | --------------------------- | ----------------------------- | ---------------------------- | -------------------- |
| 🔴 Spec & DSL            | Map BDD to DSL              | Spec must fail                | If passes unexpectedly → fix | ⏸️ AWAIT USER REVIEW |
| 🟢 Driver Implementation | Implement driver            | Specs pass or report failures | If broken → fix              | ⏸️ AWAIT USER REVIEW |
| 🧼 Refactor              | Refine & validate isolation | Tests still green             | If broken → fix              | ⏸️ AWAIT USER REVIEW |

**`AAID` Refactoring (hypothetical):**

_Phase Cycle_: Find Seam → Characterize → Transform

_Internal Pattern_ (same for all three phases):

```text
Locate → Isolate → Validate → Review
```

(This demonstrates that each workflow can define both its own phase cycle AND its own internal pattern)

---

## Rule 3: Consistent Markdown Instruction Format (Within Each Workflow)

**The Rule:** The markdown structure used to document phases in the AI rules file must be identical for all phases within a workflow.

**What is "Markdown Instruction Format"?**

The documentation template used in the rules file to teach the AI what to do in each phase.

This is separate from the internal phase flow (Rule 2). This is about HOW you write the rules file documentation.

**Application:**

| Requirement             | Explanation                                                                                                                            |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Within a workflow**   | MUST be identical: if RED phase has "Triggers, Core Principle, Instructions...", GREEN and REFACTOR must have the exact same structure |
| **Across workflows**    | SHOULD aim for similarity for consistency, but MAY differ if needed                                                                    |
| **High-level elements** | Elements like "Triggers" and "Core Principle" are abstract enough to work across most workflows                                        |

**Example: `AAID` TDD uses this structure for all phases:**

```markdown
### 🔴 RED Phase - Write Failing Test

**Triggers:** "write test", "red", "next test"
**Core Principle:** Write only enough test code to fail
**Instructions:** [detailed steps]
**On Success:** Present test, then STOP AND AWAIT USER REVIEW
**On Error:** If test passes unexpectedly, STOP and report
**Next Phase:** GREEN (mandatory)
```

All three TDD phases (RED, GREEN, REFACTOR) use: `Triggers | Core Principle | Instructions | On Success | On Error | Next Phase`

**Why This Matters:**

- Makes rules files scannable and predictable
- Easier for AI to understand and follow instructions
- Easier for contributors to add new phases
- Creates consistent "`AAID` feel" across different workflows

---

⬅️ Back to [AAID Collaboration Guidelines](../aaid-collaboration.md)
