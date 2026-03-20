# FORGE Reference

This folder contains official Microsoft schemas, templates, and documentation
used by FORGE agents (especially TOPICSMITH) to generate valid Copilot Studio configurations.

## Contents

### Schemas
- `bot.schema.yaml-authoring.json` — The master YAML schema for Copilot Studio
- `adaptive-card.schema.json` — Adaptive Card JSON schema

### MS Templates (`ms-templates/`)
Official YAML templates from microsoft/skills-for-copilot-studio:
- `topics/` — 11 topic templates (greeting, fallback, Q&A, search, auth, etc.)
- `agents/` — Agent and child-agent templates
- `actions/` — Connector action template
- `knowledge/` — Knowledge source templates (website, SharePoint)

### MS Skills (`ms-skills/`)
Official skill definitions from Microsoft — reference for how to author
topics, actions, triggers, and agent instructions.

### Best Practices (`best-practices/`)
Microsoft's recommended patterns:
- JIT glossary injection
- User context handling
- Date context
- Orchestrator variables
- Topic redirect with variables
- Preventing child agent responses

## Source
All reference files sourced from:
https://github.com/microsoft/skills-for-copilot-studio
