---
name: repos-mgr
description: Manage git repository bindings in RabbitAI Lab
version: 1.0.0
---

# Repositories Manager

Manage git repository bindings for projects in RabbitAI Lab.

## When to Use

- User wants to bind a git repository to a project
- User wants to list or view repositories linked to a project
- User wants to update repository settings (URL, branch, authentication)
- User wants to remove a repository binding

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_git_repositories** - List repositories for a project (includes auth info)
- **get_git_repository** - Get a repository by ID (includes auth info)
- **create_git_repository** - Bind a new repository with optional authentication
- **update_git_repository** - Update repository settings or auth config
- **delete_git_repository** - Remove a repository binding

## Guidelines

- `list_git_repositories` requires `projectId` — determine the project first.
- Authentication types (`authType`):
  - `NONE` - Public repository, no auth needed
  - `ACCESS_TOKEN` - Personal access token (GitHub, GitLab, etc.)
  - `SSH_KEY` - SSH key with optional passphrase
  - `BASIC` - Username and password
- When the user provides a private repo URL, ask which auth method to use and gather the necessary credentials.
- Repository responses include full authentication info — handle credentials sensitively and avoid displaying tokens/keys unless necessary.

## Workflow

1. To bind a repo: call `create_git_repository` with `name`, `url`, `projectId`, and optionally `authType` + `authConfig`.
2. To change branch: call `update_git_repository` with `id` and the new `branch`.
3. To rotate credentials: call `update_git_repository` with `id` and the new `authConfig`.
