# FORGE — Framework for Orchestrated Agent Generation Engine

Multi-agent system for generating Copilot Studio agent configurations.

## Architecture

```
[You provide: agent name + scope + sector + tone]
        ↓
  FORGEMASTER — Orchestrator
  → collects input, coordinates all agents, delivers the package
        ↓
  Phase 0.5 — Mandatory Clarification
  → asks targeted questions if input is vague or incomplete
        ↓
  INSTRUCTOR — Instructions Generator
  → generates the complete system prompt
  → MUST ask clarifying questions if input is unclear
        ↓
  DESCRIPTOR — Description Generator
  → generates display name + short/long descriptions
  → MUST ask clarifying questions if scope is ambiguous
        ↓
  ARCHITECT — Structure Advisor
  → suggests topics, variables, triggers, entities (per MS docs)
  → proceeds directly, no clarification needed
        ↓
  [Output: output/agent-name/ with 3 files]
```

## Project Structure

```
FORGE/
├── agents/                      ← agent prompts
│   ├── forgemaster.md           ← orchestrator (start here)
│   ├── instructor.md            ← generates system prompts
│   ├── descriptor.md            ← generates descriptions
│   └── architect.md             ← generates structure/config
│
├── templates/                   ← reusable base templates
│   ├── template-instructions.md
│   ├── template-description.md
│   └── template-structure.md
│
├── examples/                    ← real agents already built
│   ├── it-agent/               ← conversational IT helpdesk
│   ├── hr-agent/               ← conversational HR support
│   └── d365-variance-agent/    ← tool-only D365 agent (no prompt, no description)
│
└── output/                      ← agents generated with FORGE
    └── [agent-name]/
        ├── instructions.md
        ├── description.md
        └── structure.md
```

## How to Use

1. Open `agents/forgemaster.md` in GitHub Copilot
2. Tell it what agent you need (name, scope, sector, tone, topics)
3. FORGEMASTER handles everything:
   - **Phase 0** — Collects your input and confirms it in a summary table
   - **Phase 0.5** — Asks mandatory clarifying questions if anything is vague (instructions & description only)
   - **Phase 1** — Calls INSTRUCTOR → generates system prompt
   - **Phase 2** — Calls DESCRIPTOR → generates name and descriptions
   - **Phase 3** — Calls ARCHITECT → generates topics, variables, entities
   - **Phase 4** — Creates `output/[agent-name]/` folder with all 3 files and delivers summary
4. Review the generated package and deploy to Copilot Studio

### Clarification Rules
- INSTRUCTOR and DESCRIPTOR **must** ask questions when input is unclear — this is not optional
- Max 3-5 questions per round, with examples of good answers
- If you say "just do it", they proceed but **declare the defaults chosen**
- ARCHITECT proceeds without questions
