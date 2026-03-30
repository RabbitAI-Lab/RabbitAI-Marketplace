---
name: requirements-mgr
description: Manage requirements and requirement categories in RabbitAI Lab
version: 1.0.0
---

# Requirements Manager

Manage requirements and requirement categories in RabbitAI Lab.

## When to Use

- User wants to create, view, update, or delete requirements
- User wants to manage requirement categories (create, update, delete, list)
- User wants to organize requirements by category

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

### Requirements

- **list_requirements** - List requirements for a project (`projectId` is required)
- **get_requirement** - Get a single requirement by ID
- **create_requirement** - Create a new requirement (supports documents, designers, deliverables as `{ name, url }` arrays)
- **update_requirement** - Update requirement details
- **delete_requirement** - Delete a requirement

### Requirement Categories

- **list_requirement_categories** - List categories for a project
- **get_requirement_category** - Get a category by ID
- **create_requirement_category** - Create a category (supports nesting via `parentId`)
- **update_requirement_category** - Update a category
- **delete_requirement_category** - Delete a category

## Guidelines

- Requirement status: `NOT_STARTED` -> `IN_PROGRESS` -> `COMPLETED`; also `TERMINATED` for cancelled ones.
- Requirement priority: `LOW`, `MEDIUM`, `HIGH`.
- `list_requirements` requires `projectId` — always ask or determine the project first.
- Categories support nesting via `parentId` for hierarchical organization.
- When creating a requirement, the user may provide `documents`, `designers`, and `deliverables` as arrays of `{ name, url }` objects.

## Workflow

1. To organize requirements: first create categories, then assign `categoryId` when creating requirements.
2. To view all requirements in a project: call `list_requirements` with the project ID.
3. To update a requirement's progress: call `update_requirement` with the new `status`.
