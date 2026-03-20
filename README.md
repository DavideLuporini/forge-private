# FORGE — Framework for Orchestrated Agent Generation Engine

Multi-agent system for generating complete Microsoft Copilot Studio agent configurations — instructions, descriptions, structure, and topic YAML files.

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
  TOPICSMITH — Topic YAML Generator
  → generates production-ready .topic.mcs.yml files
  → uses official MS schema and templates as reference
        ↓
  [Output: output/agent-name/ with full package]
```

## Project Structure

```
FORGE/
├── agents/                          ← the 5 FORGE agents
│   ├── forgemaster.md               ← orchestrator (start here)
│   ├── instructor.md                ← generates system prompts
│   ├── descriptor.md                ← generates descriptions
│   ├── architect.md                 ← generates structure/config
│   └── topicsmith.md                ← generates topic YAML files
│
├── templates/                       ← reusable base templates
│   ├── template-instructions.md
│   ├── template-description.md
│   └── template-structure.md
│
├── skills/                          ← skill definitions (capability reference)
│   ├── new-topic.md                 ← create topic YAML from scratch
│   ├── validate-topic.md            ← validate YAML against schema
│   ├── add-adaptive-card.md         ← add rich UI cards
│   ├── add-knowledge.md             ← add knowledge sources
│   └── edit-instructions.md         ← guide for writing system prompts
│
├── reference/                       ← official Microsoft schemas & docs
│   ├── bot.schema.yaml-authoring.json   ← master YAML schema
│   ├── adaptive-card.schema.json        ← Adaptive Card schema
│   ├── kind-reference.md                ← quick reference of all kind values
│   ├── ms-templates/                    ← official MS YAML templates
│   │   ├── topics/                      ← 11 topic templates
│   │   ├── agents/                      ← agent & child-agent templates
│   │   ├── actions/                     ← connector action template
│   │   └── knowledge/                   ← knowledge source templates
│   ├── ms-skills/                       ← official MS skill definitions
│   │   ├── new-topic.md
│   │   ├── add-action.md
│   │   ├── add-adaptive-card.md
│   │   ├── card-templates.md
│   │   ├── add-generative-answers.md
│   │   ├── generative-answers-patterns.md
│   │   ├── generative-answers-property-reference.md
│   │   ├── edit-agent.md
│   │   ├── instructions-guide.md
│   │   ├── validate.md
│   │   ├── add-node.md
│   │   ├── edit-triggers.md
│   │   ├── add-knowledge.md
│   │   ├── add-global-variable.md
│   │   └── list-kinds.md
│   └── best-practices/                 ← MS recommended patterns
│       ├── best-practices.md
│       ├── jit-glossary.md
│       ├── jit-user-context.md
│       ├── date-context.md
│       ├── orchestrator-variables.md
│       ├── prevent-child-agent-responses.md
│       └── topic-redirect-with-variable.md
│
├── examples/                        ← real agents already built
│   ├── it-agent/                    ← conversational IT helpdesk
│   ├── hr-agent/                    ← conversational HR support
│   └── d365-variance-agent/         ← tool-only D365 agent (no prompt)
│
├── output/                          ← agents generated with FORGE
│   └── [agent-name]/
│       ├── instructions.md
│       ├── description.md
│       ├── structure.md
│       └── topics/
│           ├── [topic-1].topic.mcs.yml
│           └── [topic-2].topic.mcs.yml
│
├── SETUP_GUIDE.md                   ← how to install and use FORGE
├── .gitignore
└── README.md
```

## How to Use

1. Open `agents/forgemaster.md` in GitHub Copilot (agent mode)
2. Tell it what agent you need (name, scope, sector, tone, topics)
3. FORGEMASTER handles everything:
   - **Phase 0** — Collects your input and confirms it in a summary table
   - **Phase 0.5** — Asks mandatory clarifying questions if anything is vague (instructions & description only)
   - **Phase 1** — Calls INSTRUCTOR → generates system prompt
   - **Phase 2** — Calls DESCRIPTOR → generates name and descriptions
   - **Phase 3** — Calls ARCHITECT → generates topics, variables, entities
   - **Phase 4** — Calls TOPICSMITH → generates topic YAML files
   - **Phase 5** — Creates `output/[agent-name]/` folder with all files and delivers summary
4. Review the generated package and deploy to Copilot Studio

### Clarification Rules
- INSTRUCTOR and DESCRIPTOR **must** ask questions when input is unclear — this is not optional
- Max 3-5 questions per round, with examples of good answers
- If you say "just do it", they proceed but **declare the defaults chosen**
- ARCHITECT and TOPICSMITH proceed without questions

## Reference Sources

All reference material in `reference/` is sourced from:
- [microsoft/skills-for-copilot-studio](https://github.com/microsoft/skills-for-copilot-studio)
- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)

## Examples

| Agent | Type | Has Instructions | Has Description | Has Topics |
|-------|------|:---:|:---:|:---:|
| IT Agent | Conversational | ✅ | ✅ | — |
| HR Agent | Conversational | ✅ | ✅ | — |
| D365 Variance | Tool-only | ❌ | ❌ | ✅ (YAML) |
