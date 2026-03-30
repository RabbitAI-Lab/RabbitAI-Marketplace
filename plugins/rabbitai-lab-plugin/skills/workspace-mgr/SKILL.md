---
name: workspace-mgr
description: Manage workspaces, members, invite links, data import/export, and approvals in RabbitAI Lab
version: 1.0.0
---

# Workspace Manager

Manage workspaces in RabbitAI Lab. This skill covers workspace CRUD, member management, invite links, data import/export, and approval workflows.

## When to Use

- User wants to create, view, update, or delete a workspace
- User wants to manage workspace members (invite, remove, transfer ownership)
- User wants to create or revoke invite links
- User wants to export or import workspace data
- User wants to list, approve, or reject approval requests

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

### Workspace

- **list_workspaces** - List all workspaces the user belongs to
- **get_workspace** - Get workspace details with project and member counts
- **create_workspace** - Create a new workspace
- **update_workspace** - Update workspace (owner only)
- **delete_workspace** - Delete a workspace (owner only)

### Members

- **get_members** - View members and pending invites
- **invite_member** - Invite by email (owner only)
- **remove_member** - Remove a member (owner only)
- **transfer_ownership** - Transfer ownership to another member (owner only)

### Invite Links

- **create_invite_link** - Generate a shareable invite link (owner only)
- **get_invite_links** - List active invite links (owner only)
- **revoke_invite_link** - Revoke an invite link (owner only)
- **join_by_code** - Join a workspace via invite code

### Data Import/Export

- **export_workspace** - Export all workspace data (owner only)
- **check_import_conflicts** - Check for conflicts before importing (owner only)
- **import_workspace** - Import data from a previous export (owner only)

### Approvals

- **list_approvals** - List approvals, filterable by status (`PENDING`, `APPROVED`, `REJECTED`, `CANCELLED`) and type (`FILE_OPERATION`, `SYSTEM_CONFIG`, `DATA_EXPORT`, `EXTERNAL_ACTION`, `OTHER`)
- **approve_approval** - Approve a pending request
- **reject_approval** - Reject a pending request (`rejectReason` is required)

## Guidelines

- Operations marked "owner only" require the current user to be the workspace owner. If a non-owner tries, the API will reject the request.
- Before importing data, always call `check_import_conflicts` first to detect potential issues.
- `export_workspace` can export specific projects via `projectIds`, or all projects if omitted.

## Workflow

1. **Onboarding**: `create_workspace` -> `invite_member` or `create_invite_link`.
2. **Data migration**: `export_workspace` from source -> `check_import_conflicts` on target -> `import_workspace`.
3. **Approvals**: `list_approvals` with `status: "PENDING"` -> `approve_approval` or `reject_approval`.
