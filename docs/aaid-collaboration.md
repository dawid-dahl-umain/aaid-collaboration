# AAID Collaboration Guidelines

## Table of Contents

- [Purpose](#purpose)
- [Glossary (Ubiquitous Language)](#glossary-ubiquitous-language)
- [📐 Structural Rules (Functional Requirements)](#-structural-rules-functional-requirements)
- [🎯 AAID Guiding Principles (Non-Functional Requirements)](#-aaid-guiding-principles-non-functional-requirements)
- [Contributing to AAID](#contributing-to-aaid)
  - [Creating a New Workflow](#creating-a-new-workflow)
  - [Improving Existing Workflows](#improving-existing-workflows)
- [Validation Checklists](#validation-checklists)
  - [Functional Requirements Validation](#functional-requirements-validation)
  - [Non-Functional Requirements Validation](#non-functional-requirements-validation)
- [Resources](#resources)

## Purpose

This document defines the structural rules and guiding principles for `AAID` workflows. It separates:

- **Functional Requirements** (Structural Rules): The observable architecture visible in rules files, workflow diagrams, and articles. These define what makes a workflow structurally _be_ `AAID`.
- **Non-Functional Requirements** (Guiding Principles): The philosophy and values that guide `AAID`'s design and use. These define `AAID`'s spirit.

Use this document when:

- **Creating new workflows**
  - _E.g. `AAID`: Refactoring_
- **Improving existing workflows**
  - _E.g. `AAID`: Acceptance Testing_

## Glossary (Ubiquitous Language)

| Term                            | Definition                                                                                                                                                                                                                   |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`AAID` Workflow**             | A complete development process (like TDD or Acceptance Testing) that follows the structural rules and guiding principles. Contains both Stages and Phases.                                                                   |
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

## 📐 Structural Rules (Functional Requirements)

These rules define the observable architecture of `AAID` workflows, visible in rules files, workflow diagrams, and articles. They determine what makes a workflow structurally _be_ `AAID`. Without these, it's something else.

| Rule                                    | What It Defines                                                                           |
| --------------------------------------- | ----------------------------------------------------------------------------------------- |
| **Rule 1: Stages vs Phases**            | Two operational modes: flexible collaboration vs strict discipline, with transition point |
| **Rule 2: Internal Phase Pattern**      | All phases within a workflow follow the same sequential substeps                          |
| **Rule 3: Instruction Markdown Format** | All phases within a workflow use identical AI instruction format                          |

📖 **[Read the complete Structural Rules →](functional-requirements/structural-rules.md)**

## 🎯 AAID Guiding Principles (Non-Functional Requirements)

These principles represent the philosophy and values that guide `AAID`'s design and use. They're not structurally enforced like the core rules, but they define `AAID`'s spirit. A workflow can technically function as `AAID` without following these principles, but it won't embody what `AAID` stands for.

| Principle                                          | What It Means                                              |
| -------------------------------------------------- | ---------------------------------------------------------- |
| **Principle 1: Technology Agnosticism**            | Workflows describe _what_, never _how_ with specific tools |
| **Principle 2: Developer Mindset**                 | Engaged comprehension and incremental progress             |
| **Principle 3: Standing on Giants' Shoulders**     | Build on proven methodologies, not AI novelty              |
| **Principle 4: The Future We're Building Towards** | Design for conversation-speed human orchestration          |

📖 **[Read the complete Guiding Principles →](non-functional-requirements/guiding-principles.md)**

## Contributing to AAID

### Creating a New Workflow

Follow these steps to create a workflow that meets both functional requirements (structural rules) and non-functional requirements (guiding principles).

#### 1. Analyze Your Domain

- What problem are you solving?
- What needs collaboration (Stages) vs discipline (Phases)?
- Where is the transition point?

#### 2. Apply Structural Rules (FR)

Design your workflow architecture:

- **Rule 1: Document Transition Point**

  - Explicitly state when the workflow shifts from Stages to Phases
  - Example: "Stages 1-3 use normal AI assistance. Stage 4 enforces strict [workflow name] discipline."

- **Rule 2: Design Internal Phase Pattern**

  - Define the sequential substeps inside each phase: `[Step 1] → [Step 2] → [Step 3] → ...`
  - This pattern must be identical for all phases in your workflow

- **Rule 3: Choose Phase Markdown Structure**
  - Use identical markdown structure for all phases
  - Recommended sections: Triggers, Core Principle, Instructions, On Success, On Error, Next Phase

#### 3. Apply Guiding Principles (NFR)

Ensure your workflow embodies `AAID`'s philosophy:

- **Technology Agnosticism**: Avoid naming specific tools. Focus on what needs to happen, not how.
- **Developer Mindset**: Include review checkpoints; keep phases incremental.
- **Standing on Giants' Shoulders**: Base design on proven methodologies; cite the foundations you're building on.
- **The Future We're Building Towards**: Design for rapid human-AI cycles; use simple commands ready for voice input.

#### 4. Create Rules File

Write the AI instructions file (e.g., `.cursor/rules/your-workflow.mdc`) containing:

- Workflow sequence documentation (Stages 1-X with transition point)
- All phase definitions using your chosen markdown structure (Rule 3)
- Recognition triggers so AI knows when this workflow is active

#### 5. Create Workflow Diagram

Use [Mermaid Live Editor](https://mermaid.live/) showing Stages, transition point, and Phases with internal pattern.

#### 6. Write Human-Readable Article

Create a comprehensive guide (like the [Main `AAID` Guide](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/docs/aidd-workflow.md)) that teaches developers how to use this workflow. The article should:

- Explain the workflow's purpose and when to use it
- Walk through each stage and phase with examples
- Show real-world application with code samples
- Reference the established methodology you're building on (Standing on Giants' Shoulders)

### Improving Existing Workflows

1. **Identify which rule or principle your improvement relates to** (FR or NFR)
2. **Show before/after** (diagram updates, rules file changes)
3. **Validate consistency**: If changing one phase, must others change too? (Rules 2 & 3 require consistency within a workflow)
4. **Ensure philosophical alignment**: Does the improvement maintain `AAID`'s guiding principles?

## Validation Checklists

Once you've created your workflow artifacts (rules file, diagram, article), use these checklists to verify completeness.

### Functional Requirements Validation

**These MUST all pass for a workflow to be considered `AAID`.**

| Rule       | Validation Question                                                            | ✓   |
| ---------- | ------------------------------------------------------------------------------ | --- |
| **Rule 1** | Is the transition point from Stages to Phases explicitly documented?           | ☐   |
| **Rule 2** | Do all phases follow the same internal pattern (visible in workflow diagrams)? | ☐   |
| **Rule 3** | Do all phases use identical markdown structure in the rules file?              | ☐   |

### Non-Functional Requirements Validation

**These SHOULD be followed to maintain `AAID`'s philosophy and values.**

| Principle                                          | Validation Question                                                          | ✓   |
| -------------------------------------------------- | ---------------------------------------------------------------------------- | --- |
| **Principle 1: Technology Agnosticism**            | Does the workflow avoid prescribing specific tools/frameworks/architectures? | ☐   |
| **Principle 2: Developer Mindset**                 | Does the workflow enforce review checkpoints and incremental progress?       | ☐   |
| **Principle 3: Standing on Giants' Shoulders**     | Can you identify which established practices influenced this design?         | ☐   |
| **Principle 4: The Future We're Building Towards** | Does the workflow support rapid, voice-ready human-AI cycles?                | ☐   |

## Resources

- [Main `AAID` Guide](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/docs/aidd-workflow.md)
- [`AAID`: TDD Diagram](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/aaid-workflow-diagram.mermaid)
- [`AAID`: Acceptance Testing Diagram](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/appendices/appendix-a/aaid-at-workflow.diagram.mermaid)
- [Demo Repository](https://github.com/dawid-dahl-umain/augmented-ai-development-demo)
