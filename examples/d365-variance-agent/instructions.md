# D365 Variance Agent — Instructions

> **NOTE:** This agent has NO system prompt / instructions.
> It operates entirely through custom tools (AdaptiveDialogs) that invoke Power Automate flows.
> The orchestration logic is embedded in the tool definitions themselves.

This is a valid pattern in Copilot Studio when the agent:
- Does not need conversational guidance
- Is purely task-driven (trigger → execute → respond)
- Delegates all logic to Power Automate flows
- Has no ambiguity in user intent (structured inputs only)
