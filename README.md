# speck

> *Agentic coding files for spec driven development (SDD)*

→ Take me directly to the [agent files](agent-files/).

## Workflow

### Phases

**1/ Clarify**  
Turn an idea into specified requirements through conversation. AI asks focused questions, you answer. Together you shape what the feature should be.

**2/ Design**  
AI works autonomously—researches the codebase, searches the web, explores options, makes decisions and documents them. Produces a standalone design doc you can review and approve. Correct the approach here while it's cheap, not at PR time.

**3/ Implement**  
AI autonomously implements the feature, documents findings, and prepares a PR-ready branch.

See [agent files](agent-files/) for more details on each phase.

### Key Concepts

- **Work asynchronously** - Phase 1 is a focused conversation you choose to have. Phases 2-3 run autonomously—AI works, you review when ready. No constant context switches pulling you back.
- **Document-based** - All decisions and progress live in files, not chat history. Easy to review, easy to resume in fresh sessions, works with any tool.
- **Subagents** - Features are too complex for a single context window. Subagents handle focused tasks with clean context while the main agent stays on the big picture.

### Artifacts

Each phase produces artifacts in `docs/specs/<yymmdd-feature-name>/` (plus the code itself in Phase 3):

```
docs/specs/241219-user-export/
├── 01-requirements.md      # Phase 1 output
├── 02-design.md            # Phase 2 output
├── 03-implementation.md    # Phase 3 progress and findings
└── research/               # Research from any phase
    └── ...
```

## Beyond the Workflow: Context Matters

These specs alone won't do magic.

This workflow defines *how* to build features, but other context shapes *what* gets built and *how well*:

- **Clarification phase** needs: Product vision, user personas, business constraints, ...
- **Design phase** needs: System architecture, existing patterns, integration points, ...
- **Implementation phase** needs: Coding standards, test patterns, project conventions, ...

Good, structured code—and the documentation around it—makes AI assistance more effective.

## Setup

Use any agentic coding tool. Point it at these workflow guides and iterate based on your needs.

<details>
<summary>Example: Claude Code setup</summary>

**1. Copy the workflow files** into your project (e.g., `docs/speck/`).

**2. Add commands** to `.claude/commands/`:

```markdown
<!-- sdd-1-clarify.md -->
# SDD Phase 1: Clarify

Start Phase 1 of the spec-driven development workflow.

## Arguments

$ARGUMENTS - The rough idea or feature description

## Instructions

First, read `docs/speck/00-overview.md` to understand the overall workflow.
Then, read and follow the phase instructions in `docs/speck/01-clarify.md`.

For product context, read `docs/product/vision.md`.

Create the spec folder at `docs/specs/<yymmdd-feature-name>/` where:
- `yymmdd` is today's date
- `feature-name` is a short kebab-case name derived from the idea

The rough idea provided is:

    $ARGUMENTS
```

```markdown
<!-- sdd-2-design.md -->
# SDD Phase 2: Design

Start Phase 2 of the spec-driven development workflow.

## Arguments

$ARGUMENTS - Path to the spec folder (e.g., docs/specs/241219-user-export)

## Instructions

First, read `docs/speck/00-overview.md` to understand the overall workflow.
Then, read and follow the phase instructions in `docs/speck/02-design.md`.

For architecture context, read `docs/architecture/`.

The spec folder is: $ARGUMENTS
```

```markdown
<!-- sdd-3-implement.md -->
# SDD Phase 3: Implement

Start Phase 3 of the spec-driven development workflow.

## Arguments

$ARGUMENTS - Path to the spec folder (e.g., docs/specs/241219-user-export)

## Instructions

First, read `docs/speck/00-overview.md` to understand the overall workflow.
Then, read and follow the phase instructions in `docs/speck/03-implement.md`.

For coding guidelines, read `docs/guidelines/`.

The spec folder is: $ARGUMENTS
```

Adjust the context paths to match your project structure.

**3. Usage:**

```bash
claude "/sdd-1-clarify add user export feature"
claude "/sdd-2-design docs/specs/241219-user-export"
claude "/sdd-3-implement docs/specs/241219-user-export"
```

As you complete features, your `docs/specs/` folder becomes additional context—examples of how decisions were made.

Other agentic tools will have similar concepts—custom commands or prompts that reference files. Adapt the pattern to your tool.
</details>
