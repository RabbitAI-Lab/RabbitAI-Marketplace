---
name: ai-settings
description: Configure AI automation settings for projects in RabbitAI Lab
version: 1.0.0
---

# AI Settings Manager

Configure AI automation settings for projects in RabbitAI Lab.

## When to Use

- User wants to view or change AI automation behavior for a project
- User wants to enable/disable auto admission, plan alignment, task design, or testing
- User wants to configure manual intervention points in AI workflows

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **get_project_ai_settings** - View current AI settings for a project
- **update_project_ai_settings** - Update AI settings (only fields provided will be changed)

## Guidelines

- `update_project_ai_settings` is a **partial update** — only include the fields you want to change; omitted fields remain unchanged.
- The AI pipeline flow is: requirement admission -> plan alignment -> task design -> testing.
- Key automation toggles:
  - `autoRequirementAdmission` - Requirements auto-pass admission
  - `autoStartPlanAlignment` / `autoPlanAlignmentApproval` - Plan alignment auto-start and auto-approve
  - `autoStartTaskDesign` / `autoTaskDesignAdmission` - Task design auto-start and auto-approve
  - `autoUiTest` / `autoGenerateApiTests` / `autoApiTest` - Test automation
- Manual intervention: set `allowManualIntervention` to true, then specify `manualInterventionNodes` (`requirement`, `test`, `task`, `bug`).

## Workflow

1. To review settings: call `get_project_ai_settings` with the project ID.
2. To change settings: call `update_project_ai_settings` with only the fields to modify.
3. If the user says "enable full automation", set all auto-* fields to true and disable manual intervention.
4. If the user says "I want to review requirements manually", set `allowManualIntervention: true` and include `requirement` in `manualInterventionNodes`.
