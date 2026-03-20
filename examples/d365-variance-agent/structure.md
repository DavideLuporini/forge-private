# D365 Variance Agent — Structure

## Agent Type
Tool-only agent — no system prompt, no description. All logic lives in custom tools (AdaptiveDialogs) that call Power Automate flows.

---

## Custom Tools

### 1. Analyze Variance
- **Type:** AdaptiveDialog
- **Trigger:** User provides a Configuration Id
- **Model description:** "Performs variance analysis using given configuration id"

#### Inputs
| Name | Type | Source | Prompted |
|------|------|--------|----------|
| ConfigurationId | String | User input | Yes — automatic prompt |
| AgentName | String | Topic variable | No |
| TemplateId | String | Topic variable | No |
| AgentConfiguration | String | Topic variable | No |

#### Flow sequence
1. Display configuration id confirmation
2. **Flow 1** — Retrieve configuration details (returns AgentConfiguration, AgentName, TemplateId)
3. **Flow 2** — Check source folder (returns ErrorMessage, ListOfFiles, State)
4. **Condition** — If State = false → show error, end dialog
5. Split ListOfFiles by ";" into ArrayOfFiles
6. **Foreach** file in ArrayOfFiles → **Flow 3** — Process individual file for variance detection
7. End conversation

#### Power Automate Flows
| Step | Flow ID | Purpose |
|------|---------|---------|
| Retrieve config | `b1ab4379-2490-f011-b41b-6045bd087bf6` | Get agent config, name, template |
| Check source | `ffe89153-2490-f011-b41b-6045bd087bf6` | Validate source folder, list files |
| Process file | `7a34665d-2490-f011-b41b-0022480ac28b` | Run variance analysis per file |

---

### 2. Reconcile Data
- **Type:** AdaptiveDialog
- **Trigger:** User provides a Configuration Id
- **Model description:** "This tool can handle the reconciliation agent with given Configuration Id"

#### Inputs
| Name | Type | Source | Prompted |
|------|------|--------|----------|
| CongfigurationId | String | User input | Yes — automatic prompt |

> **Note:** The input is misspelled as "CongfigurationId" (missing "i") in the original. This is carried over from the source YAML.

#### Flow sequence
1. Display configuration id confirmation
2. **Flow 1** — Retrieve configuration details (returns AgentConfiguration, AgentName, ReconciliationTemplateId)
3. **Flow 2** — Check source folder (returns ErrorMessage, FilesCount, ListOfFiles, State)
4. **Condition** — If State = false → show error, end dialog. Else → show success.
5. **Flow 3** — Execute reconciliation (returns CurrentlyExecutedStep, ErrorMessage, State)

#### Power Automate Flows
| Step | Flow ID | Purpose |
|------|---------|---------|
| Retrieve config | `cb182bd5-f8fd-ef11-bae3-00224820a45b` | Get agent config, name, template |
| Check source | `6e8fe52f-0001-f011-bae3-6045bdfa083c` | Validate source folder, list files |
| Reconcile | `de973914-0101-f011-bae3-6045bdfa083c` | Execute reconciliation process |

---

## Topic Variables Used
| Variable | Used By | Description |
|----------|---------|-------------|
| Topic.ConfigurationId | Analyze variance | User-provided config ID |
| Topic.CongfigurationId | Reconcile data | User-provided config ID (misspelled) |
| Topic.AgentConfiguration | Both | Retrieved agent configuration |
| Topic.AgentName | Both | Retrieved agent name |
| Topic.TemplateId | Analyze variance | Variance analysis template |
| Topic.ReconciliationTemplateId | Reconcile data | Reconciliation template |
| Topic.ListOfFiles | Both | Semicolon-separated file list |
| Topic.ArrayOfFiles | Analyze variance | Split array from ListOfFiles |
| Topic.State | Both | Success/failure flag |
| Topic.ErrorMessage | Both | Error message from flows |
| Topic.FilesCount | Reconcile data | Number of files found |
| Topic.CurrentlyExecutedStep | Reconcile data | Progress tracking |

## System Variables Used
| Variable | Purpose |
|----------|---------|
| System.Conversation.Id | Passed to all flows for session tracking |
| System.User.Email | Passed to all flows for user identification |

---

## Architecture Pattern
```
User says "analyze variance" or "reconcile data"
        ↓
Copilot Studio recognizes intent → routes to correct tool
        ↓
Tool prompts for Configuration Id
        ↓
Flow 1: Retrieve config from D365
        ↓
Flow 2: Validate source folder
        ↓
Condition: valid?
  ├─ No → Error message → End
  └─ Yes → Flow 3: Execute process
        ↓
End conversation
```

## Key Observations
1. **No generative AI needed** — This agent is deterministic, not conversational
2. **All logic in Power Automate** — The AdaptiveDialogs are just orchestration wrappers
3. **Single input pattern** — Both tools only need a Configuration Id from the user
4. **Error handling** — Both tools check State flag before proceeding
5. **Typo in source** — "CongfigurationId" should be "ConfigurationId" in Reconcile data
