# Copilot Studio YAML — Kind Reference

Quick reference of all known `kind` values for Copilot Studio topic YAML.

## Root
| Kind | Description |
|------|-------------|
| `AdaptiveDialog` | Root element for every topic |

## Triggers (in `beginDialog`)
| Kind | Description |
|------|-------------|
| `OnRecognizedIntent` | User input matches trigger phrases |
| `OnUnknownIntent` | No intent matched (fallback) |
| `OnConversationStart` | New conversation begins |
| `OnSelectIntent` | Multiple topics matched (disambiguation) |
| `OnRedirect` | Topic redirect target |
| `OnSignIn` | Sign-in event |
| `OnError` | Error/exception |
| `OnEventActivity` | Named event activity |

## Actions (in `actions` arrays)
| Kind | Description |
|------|-------------|
| `SendActivity` | Send message (text, speak, attachments) |
| `SendMessage` | Send simple text message |
| `Question` | Ask user question, store response |
| `ConditionGroup` | If/else branching |
| `SetVariable` | Set variable value |
| `BeginDialog` | Redirect to another topic |
| `EndDialog` | End current topic |
| `EndConversation` | End entire conversation |
| `InvokeFlowAction` | Call Power Automate flow |
| `HttpRequestAction` | HTTP request |
| `Foreach` | Loop over collection |
| `SearchAndSummarizeContent` | Generative answers |
| `CreateSearchQuery` | Optimize search query |
| `ParseValue` | Parse JSON/value |
| `GotoAction` | Jump to action by ID |
| `EditTable` | Modify table data |
| `OAuthInput` | OAuth login dialog |
| `LogCustomTelemetryEvent` | Log telemetry |
| `ReplaceDialog` | Replace current dialog |
| `CancelAllDialogs` | Cancel all dialogs |

## Inputs
| Kind | Description |
|------|-------------|
| `AutomaticTaskInput` | Automatic input parameter |
| `ManualTaskInput` | Manual/hardcoded input |

## Entities
| Kind | Description |
|------|-------------|
| `EmbeddedEntity` | Inline entity |
| `ClosedListEntity` | Predefined choice list |

## Prebuilt Entities (used with `entity:` property)
- `StringPrebuiltEntity`
- `BooleanPrebuiltEntity`
- `NumberPrebuiltEntity`
- `StatePrebuiltEntity`
- `EmailPrebuiltEntity`
- `DateTimePrebuiltEntity`
- `PersonNamePrebuiltEntity`

## Cards
| Kind | Description |
|------|-------------|
| `AdaptiveCardTemplate` | Render Adaptive Card |

## Variable Prefixes
| Prefix | Scope |
|--------|-------|
| `Topic.` | Current topic |
| `Global.` | Global (across topics) |
| `System.` | System-provided |
| `Environment.` | Environment variables |

## Common System Variables
| Variable | Description |
|----------|-------------|
| `System.Activity.Text` | User's current message |
| `System.User.Email` | User email |
| `System.User.DisplayName` | User display name |
| `System.Conversation.Id` | Conversation ID |
| `System.Bot.Name` | Agent name |

## Power Fx
- Prefix with `=` in YAML
- Example: `condition: =Topic.Choice = "Yes"`
- Example: `value: =Concatenate(Topic.First, " ", Topic.Last)`
- Example: `condition: =!IsBlank(Topic.Answer)`
