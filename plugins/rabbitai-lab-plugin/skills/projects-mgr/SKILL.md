---
name: projects-mgr
description: Manage projects in RabbitAI Lab - create, update, delete, and list projects within workspaces
version: 1.0.0
---

# Projects Manager

Manage projects in RabbitAI Lab.

## When to Use

- User wants to create, view, update, or delete projects
- User wants to list projects in a workspace or across all workspaces
- User wants to check project info or task counts

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_projects** - List projects with task counts, optionally filtered by workspace
- **get_project** - Get a single project by ID
- **create_project** - Create a new project in a workspace
- **update_project** - Update project details (name, description, status, color, dates)
- **delete_project** - Delete a project

## Guidelines

- Creating a project requires a `workspaceId` — if the user doesn't specify one, list their workspaces first and ask them to choose.
- Project status can be: `ACTIVE`, `ARCHIVED`, `COMPLETED`.
- When listing projects, note that `workspaceId` is optional. Without it, projects from all user workspaces are returned.
- Before deleting a project, confirm with the user since this is a destructive action.

## Workflow

1. To create a project: first determine the target workspace via `list_workspaces`, then call `create_project`.
2. To view projects: call `list_projects` with optional `workspaceId` filter.
3. To update a project: call `update_project` with only the fields that need to change.
