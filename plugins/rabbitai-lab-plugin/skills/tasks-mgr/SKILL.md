---
name: tasks-mgr
description: Manage tasks in RabbitAI Lab - create, update, delete, and list tasks within projects
version: 1.0.0
---

# Tasks Manager

Manage tasks in RabbitAI Lab.

## When to Use

- User wants to create, view, update, or delete tasks
- User wants to list tasks in a project
- User wants to change task status or priority
- User wants to assign a task to a project or requirement

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_tasks** - List tasks, optionally filtered by project or category
- **get_task** - Get a single task by ID
- **create_task** - Create a new task
- **update_task** - Update task details
- **delete_task** - Delete a task

## Guidelines

- Task status values: `TODO` -> `IN_PROGRESS` -> `DONE`
- Task priority values: `LOW`, `MEDIUM`, `HIGH`
- A task can be linked to a project (`projectId`) and/or a requirement (`requirementId`).
- When the user says "mark as done" or "complete task", set `status` to `DONE`.
- When the user says "start working on task", set `status` to `IN_PROGRESS`.
- If the user doesn't specify a project, you may need to `list_projects` first to find the right one.

## Workflow

1. To view tasks: call `list_tasks` with `projectId` to filter.
2. To create a task: at minimum provide `title`; include `projectId` if the user specifies a project.
3. To update status: call `update_task` with only `id` and `status`.
