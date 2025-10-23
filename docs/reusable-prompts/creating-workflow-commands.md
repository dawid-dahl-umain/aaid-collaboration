# Creating Workflow Commands

Reusable prompt commands speed up workflows with short triggers (like `/red-&-stop`) instead of typing long prompts repeatedly. They also serve as corrective tools when AI deviates from the rules file.

## Why Create Commands?

**Speed:** Type `/research-&-stop` instead of typing long instructions repeatedly across sessions

**Explicit triggers:** Invoke specific workflow actions on demand (planning, research, context gathering)

**Corrective steering:** Phase commands redirect AI back to discipline when it forgets or ignores the rules file (which happens regularly since AI isn't 100% reliable)

## Command Structure

```markdown
# /command-name

**Purpose:** [One sentence description]

**Workflow Stage/Phase:** [Where this fits in workflow]

**Instructions:**

1. [What AI should do]
2. [Verification step if applicable]
3. **STOP AND AWAIT USER REVIEW** (for phase commands)

**Reference:** Follow [phase/stage name] rules in [rules file location]
```

## Aligning with Your Workflow

**Stage commands** (collaborative): Explicitly trigger planning, research, or context gathering actions

- Example: `/project-context`, `/research-&-stop`

**Phase commands** (disciplined): Redirect AI to strict workflow discipline when it deviates from the rules file

- Example: `/red-&-stop`, `/green-&-stop`, `/refactor-&-stop`
- These reinforce mandatory sequences and review checkpoints

Phase commands should reflect your workflow's internal phase pattern. If phases follow `Collaborate → Verify → Handle Issues → Review`, structure commands to match those substeps.

## Design Guidelines

- **Keep simple**: Commands should be memorable and voice-ready (`/red-&-stop` not `/execute-red-phase-with-verification`)
- **Technology agnostic**: "Run test suite" not "Run npm test"
- **Reference rules file**: Commands trigger behavior; rules file remains single source of truth
- **Include stop points**: Phase commands must enforce `AWAIT USER REVIEW`

## Quick Examples

### Phase Command

```markdown
# /green-&-stop

**Purpose:** Enter GREEN phase - write simplest code to pass test

**Workflow Phase:** GREEN (TDD Stage 4)

**Instructions:**

1. Write minimum code to make failing test pass (start naive/hardcoded)
2. Run all tests and verify they pass
3. **STOP AND AWAIT USER REVIEW**

**Reference:** Follow GREEN phase rules in `.cursor/rules/aaid.mdc`
```

### Investigation Command

```markdown
# /analyze-&-stop

**Purpose:** Diagnose problems without making changes

**Workflow Use:** Error handling in any phase

**Instructions:**

1. Analyze the error/failure and root cause
2. Present findings and potential solutions
3. **STOP AND AWAIT USER REVIEW** before implementing fixes

**Reference:** Follow investigation protocols in AAID rules
```

## Reference: Working Examples

For complete working examples of reusable commands used in production AAID workflows, see [Appendix B: Helpful Commands](https://github.com/dawid-dahl-umain/augmented-ai-development/blob/main/appendices/appendix-b/reusable-prompts.md) in the main AAID repository.

---

⬅️ Back to [AAID Collaboration Guidelines](../aaid-collaboration.md)
