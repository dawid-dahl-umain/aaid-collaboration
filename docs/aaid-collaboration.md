# AAID Collaboration Guidelines

## Table of Contents

- [Purpose](#purpose)
- [Glossary (Ubiquitous Language)](#glossary-ubiquitous-language)
- [The Four Core AAID Rules](#the-four-core-aaid-rules)
  - [Rule 1: Stages vs Phases (Two Operational Modes)](#rule-1-stages-vs-phases-two-operational-modes)
  - [Rule 2: Internal Phase Pattern (Within Each Workflow)](#rule-2-internal-phase-pattern-within-each-workflow)
  - [Rule 3: Technology Agnosticism](#rule-3-technology-agnosticism)
  - [Rule 4: Consistent Markdown Instruction Format (Within Each Workflow)](#rule-4-consistent-markdown-instruction-format-within-each-workflow)
- [Quick Validation Checklist](#quick-validation-checklist)
- [Contributing to AAID](#contributing-to-aaid)
  - [Creating a New Workflow](#creating-a-new-workflow)
  - [Improving Existing Workflows](#improving-existing-workflows)
- [Summary](#summary)
- [Resources](#resources)

## Purpose

This document defines the core architectural rules for `AAID` workflows. Use it when:

- **Creating new workflows**
- **Improving existing workflows**

## Glossary (Ubiquitous Language)

| Term                            | Definition                                                                                                                                                                                                                   |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`AAID` Workflow**             | A complete development process (like TDD or Acceptance Testing) that follows the four `AAID` rules. Contains both Stages and Phases.                                                                                         |
| **Stage**                       | A step in the workflow using collaborative mode where developer and AI have flexible, conversational back-and-forth to understand, plan, and align.                                                                          |
| **Phase**                       | A step in the workflow using disciplined mode where AI follows strict rules, mandatory sequences, and must stop for review after each phase. Phases exist within a Stage (e.g., Stage 4 contains RED/GREEN/REFACTOR phases). |
| **Internal Phase Pattern**      | The sequential substeps that happen inside each phase (e.g., `Collaborate → Verify → Handle Issues → Review`). All phases within a workflow must use the same pattern.                                                       |
| **Transition Point**            | The explicit moment documented in the rules file where the workflow shifts from collaborative Stages to disciplined Phases. Must be clearly stated so AI knows when to enforce strict rules.                                 |
| **Collaborative Mode**          | The operational mode during Stages where AI behavior is flexible, conversational, and exploratory. AI can iterate freely with the developer.                                                                                 |
| **State Machine Mode**          | The operational mode during Phases where AI behavior is strict and rule-enforced. AI must follow exact sequences and cannot skip steps. Also called "disciplined mode".                                                      |
| **Markdown Instruction Format** | The documentation template structure used in the rules file to teach AI what to do in each phase (e.g., Triggers, Core Principle, Instructions, etc.). Must be identical for all phases within a workflow.                   |
| **Rules File**                  | The markdown document (like `.cursor/rules/aaid.mdc`) that contains instructions for the AI, defining the workflow sequence, phases, and behavioral rules.                                                                   |
| **Review Checkpoint**           | A mandatory stop point where AI must present work and wait for developer approval before proceeding. Marked as `⏸️ AWAIT USER REVIEW` in phases.                                                                             |
| **Verification**                | The step where AI executes commands on the developer's system to confirm success (e.g., running tests, building code). Produces concrete pass/fail results, not just AI reasoning.                                           |
| **Workflow Diagram**            | A visual representation (usually Mermaid) showing the flow of Stages, the transition point, and Phases with their internal patterns.                                                                                         |

## The Four Core AAID Rules

### Rule 1: Stages vs Phases (Two Operational Modes)

When it comes to AI agent and human developer interactions, `AAID` workflows operate in two distinct modes:

| Mode       | Behavior                              | Purpose                                 | Example                                         |
| ---------- | ------------------------------------- | --------------------------------------- | ----------------------------------------------- |
| **Stages** | Flexible conversation, back-and-forth | Preparation, setup, alignment           | Context Providing, Planning, TDD Initialization |
| **Phases** | Strict rules, mandatory sequence      | Disciplined execution with verification | RED → GREEN → REFACTOR (in TDD)                 |

**Key Distinction:**

- **Stages**: AI interactions are more spontaneous and free-flowing; natural dialogue, iteration, exploration
- **Phases**: AI is instructed to follow hard rules, much like a state machine; cannot skip steps, must stop for review

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

### Rule 2: Internal Phase Pattern (Within Each Workflow)

**The Rule:** All phases within a single workflow must follow the same internal pattern.

**What is "Internal Phase Pattern"?**

The sequential steps AI goes through INSIDE each phase (visible as substeps in workflow diagrams).

**Important:** Each workflow defines its own pattern. The requirement is internal consistency within that workflow.

**Examples:**

**`AAID` TDD Internal Pattern:**

```text
Collaborate → Verify → Handle Issues → Review
```

| Phase       | Collaborate          | Verify                            | Handle Issues                 | Review               |
| ----------- | -------------------- | --------------------------------- | ----------------------------- | -------------------- |
| 🔴 RED      | Write failing test   | Run test, confirm failure         | If passes unexpectedly → STOP | ⏸️ AWAIT USER REVIEW |
| 🟢 GREEN    | Write minimal code   | Run all tests, confirm pass       | If any fail → STOP            | ⏸️ AWAIT USER REVIEW |
| 🧼 REFACTOR | Improve code quality | Run all tests, confirm still pass | If any break → STOP           | ⏸️ AWAIT USER REVIEW |

**`AAID` AT (Acceptance Testing) Internal Pattern:**

```text
Collaborate → Verify → Handle Issues → Review
```

| Phase      | Collaborate                 | Verify                        | Handle Issues                | Review               |
| ---------- | --------------------------- | ----------------------------- | ---------------------------- | -------------------- |
| 🔴 Phase 1 | Map BDD to DSL              | Spec must fail                | If passes unexpectedly → fix | ⏸️ AWAIT USER REVIEW |
| 🟢 Phase 2 | Implement driver            | Specs pass or report failures | If broken → fix              | ⏸️ AWAIT USER REVIEW |
| 🧼 Phase 3 | Refine & validate isolation | Tests still green             | If broken → fix              | ⏸️ AWAIT USER REVIEW |

**`AAID` Refactoring might use a different pattern:**

```text
Seam → Characterize → Verify → Transform
```

(This is hypothetical - the point is each workflow can define its own structure)

**The Requirement:**

- TDD's three phases all use TDD's pattern ✅
- AT's three phases all use AT's pattern ✅
- Refactoring's phases would all use Refactoring's pattern ✅
- Mixing different patterns within one workflow ❌

**Why This Matters:**

- Creates predictable rhythm for developers
- Allows visual diagrams to show repeating patterns
- Makes phases feel consistent

---

### Rule 3: Technology Agnosticism

**The Rule:** `AAID` must never mandate specific tools, frameworks, libraries, or architectures.

**Why:** Teams must choose technical implementations based on their context.

| ✅ Correct (High-level)                         | ❌ Wrong (Too specific)         |
| ----------------------------------------------- | ------------------------------- |
| "Use a testing framework that supports mocking" | "Use Jest for testing"          |
| "Choose a protocol driver (REST, GraphQL, CLI)" | "Use Supertest for API testing" |
| "Run your build pipeline"                       | "Run npm build"                 |
| "Commit to version control"                     | "Commit to Git"                 |

**Principle:** `AAID` operates at _workflow_ level, not _tool_ level.

---

### Rule 4: Consistent Markdown Instruction Format (Within Each Workflow)

**The Rule:** The markdown structure used to document phases in the AI rules file must be identical for all phases within a workflow.

**What is "Markdown Instruction Format"?**

The documentation template used in the rules file to teach the AI what to do in each phase.

This is separate from the internal phase flow (Rule 2). This is about HOW you write the rules file documentation.

**Application:**

| Requirement             | Explanation                                                                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Within a workflow**   | MUST be identical - if RED phase has "Triggers, Core Principle, Instructions...", GREEN and REFACTOR must have the exact same structure |
| **Across workflows**    | SHOULD aim for similarity for consistency, but MAY differ if needed                                                                     |
| **High-level elements** | Elements like "Triggers" and "Core Principle" are abstract enough to work across most workflows                                         |

**Example - `AAID` TDD uses this structure for all phases:**

```markdown
### 🔴 RED Phase - Write Failing Test

**Triggers:** "write test", "red", "next test"
**Core Principle:** Write only enough test code to fail
**Instructions:** [detailed steps]
**On Success:** Present test, then STOP AND AWAIT USER REVIEW
**On Error:** If test passes unexpectedly, STOP and report
**Next Phase:** GREEN (mandatory)
```

All three TDD phases (RED, GREEN, REFACTOR) use: `Triggers → Core Principle → Instructions → On Success → On Error → Next Phase`

**Why This Matters:**

- Makes rules files scannable and predictable
- Easier for AI to understand and follow instructions
- Easier for contributors to add new phases
- Creates consistent "`AAID` feel" across different workflows

---

## Quick Validation Checklist

| Rule       | Validation Question                                                                    | ✓   |
| ---------- | -------------------------------------------------------------------------------------- | --- |
| **Rule 1** | Are collaborative Stages clearly separated from disciplined Phases?                    | ☐   |
|            | Is the transition point explicitly documented in the rules file?                       | ☐   |
| **Rule 2** | Do all phases within this workflow follow the same internal pattern?                   | ☐   |
|            | Can you overlay phase diagrams and see identical step patterns?                        | ☐   |
| **Rule 3** | Does the workflow avoid naming specific tools/frameworks/architectures?                | ☐   |
|            | Could teams using different tech stacks or architectures both use this workflow?       | ☐   |
| **Rule 4** | Do all phases within this workflow use identical markdown structure in the rules file? | ☐   |
|            | Are the section headers consistent across all phases within this workflow?             | ☐   |

## Contributing to AAID

### Creating a New Workflow

#### 1. Analyze Your Domain

- What problem are you solving?
- What needs collaboration (Stages) vs discipline (Phases)?
- Where is the transition point?

#### 2. Design Internal Phase Pattern (Rule 2)

- What sequential steps happen inside each phase?
- Define the pattern: `[Step 1] → [Step 2] → [Step 3] → ...` (as many steps as needed)
- This pattern must be identical for all phases in your workflow

#### 3. Choose Markdown Structure (Rule 4)

Recommended sections (high-level enough for most workflows):

- **Triggers** - Keywords that activate the phase
- **Core Principle** - What this phase accomplishes
- **Instructions** - Detailed steps
- **On Success** - Typically: "STOP AND AWAIT USER REVIEW"
- **On Error** - Typically: "STOP and report what failed"
- **Next Phase** - Which phase comes next

Use identical structure for all phases.

#### 4. Document Transition Point (Rule 1)

In your rules file:

```markdown
Stages 1-X use normal AI assistance.
Stage Y enforces strict [your workflow name] discipline.
```

#### 5. Maintain Technology Agnosticism (Rule 3)

Avoid naming specific tools. Focus on what needs to happen, not how.

#### 6. Validate

Use the Quick Validation Checklist above.

#### 7. Create Rules File

Write the AI instructions file (e.g., `.cursor/rules/your-workflow.mdc`) containing:

- Workflow sequence documentation (Stages 1-X with transition point)
- All phase definitions using your chosen markdown structure (Rule 4)
- Recognition triggers so AI knows when this workflow is active

#### 8. Create Workflow Diagram

Use [Mermaid Live Editor](https://mermaid.live/) showing Stages, transition point, and Phases with internal pattern.

### Improving Existing Workflows

1. **Identify which rule your improvement relates to**
2. **Show before/after** (diagram updates, rules file changes)
3. **Validate consistency**: If changing one phase, must others change too? (Rules 2 & 4 require consistency)

## Summary

`AAID` workflows follow four rules:

1. **Stages vs Phases** - Collaborative mode vs disciplined mode, with explicit transition
2. **Internal Phase Pattern** - All phases within a workflow share the same sequential steps
3. **Technology Agnosticism** - Never mandate specific tools/frameworks
4. **Markdown Format** - All phases within a workflow use identical documentation structure

Follow these → `AAID`-style ✅  
Break these → Something else ❌

## Resources

- [Main `AAID` Guide](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/docs/aidd-workflow.md)
- [TDD Diagram](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/aaid-workflow-diagram.mermaid)
- [AT Diagram](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/appendices/appendix-a/aaid-at-workflow.diagram.mermaid)
- [Demo Repository](https://github.com/dawid-dahl-umain/augmented-ai-development-demo)
