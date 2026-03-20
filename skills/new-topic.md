# Skill: New Topic

## Purpose
Create a new Copilot Studio topic YAML file from scratch.

## When to use
- TOPICSMITH needs to generate a topic that doesn't match any existing template
- User requests a custom topic type

## Steps
1. Determine the topic's purpose and trigger type
2. Select the closest template from `reference/ms-templates/topics/`
3. Customize the template:
   - Replace `_REPLACE` IDs with generated unique IDs
   - Set `modelDisplayName` and `modelDescription`
   - Add trigger phrases in `triggerQueries`
   - Build the action sequence
   - Declare input/output variables in `inputType`/`outputType`
4. Validate the YAML structure
5. Save to `output/[agent-name]/topics/[name].topic.mcs.yml`

## Template selection guide

| User need | Template | Key actions |
|-----------|----------|------------|
| Welcome message | greeting | SendActivity |
| Handle unknown input | fallback | SearchAndSummarizeContent or SendActivity |
| Ask questions with branching | question-topic | Question → ConditionGroup |
| Search knowledge base | search-topic | SearchAndSummarizeContent |
| Handle errors | error-handler | ConditionGroup → SendActivity |
| Require login | auth-topic | OAuthInput → ConditionGroup |
| Multiple matches | disambiguation | OnSelectIntent |
| Set session variables | conversation-init | OnConversationStart → SetVariable |

## Validation checklist
- [ ] `kind: AdaptiveDialog` at root
- [ ] `beginDialog` with valid trigger kind
- [ ] All actions have unique `id` values
- [ ] All variable references use correct prefix (Topic., Global., System.)
- [ ] All paths terminate with EndDialog or EndConversation
- [ ] Trigger phrases are natural and varied (min 5)
- [ ] modelDescription is clear and concise
