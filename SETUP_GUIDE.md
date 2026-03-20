# FORGE — Setup Guide

## Prerequisites
- GitHub Copilot with agent mode enabled (Business/Enterprise)
- Access to Microsoft Copilot Studio
- Git installed

## Quick Start

### Step 1 — Clone the repository
```bash
git clone https://github.com/DavideLuporini/forge-private.git FORGE
cd FORGE
```

### Step 2 — Open in your IDE
Open the FORGE folder in VS Code or your preferred IDE with GitHub Copilot enabled.

### Step 3 — Start FORGEMASTER
Open `agents/forgemaster.md` and use it as context for GitHub Copilot in agent mode.

Tell Copilot something like:
> "I need a new Copilot Studio agent for [purpose]. Use FORGEMASTER to build it."

### Step 4 — Follow the flow
FORGEMASTER will:
1. Ask for your requirements
2. Ask clarifying questions (mandatory for instructions & description)
3. Generate instructions via INSTRUCTOR
4. Generate description via DESCRIPTOR
5. Generate structure via ARCHITECT
6. Generate topic YAML files via TOPICSMITH
7. Save everything to `output/[agent-name]/`

### Step 5 — Deploy to Copilot Studio
1. Open Copilot Studio
2. Create a new agent
3. Paste the generated instructions into the system prompt
4. Use the description for the agent card
5. Import topic YAML files via the code editor or VS Code extension

## Project Structure

```
FORGE/
├── agents/           ← The 5 FORGE agents (start with forgemaster.md)
├── templates/        ← Base templates for generation
├── skills/           ← Skill definitions (capabilities reference)
├── reference/        ← Microsoft schemas, templates, best practices
│   ├── bot.schema.yaml-authoring.json    ← Official YAML schema
│   ├── adaptive-card.schema.json         ← Adaptive Card schema
│   ├── ms-templates/                     ← Official MS topic/agent templates
│   ├── ms-skills/                        ← Official MS skill definitions
│   └── best-practices/                   ← MS best practices guides
├── examples/         ← Real agent examples (IT, HR, D365)
└── output/           ← Generated agent packages
```

## Tips
- The more context you give FORGEMASTER, the better the output
- Always review generated YAML before importing into Copilot Studio
- Power Automate flow IDs are placeholders — replace them with real IDs
- Check `reference/best-practices/` for advanced patterns
