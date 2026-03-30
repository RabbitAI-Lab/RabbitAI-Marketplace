---
name: bugs-mgr
description: Manage bugs in RabbitAI Lab - report, track, update, and search bugs
version: 1.0.0
---

# Bugs Manager

Manage bugs in RabbitAI Lab.

## When to Use

- User wants to report a new bug
- User wants to list, view, or search bugs in a project
- User wants to update bug status or severity
- User wants to filter bugs by requirement or task

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_bugs** - List bugs with pagination and keyword search; can filter by requirement or task
- **get_bug** - Get a single bug by ID
- **create_bug** - Report a new bug (supports linking to requirement and task)
- **update_bug** - Update bug details
- **delete_bug** - Delete a bug

## Guidelines

- Bug status lifecycle: `NEW` -> `FIXING` -> `FIXED` -> `CLOSED`. Bugs can also be `NOT_REPRODUCIBLE` or `REOPENED`.
- Bug severity: `MINOR`, `MAJOR`, `CRITICAL`, `FATAL`.
- `list_bugs` requires `projectId` — always determine the project first.
- When reporting a bug, encourage the user to provide: title, description (reproduction steps), expected result, and current behavior.
- When the user says "this bug is fixed", set `status` to `FIXED`.
- When the user says "this bug happened again", set `status` to `REOPENED`.

## Workflow

1. To report a bug: gather title, project, and description from the user, then call `create_bug`.
2. To find bugs: call `list_bugs` with `projectId` and optional `keyword` for search.
3. To update progress: call `update_bug` with `id` and the new `status`.
