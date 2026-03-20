# FORGE Skills

Skills are atomic capability definitions that FORGE agents use as reference.
Each skill describes a specific task with steps, patterns, and validation rules.

## Available Skills

| Skill | Purpose | Used by |
|-------|---------|---------|
| `new-topic.md` | Create a new topic YAML from scratch | TOPICSMITH |
| `validate-topic.md` | Validate topic YAML against schema | TOPICSMITH |
| `add-adaptive-card.md` | Add rich UI cards to topics | TOPICSMITH |
| `add-knowledge.md` | Add knowledge sources to agents | ARCHITECT |
| `edit-instructions.md` | Guide for writing system prompts | INSTRUCTOR |

## How skills work
Skills are not executed directly. They are reference documents that agents read
to understand HOW to perform a specific task. Think of them as "procedure manuals"
for AI agents.
