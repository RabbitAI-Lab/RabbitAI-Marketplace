---
name: tests-mgr
description: Manage test cases in RabbitAI Lab - create, update, delete, list, and search tests
version: 1.0.0
---

# Tests Manager

Manage test cases in RabbitAI Lab.

## When to Use

- User wants to create a new test case
- User wants to list, view, or search tests in a project
- User wants to update test status or details
- User wants to filter tests by requirement, task, or bug

## Available Tools

All tools are from the `rabbit-ai` MCP server. Parameter details are provided by the MCP server at call time.

- **list_tests** - List tests with pagination and keyword search; can filter by requirement, task, or bug
- **get_test** - Get a single test by ID
- **create_test** - Create a new test (supports verification steps, browser scripts, screenshots as `{ name, url }` arrays)
- **update_test** - Update test details
- **delete_test** - Delete a test

## Guidelines

- Test status: `NEW` -> `VERIFYING` -> `VERIFIED`.
- `list_tests` requires `projectId` — always determine the project first.
- A test can be linked to a `requirementId`, `taskId`, and/or `bugId` to establish traceability.
- When creating a test, `verificationSteps` should describe clear, step-by-step instructions for validation.
- `browserScript` can hold browser automation code for automated testing.
- `screenshots` is an array of `{ name, url }` objects for visual evidence.

## Workflow

1. To create a test: provide at minimum a `title`; include `projectId` and optionally link to a requirement or task.
2. To find tests: call `list_tests` with `projectId` and optional `keyword`.
3. To verify a test: call `update_test` with `id` and `status: "VERIFIED"`.
