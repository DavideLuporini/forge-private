# FORGE — Framework for Orchestrated Agent Generation Engine

Multi-agent system for generating Copilot Studio agent configurations.

## Architecture

```
[Input: agent name + scope + sector]
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
  [Output: agent-ready package]
```

## Project Structure

```
FORGE/
├── templates/                   ← reusable base templates
│   ├── template-instructions.md
│   ├── template-description.md
│   └── template-structure.md
│
├── agents/                      ← the 3 builder agent prompts
│   ├── instructor.md
│   ├── descriptor.md
│   └── architect.md
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

### Step 1 — Generate Instructions
Open `agents/instructor.md` in GitHub Copilot.
Provide: agent name, scope, sector, tone.
Save output to `output/[agent-name]/instructions.md`.

### Step 2 — Generate Description
Open `agents/descriptor.md` in GitHub Copilot.
Attach the instructions.md from Step 1.
Save output to `output/[agent-name]/description.md`.

### Step 3 — Generate Structure
Open `agents/architect.md` in GitHub Copilot.
Attach both previous outputs.
Save output to `output/[agent-name]/structure.md`.
