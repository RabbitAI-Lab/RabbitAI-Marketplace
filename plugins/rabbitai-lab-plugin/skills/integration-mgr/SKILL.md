---
name: integration-mgr
description: Manage third-party integrations and chat group bindings for projects in RabbitAI Lab
version: 1.0.0
---

# Integration Manager

Manage third-party integrations and chat group bindings for projects in RabbitAI Lab.

## When to Use

- User wants to view third-party integration configurations for a project
- User wants to bind a chat group (Slack, Discord, WeCom, DingTalk, etc.) to a project
- User wants to update or remove chat group bindings

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

### Integrations

- **list_project_integrations** - List integration configs for a project, optionally filtered by type

### Chat Groups

- **list_project_chat_groups** - List chat group bindings, optionally filtered by project
- **get_project_chat_group** - Get a chat group binding by ID
- **create_project_chat_group** - Bind a new chat group to a project
- **update_project_chat_group** - Update a chat group binding
- **delete_project_chat_group** - Remove a chat group binding

## Guidelines

- `list_project_integrations` returns full authorization info (API keys, tokens) — handle sensitively.
- When binding a chat group, the `type` field identifies the platform (e.g., slack, discord, wecom, dingtalk).
- `chatId` is the external chat group ID from the third-party platform, not a RabbitAI ID.
- Integration responses may contain sensitive credentials — avoid exposing them in responses unless the user specifically asks.

## Workflow

1. To check integrations: call `list_project_integrations` with the project ID.
2. To connect a chat group: call `create_project_chat_group` with the project ID, platform type, and external chat ID.
3. To update a chat group name: call `update_project_chat_group` with the binding ID and new name.
