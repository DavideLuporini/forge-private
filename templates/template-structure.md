# Template: Agent Structure (Topics, Variables, Triggers)

Use this template to plan the Copilot Studio configuration for a new agent.
Based on Microsoft Copilot Studio documentation.

---

## Topics

Topics are conversation flows that the agent can handle.
Each topic has: a name, trigger phrases, and a conversation flow.

### System Topics (built-in, always present)
- Greeting — first message when user opens chat
- Escalate — hand off to human agent
- End of Conversation — wrap-up and satisfaction survey
- Fallback — when no topic matches
- Multiple Topics Matched — disambiguation

### Custom Topics Template

| Topic Name | Description | Trigger Phrases (5-10 per topic) | Ends With |
|---|---|---|---|
| [TOPIC_1] | [What this topic handles] | [phrase1, phrase2, phrase3...] | [Resolution / Escalation / Follow-up] |
| [TOPIC_2] | [What this topic handles] | [phrase1, phrase2, phrase3...] | [Resolution / Escalation / Follow-up] |

---

## Global Variables

Variables that persist across the entire session.

| Variable Name | Type | Source | Description |
|---|---|---|---|
| UserName | String | user_profile | Employee's display name |
| UserCountry | String | user_profile | Employee's country for localized answers |
| UserJobTitle | String | user_profile | Employee's role for personalized guidance |
| EscalationReason | String | Set by agent | Why the conversation was escalated |
| [CUSTOM_VAR] | [Type] | [Source] | [Description] |

---

## Topic Variables (per-topic, session-scoped)

| Variable Name | Used In Topic | Type | Description |
|---|---|---|---|
| [VAR_NAME] | [TOPIC_NAME] | [Type] | [Description] |

---

## Entities

Custom entities for recognizing domain-specific terms.

| Entity Name | Type | Values / Pattern | Used In |
|---|---|---|---|
| [ENTITY_1] | Closed list / Regex / Prebuilt | [values or pattern] | [Which topics use it] |

---

## Knowledge Sources

| Source Name | Type | URL / Location | Description |
|---|---|---|---|
| [SOURCE_1] | SharePoint / Website / File | [path or URL] | [What info it contains] |

---

## Suggested Connections

| Connection | Purpose | Microsoft Docs Reference |
|---|---|---|
| Power Automate flows | Trigger actions (create tickets, send emails) | [Use flows in Copilot Studio] |
| Dataverse | Store/retrieve structured data | [Use Dataverse in Copilot Studio] |
| SharePoint | Knowledge base for generative answers | [Add knowledge sources] |
| Azure AD / Entra ID | User profile enrichment | [Authentication in Copilot Studio] |
| ServiceNow / Jira | Ticket creation and status lookup | [Use connectors] |

---

## Example: IT Agent Structure

### Topics
| Topic | Triggers | Ends With |
|---|---|---|
| Password Reset | "reset password", "forgot password", "can't log in", "locked out" | Resolution |
| VPN Issues | "VPN not working", "can't connect to VPN", "remote access" | Resolution / Escalation |
| Software Install | "install software", "need an app", "request application" | Resolution |
| Hardware Issue | "broken laptop", "screen cracked", "keyboard not working" | Escalation |
| Security Incident | "phishing email", "suspicious link", "hacked", "data breach" | Escalation |

### Entities
| Entity | Type | Values |
|---|---|---|
| SoftwareList | Closed list | Teams, Outlook, Office 365, Slack, Zoom, VS Code, SAP |
| DeviceType | Closed list | Laptop, Desktop, Monitor, Keyboard, Mouse, Headset |

---

## Example: HR Agent Structure

### Topics
| Topic | Triggers | Ends With |
|---|---|---|
| Leave Policy | "how many days off", "vacation policy", "sick leave", "parental leave" | Resolution |
| Benefits | "health insurance", "benefits enrollment", "dental plan", "pension" | Resolution |
| Onboarding | "first day", "new hire", "onboarding checklist", "welcome" | Resolution |
| Payroll | "payslip", "salary", "pay date", "tax forms" | Resolution / Escalation |
| Complaint | "file complaint", "harassment", "grievance", "hostile environment" | Escalation |

### Entities
| Entity | Type | Values |
|---|---|---|
| LeaveType | Closed list | Annual, Sick, Parental, Bereavement, Unpaid, Sabbatical |
| BenefitPlan | Closed list | Health, Dental, Vision, Life Insurance, Pension, Wellness |
