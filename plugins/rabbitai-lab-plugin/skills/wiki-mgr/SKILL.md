---
name: wiki-mgr
description: Manage wiki documents in RabbitAI Lab
version: 1.0.0
---

# Wiki Manager

Manage wiki documents in RabbitAI Lab.

## When to Use

- User wants to create, view, update, or delete wiki documents
- User wants to write or edit project documentation
- User wants to list all wiki pages in a project

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_wikis** - List wikis, optionally filtered by project
- **get_wiki** - Get a wiki by ID
- **create_wiki** - Create a new wiki (content supports markdown)
- **update_wiki** - Update wiki title or content
- **delete_wiki** - Delete a wiki

## Guidelines

- Wiki content is in **markdown format**. When creating or updating, format the content appropriately.
- Creating a wiki requires `title` and `projectId`.
- When the user provides raw text for wiki content, convert it to well-structured markdown before calling `create_wiki` or `update_wiki`.
- `list_wikis` without `projectId` returns wikis from all projects the user has access to.

## Workflow

1. To write documentation: determine the project, then call `create_wiki` with a title and markdown content.
2. To edit a wiki: first `get_wiki` to see current content, then `update_wiki` with changes.
3. To browse docs: call `list_wikis` with a project filter.
