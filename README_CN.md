# RabbitAI Marketplace

[English](README.md)

RabbitAI Lab 官方 Claude Code 插件市场 —— 通过 MCP 连接 RabbitAI Lab 平台，提供 AI 驱动的项目管理工具集。

## 可用插件

| 插件 | 说明 |
|------|------|
| **rabbitai-lab-plugin** | RabbitAI Lab 官方插件，提供工作区、项目、需求、任务、缺陷、测试、知识库、仓库、集成及 AI 设置等全套管理能力 |

### 插件包含的 Skills

| Skill | 说明 |
|-------|------|
| **workspace-mgr** | 工作区管理：创建、更新、删除工作区，成员管理，邀请链接，数据导入/导出，审批流程 |
| **projects-mgr** | 项目管理：在工作区内创建、查看、更新、删除项目 |
| **requirements-mgr** | 需求管理：需求及需求分类的 CRUD，支持嵌套分类和附件链接 |
| **tasks-mgr** | 任务管理：任务的创建、状态流转、优先级设置 |
| **bugs-mgr** | 缺陷管理：缺陷报告、跟踪、状态流转和严重度评估 |
| **tests-mgr** | 测试管理：测试用例管理，支持验证步骤、浏览器脚本和截图 |
| **wiki-mgr** | 知识库管理：Markdown 格式的项目文档创建、编辑和浏览 |
| **repos-mgr** | 仓库管理：Git 仓库绑定，支持多种认证方式（Token / SSH / Basic） |
| **integration-mgr** | 集成管理：第三方集成配置，聊天群组绑定（Slack / Discord / 企业微信 / 钉钉等） |
| **ai-settings** | AI 设置：配置项目 AI 自动化行为，包括需求准入、计划对齐、任务设计和测试自动化 |

## 前提条件

- Node.js 18 或更高版本
- 已安装 Claude Code CLI
- 拥有 RabbitAI Lab 账号并获取 MCP API Key

## 快速开始

### 方式 A：通过 Claude Code CLI 安装

1. 添加 Marketplace：

```bash
claude plugin marketplace add RabbitAI-Lab/RabbitAI-Marketplace
```

2. 安装插件：

```bash
claude plugin install rabbitai-lab-plugin@RabbitAI-Marketplace
```

### 方式 B：手动配置

1. 在项目根目录创建或编辑 `.mcp.json`：

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

2. 将 `YOUR_MCP_API_KEY` 替换为你的 RabbitAI Lab MCP API Key。

### 配置环境变量

设置 `RABBITAI_LAB_MCP_API_KEY` 环境变量：

```bash
export RABBITAI_LAB_MCP_API_KEY="your-api-key-here"
```

## 使用方式

1. 进入你的项目目录并启动 Claude Code：

```bash
claude
```

2. 直接使用自然语言与 RabbitAI Lab 交互：

```
# 工作区管理
列出我的所有工作区
创建一个名为"新项目"的工作区

# 项目管理
在工作区 xxx 中创建一个项目
列出所有进行中的项目

# 需求管理
为项目 xxx 添加一个需求：用户登录功能
列出项目 xxx 的所有需求

# 任务管理
为需求 xxx 创建一个任务
将任务 xxx 标记为完成

# 缺陷管理
报告一个 bug：登录页面无法加载
列出项目 xxx 的所有严重 bug

# 测试管理
为需求 xxx 创建一个测试用例
验证测试 xxx 是否通过

# 知识库
为项目 xxx 创建一篇文档
更新文档 xxx 的内容

# 仓库管理
为项目 xxx 绑定 Git 仓库 https://github.com/...
列出项目 xxx 的所有仓库

# 集成管理
将项目 xxx 绑定到 Slack 频道
列出项目 xxx 的所有集成配置

# AI 设置
查看项目 xxx 的 AI 自动化设置
开启项目 xxx 的全自动化模式
```

## 项目结构

```
RabbitAI-Marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace 配置
├── .github/
│   └── workflows/
│       └── validate.yml          # CI 校验：JSON 格式与插件路径验证
├── plugins/
│   └── rabbitai-lab-plugin/
│       ├── .claude-plugin/
│       │   └── plugin.json       # 插件元信息
│       ├── .mcp.json             # MCP 服务器配置
│       ├── skills/               # Skill 定义
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

## 贡献指南

欢迎贡献！请随时提交 Issue 或 Pull Request。

## 许可证

MIT License
