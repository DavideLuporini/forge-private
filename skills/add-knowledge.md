# Skill: Add Knowledge Source

## Purpose
Add a knowledge source to a Copilot Studio agent for generative answers.

## Knowledge source types

### Public Website
```yaml
kind: PublicSiteSearchSource
siteName: "_REPLACE_SITE_NAME"
siteUrl: "_REPLACE_URL"
```
Use when: The agent should search a public website for answers.

### SharePoint
```yaml
kind: SharePointSearchSource
siteName: "_REPLACE_SITE_NAME"
siteUrl: "_REPLACE_SHAREPOINT_URL"
```
Use when: The agent should search internal SharePoint sites.

## Where to save
Knowledge files go in: `output/[agent-name]/knowledge/[name].knowledge.mcs.yml`

## Templates
See `reference/ms-templates/knowledge/` for full templates.
