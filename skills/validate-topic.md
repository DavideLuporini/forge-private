# Skill: Validate Topic

## Purpose
Validate a Copilot Studio topic YAML file against the official schema and best practices.

## When to use
- After TOPICSMITH generates a topic
- When reviewing existing topic YAML
- Before importing into Copilot Studio

## Validation layers

### Layer 1 — Schema compliance
- Root `kind` must be `AdaptiveDialog`
- All action `kind` values must exist in `reference/bot.schema.yaml-authoring.json`
- Required properties present for each kind
- Correct YAML syntax

### Layer 2 — Structural integrity
- Every action has a unique `id`
- No orphan actions (unreachable code)
- All conditional branches have actions
- All paths end with `EndDialog` or `EndConversation`
- No infinite loops in `BeginDialog` redirects

### Layer 3 — Variable consistency
- All referenced `Topic.*` variables are either:
  - Set via `SetVariable` before use, OR
  - Declared in `inputType`, OR
  - Set by a `Question` action, OR
  - Set by flow/HTTP output binding
- No unused variables (declared but never referenced)
- System variables use correct names

### Layer 4 — Best practices
- At least 5 trigger phrases per OnRecognizedIntent
- Trigger phrases are diverse (not minor variations)
- User-facing messages are clear and helpful
- Error handling exists for flow/HTTP calls
- Sensitive operations have confirmation steps

## Output format
```
## Validation Report: [topic-name]

### Schema: [PASS/FAIL]
- [details]

### Structure: [PASS/FAIL]
- [details]

### Variables: [PASS/FAIL]
- [details]

### Best Practices: [PASS/WARNINGS]
- [details]

### Overall: [READY / NEEDS FIXES]
```
