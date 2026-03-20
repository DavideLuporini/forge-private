# Skill: Edit Instructions

## Purpose
Guide for writing effective Copilot Studio agent instructions (system prompts).

## Structure
Every instruction set should follow the FORGE template structure:

1. **Core Identity** — Who the agent is, personality, role
2. **Context Handling** — What info is available, what to use/avoid
3. **Boundaries & Guardrails** — What the agent must NOT do
4. **When Unsure** — How to handle ambiguity
5. **When to Hand Off** — Escalation criteria
6. **Emotional Intelligence** — How to handle user emotions
7. **Formatting Rules** — Output style constraints

## Best practices
- Keep instructions under 8000 characters (Copilot Studio limit)
- Use imperative voice ("You are...", "Always...", "Never...")
- Be specific about boundaries — vague limits get ignored
- Include examples of good/bad responses where possible
- Test with adversarial prompts to verify guardrails hold

## Reference
See `templates/template-instructions.md` for the full template.
See `reference/ms-skills/instructions-guide.md` for Microsoft's guide.
