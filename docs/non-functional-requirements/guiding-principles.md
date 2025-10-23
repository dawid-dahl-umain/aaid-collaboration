# AAID Guiding Principles (Non-Functional Requirements)

These principles represent the philosophy and values that guide `AAID`'s design and use. They're not structurally enforced like the core rules, but they define `AAID`'s spirit. A workflow can technically function as `AAID` without following these principles, but it won't embody what `AAID` stands for.

| Principle                                      | What It Means                                              |
| ---------------------------------------------- | ---------------------------------------------------------- |
| **Principle 1: Technology Agnosticism**        | Workflows describe _what_, never _how_ with specific tools |
| **Principle 2: Developer Mindset**             | Engaged comprehension and incremental progress             |
| **Principle 3: Standing on Giants' Shoulders** | Build on proven methodologies, not AI novelty              |
| **Principle 4: Optimizing for the Future**     | Design for conversation-speed human orchestration          |

## Table of Contents

- [Principle 1: Technology Agnosticism](#principle-1-technology-agnosticism)
- [Principle 2: Developer Mindset](#principle-2-developer-mindset)
- [Principle 3: Standing on Giants' Shoulders](#principle-3-standing-on-giants-shoulders)
- [Principle 4: The Future AAID Is Optimizing For](#principle-4-the-future-aaid-is-optimizing-for)

## Principle 1: Technology Agnosticism

**The Principle:** `AAID` operates at the _workflow_ level, not the _tool_ level. Workflows describe what needs to happen, never how to implement it with specific technologies.

**Why It Matters:** Teams work in diverse contexts with different constraints, existing systems, and technical preferences. By remaining technology-agnostic, `AAID` workflows become universally applicable rather than prescriptive.

**In Practice:**

| ✅ Correct (High-level)                         | ❌ Wrong (Too specific)         |
| ----------------------------------------------- | ------------------------------- |
| "Use a testing framework that supports mocking" | "Use Jest for testing"          |
| "Choose a protocol driver (REST, GraphQL, CLI)" | "Use Supertest for API testing" |
| "Run your build pipeline"                       | "Run npm build"                 |
| "Commit to version control"                     | "Commit to Git"                 |
| "Separate business logic from infrastructure"   | "Use Hexagonal Architecture"    |
| "Organize code with clear boundaries"           | "Use MVC pattern"               |

This principle ensures `AAID` remains portable across languages, frameworks, architectures, and team contexts.

---

## Principle 2: Developer Mindset

**The Principle:** `AAID` augments developers, not replaces them. Two mindsets are essential:

1. **Engaged comprehension**: Understand every line of code, every test, every refactoring. The AI generates; you decide what stays, what changes, and why.
2. **Incremental progress**: Move in small, focused steps. One test at a time. One feature at a time. One refactor at a time.

**Why It Matters:** Without comprehension, you're hoping code works rather than knowing it works. Without incremental steps, you lose control as the AI generates large amounts of potentially problematic code. The review checkpoints (`⏸️ AWAIT USER REVIEW`) enforce this mindset structurally.

**In Practice:**

- Review and understand AI-generated code before accepting it
- Question implementations that don't make sense
- Keep changes small enough to fully comprehend
- Use review checkpoints to validate understanding
- Recognize that speed comes from control, not from skipping reviews

This principle separates professional `AAID` development from "vibe coding" where developers blindly accept AI output.

---

## Principle 3: Standing on Giants' Shoulders

**The Principle:** `AAID` doesn't reinvent software development. It applies proven, battle-tested methodologies from industry leaders and adapts them for AI-augmented collaboration. **Wisdom comes first, AI added after if appropriate!**

**Why It Matters:** Decades of research and practice have established what works in professional software development. `AAID` builds on this foundation rather than discarding it for AI novelty.

**Foundations AAID Builds On:**

- **Kent Beck**: TDD cycles, incremental development
- **Robert C. Martin**: Three Laws of TDD, clean code principles
- **Dave Farley**: Continuous Delivery, four-layer acceptance testing
- **Daniel Terhorst-North**: Behavior-Driven Development methodology
- **Martin Fowler**: Refactoring, evolutionary design, Domain-Specific Languages
- **Aslak Hellesøy**: Gherkin syntax for executable specifications
- **DORA Research**: Developer-owned testing, small batches, deployment metrics

**In Practice:**

When creating new `AAID` workflows, ask:

- What proven methodology addresses this domain?
- How can AI augment this established practice?
- What insights from industry leaders apply here?

This principle ensures `AAID` workflows rest on solid foundations rather than untested AI-first approaches.

---

## Principle 4: The Future AAID Is Optimizing For

**The Principle:** `AAID`'s architecture optimizes towards a future where development happens at conversation speed. As AI becomes faster and more reliable, humans will orchestrate through near-instantaneous voice commands: "Go", "Yes", "Use pure functions", "Back", "Refactor". This vision guides `AAID`'s design decisions today.

**Why It Matters:** This defines `AAID`'s architectural direction. Other workflows optimize for longer autonomous AI sessions (prompt once, wait, review bulk output: "_prompt and pray_"). `AAID` inverts this: optimize for instantaneous AI response to continuous human steering. We're building towards conversation-speed development, not batch processing.

**The Future We're Building Towards:**

When AI becomes sufficiently fast and reliable:

- Commands given by voice, responses appear instantly
- Human attention on steering, not waiting or correcting AI mistakes
- AI generates 100% of code; human conducts the session
- Development flows like conversation: "red phase" → code appears → "yes" → next phase begins

**In Practice Today:**

Current `AAID` design decisions support this future:

- Short iteration cycles (ready for instant AI)
- Mandatory review checkpoints (training ground for future conducting)
- Simple command triggers (voice-ready: "red phase", "green phase")
- Human always in control (foundation for orchestration model)

This principle shapes `AAID`'s architecture, complementing **Developer Mindset** (which defines timeless human values regardless of AI speed).

---

⬅️ Back to [AAID Collaboration Guidelines](../aaid-collaboration.md)
