# RabbitAI Marketplace

[中文文档](README_CN.md)

The official Claude Code plugin marketplace from RabbitAI Lab — connect to the RabbitAI Lab platform via MCP for a suite of AI-powered project management tools.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| **rabbitai-lab-plugin** | RabbitAI Lab official plugin — provides full management capabilities for workspaces, projects, requirements, tasks, bugs, tests, wikis, repositories, integrations, and AI settings |

### Included Skills

| Skill | Description |
|-------|-------------|
| **workspace-mgr** | Workspace management: create, update, delete workspaces; member management; invite links; data import/export; approval workflows |
| **projects-mgr** | Project management: create, view, update, and delete projects within workspaces |
| **requirements-mgr** | Requirements management: CRUD for requirements and categories with nested categorization and attachment links |
| **tasks-mgr** | Task management: create tasks, manage status transitions, and set priorities |
| **bugs-mgr** | Bug management: report, track, update status, and assess severity |
| **tests-mgr** | Test management: test case management with verification steps, browser scripts, and screenshots |
| **wiki-mgr** | Wiki management: create, edit, and browse Markdown-formatted project documentation |
| **repos-mgr** | Repository management: bind Git repositories with multiple auth methods (Token / SSH / Basic) |
| **integration-mgr** | Integration management: third-party integration configs, chat group bindings (Slack / Discord / WeCom / DingTalk, etc.) |
| **ai-settings** | AI settings: configure AI automation behavior including requirement admission, plan alignment, task design, and test automation |

## Prerequisites

- Node.js 18 or higher
- Claude Code CLI installed
- A RabbitAI Lab account with an MCP API Key

## Quick Start

### Option A: Install via Claude Code CLI

1. Add the marketplace:

```bash
claude plugin marketplace add RabbitAI-Lab/RabbitAI-Marketplace
```

2. Install the plugin:

```bash
claude plugin install rabbitai-lab-plugin@RabbitAI-Marketplace
```

### Option B: Manual Configuration

1. Create or edit `.mcp.json` in your project root:

```json
{
  "mcpServers": {
    "rabbit-ai": {
      "type": "http",
      "url": "https://rabbitai-lab.iapp.link/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_API_KEY",
        "projects": ""
      }
    }
  }
}
```

2. Replace `YOUR_MCP_API_KEY` with your RabbitAI Lab MCP API Key.

### Configure Environment Variable

Set the `RABBITAI_LAB_MCP_API_KEY` environment variable:

```bash
export RABBITAI_LAB_MCP_API_KEY="your-api-key-here"
```

## Usage

1. Navigate to your project directory and start Claude Code:

```bash
claude
```

2. Interact with RabbitAI Lab using natural language:

```
# Workspace management
List all my workspaces
Create a workspace named "New Project"

# Project management
Create a project in workspace xxx
List all active projects

# Requirements management
Add a requirement to project xxx: user login feature
List all requirements in project xxx

# Task management
Create a task for requirement xxx
Mark task xxx as done

# Bug management
Report a bug: login page fails to load
List all critical bugs in project xxx

# Test management
Create a test case for requirement xxx
Verify test xxx has passed

# Wiki
Create a document for project xxx
Update the content of document xxx

# Repository management
Bind a Git repo to project xxx: https://github.com/...
List all repositories for project xxx

# Integration management
Bind project xxx to a Slack channel
List all integration configs for project xxx

# AI settings
View AI automation settings for project xxx
Enable full automation mode for project xxx
```

## Project Structure

```
RabbitAI-Marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace configuration
├── .github/
│   └── workflows/
│       └── validate.yml          # CI validation: JSON format and plugin path checks
├── plugins/
│   └── rabbitai-lab-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json       # Plugin metadata
│       ├── .mcp.json             # MCP server configuration
│       ├── skills/               # Skill definitions
│       │   ├── ai-settings/
│       │   ├── bugs-mgr/
│       │   ├── integration-mgr/
│       │   ├── projects-mgr/
│       │   ├── repos-mgr/
│       │   ├── requirements-mgr/
│       │   ├── tasks-mgr/
│       │   ├── tests-mgr/
│       │   ├── wiki-mgr/
│       │   └── workspace-mgr/
│       ├── agents/
│       ├── commands/
│       ├── hooks/
│       └── scripts/
├── .gitignore
└── README.md
```

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

MIT License
