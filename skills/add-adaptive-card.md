# Skill: Add Adaptive Card

## Purpose
Add an Adaptive Card to a topic for rich UI interactions (forms, confirmations, info displays).

## When to use
- Topic needs structured form input
- Topic needs a confirmation dialog with buttons
- Topic needs to display formatted information

## Card patterns

### Pattern 1 — Info Card
Displays information with optional action buttons.
```json
{
  "type": "AdaptiveCard",
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.5",
  "body": [
    {
      "type": "TextBlock",
      "text": "_REPLACE_TITLE",
      "weight": "Bolder",
      "size": "Medium"
    },
    {
      "type": "TextBlock",
      "text": "_REPLACE_BODY",
      "wrap": true
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "_REPLACE_BUTTON_TEXT",
      "data": { "action": "_REPLACE_ACTION_VALUE" }
    }
  ]
}
```

### Pattern 2 — Form Card
Collects user input via form fields.
```json
{
  "type": "AdaptiveCard",
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.5",
  "body": [
    {
      "type": "TextBlock",
      "text": "_REPLACE_FORM_TITLE",
      "weight": "Bolder",
      "size": "Medium"
    },
    {
      "type": "Input.Text",
      "id": "_REPLACE_FIELD_ID",
      "label": "_REPLACE_FIELD_LABEL",
      "isRequired": true,
      "errorMessage": "_REPLACE_ERROR_MSG"
    },
    {
      "type": "Input.ChoiceSet",
      "id": "_REPLACE_CHOICE_ID",
      "label": "_REPLACE_CHOICE_LABEL",
      "choices": [
        { "title": "_REPLACE_OPTION_1", "value": "option1" },
        { "title": "_REPLACE_OPTION_2", "value": "option2" }
      ]
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Submit"
    }
  ]
}
```

### Pattern 3 — Confirmation Card
Yes/No confirmation before proceeding.
```json
{
  "type": "AdaptiveCard",
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.5",
  "body": [
    {
      "type": "TextBlock",
      "text": "_REPLACE_CONFIRMATION_TEXT",
      "wrap": true,
      "weight": "Bolder"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Yes",
      "data": { "confirmed": true }
    },
    {
      "type": "Action.Submit",
      "title": "No",
      "data": { "confirmed": false }
    }
  ]
}
```

## How to embed in topic YAML
```yaml
- kind: SendActivity
  id: sendActivity_XXXXXX
  activity:
    attachments:
      - kind: AdaptiveCardTemplate
        cardContent: |
          {PASTE_CARD_JSON_HERE}
```

## Schema reference
See `reference/adaptive-card.schema.json` for full Adaptive Card schema.
