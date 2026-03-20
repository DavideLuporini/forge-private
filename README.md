# FORGE — Framework for Orchestrated Agent Generation Engine

Multi-agent system for generating Copilot Studio agent configurations.

## Architecture

```
[You provide: agent name + scope + sector + tone]
        ↓
  FORGEMASTER — Orchestrator
  → collects input, coordinates all agents, delivers the package
        ↓
  INSTRUCTOR — Instructions Generator
  → generates the complete system prompt
        ↓
  DESCRIPTOR — Description Generator
  → generates display name + short/long descriptions
        ↓
  ARCHITECT — Structure Advisor
  → suggests topics, variables, triggers, entities (per MS docs)
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
│   ├── it-agent/
│   └── hr-agent/
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
   - Calls INSTRUCTOR → generates system prompt
   - Calls DESCRIPTOR → generates name and descriptions
   - Calls ARCHITECT → generates topics, variables, entities
   - Creates `output/[agent-name]/` folder with all 3 files
4. Review the generated package and deploy to Copilot Studio
