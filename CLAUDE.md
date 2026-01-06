# CLAUDE.md

## Repository Purpose

This repository contains **speck** — agentic coding files for spec-driven development (SDD). These are workflow guides that help AI agents implement features through a structured three-phase approach: Clarify, Design, and Implement.

**This is a meta-repository.** It doesn't contain application code; it contains workflow specification files that are meant to be copied into other projects and referenced by AI agents.

## Repository Structure

```
agent-files/
├── 00-overview.md     # Philosophy and workflow summary
├── 01-clarify.md      # Phase 1: Requirements clarification
├── 02-design.md       # Phase 2: Design document creation
└── 03-implement.md    # Phase 3: Implementation with subagents
```

All substantive content lives in the `agent-files/` directory. The README.md explains the workflow and provides setup examples.

## Core Workflow Concepts

### Three-Phase Development

1. **Clarify Phase** - AI asks focused questions to turn rough ideas into clear requirements. Output: `01_requirements_<feature-name>.md`
2. **Design Phase** - AI autonomously researches codebase and creates design document for approval. Output: `02_design_<feature-name>.md`
3. **Implement Phase** - Main agent coordinates subagents to execute implementation. Output: Code + `03_implementation_<feature-name>.md`

### Key Principles

- **Documents as communication** - All decisions and progress in files, not chat history
- **Subagents for clean context** - Complex work delegated to fresh contexts
- **Two approval gates** - Human reviews after clarify and after design, before implementation
- **AI proposes, human validates** - AI makes decisions autonomously with documented rationale
- **Fresh context per phase** - Each phase can start new conversation by reading artifacts

### Artifacts Structure

When users implement this workflow in their projects, each feature creates:

```
docs/specs/<yymmdd-feature-name>/
├── 01_requirements_<feature-name>.md   # Phase 1 output
├── 02_design_<feature-name>.md         # Phase 2 output
├── 03_implementation_<feature-name>.md # Phase 3 progress
└── research/                           # Research from any phase
```

## Working with These Files

### When Modifying Workflow Files

- **Maintain the philosophy** - Documents over chat, subagents for clean context, AI autonomy with human checkpoints
- **Keep instructions clear** - These files guide AI agents; ambiguity leads to poor execution
- **Preserve phase boundaries** - Clarify focuses on what/why, Design on decisions/alternatives, Implement on execution
- **Test changes** - If modifying workflow, consider how it affects agents in each phase

### Key Differences Between Phases

| Aspect | Clarify | Design | Implement |
|--------|---------|--------|-----------|
| Questions | Ask user directly, one at a time | Research autonomously, don't ask | Coordinator delegates to subagents |
| Decisions | User decides scope | AI decides approach with rationale | Subagents decide implementation details |
| Research | Use subagents for codebase exploration | Use subagents for solution exploration | Main agent doesn't implement directly |
| Output | Requirements document | Standalone design document | Code + implementation log |

### Critical Rules from the Specs

From **01-clarify.md**:
- Ask ONE question per message, wait for answer
- Never invent numbers or metrics
- What/why only, not how
- Use subagents for research

From **02-design.md**:
- Design is "what solution and why", not "how to build"
- Mark decisions clearly with `> **Decision:** ...` pattern
- Document must stand alone (no chat context needed)
- Stay autonomous — don't ask developer for every decision

From **03-implement.md**:
- Main agent coordinates, subagents execute
- Pass full design document to every subagent
- Steps are logical units, not detailed instructions
- Multiple commits per step is normal
- Tests belong with the code, not separate steps
- Human tests before PR creation

## Common Pitfalls to Avoid

1. **Phase confusion** - Don't do design work in clarify phase, don't implement in design phase
2. **Over-asking** - In design phase, research and decide autonomously rather than constantly asking
3. **Under-delegating** - In implement phase, coordinator should delegate to subagents, not implement directly
4. **Detail creep** - Implementation steps should be high-level; subagents are equally capable
5. **Premature PR** - Implementation phase ends with human testing, not PR creation

## This Repository's Maintenance

Since this is a reference repository with workflow specifications:

- Changes should improve clarity or workflow effectiveness
- Breaking changes affect all users who've adopted the workflow
- README.md examples should stay synchronized with agent-files/ content
- Each file should remain independently readable (agents read one at a time)
