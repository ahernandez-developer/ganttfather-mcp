# GanttFather MCP server

A remote [Model Context Protocol](https://modelcontextprotocol.io) server for [GanttFather](https://ganttfather.com), an online Gantt chart and Kanban tool. It lets an AI assistant read and edit your GanttFather projects: tasks, dates, dependencies, resources, the critical path, and the chart itself.

This repository holds documentation and the registry entry only. The server is hosted; there is nothing to install or run.

- **URL:** `https://mcp.ganttfather.com/`
- **Transport:** streamable HTTP
- **Sign-in:** OAuth 2.1 with dynamic client registration and PKCE (S256), scopes `mcp:read` and `mcp:write`. Clients that can't do OAuth can send a project token from GanttFather (AI Agents & API) as `Authorization: Bearer <token>`.
- **Official MCP Registry:** `com.ganttfather/ganttfather`
- **Docs and setup guides:** https://ganttfather.com/mcp/
- **Price:** free for one project with two editors; viewers and guests are free.

## Add it to your client

The quickest way is to add the URL as a remote server and sign in when your client asks.

**Claude** (claude.ai and the desktop app): Settings, Connectors, Add custom connector, then paste `https://mcp.ganttfather.com/`.

**Claude Code**

```bash
claude mcp add --transport http ganttfather https://mcp.ganttfather.com/
```

**VS Code (GitHub Copilot Chat)**, in `.vscode/mcp.json`:

```json
{ "servers": { "ganttfather": { "type": "http", "url": "https://mcp.ganttfather.com/" } } }
```

**GitHub Copilot CLI**

```bash
copilot mcp add --transport http ganttfather https://mcp.ganttfather.com/
```

Then run `/mcp auth ganttfather` inside Copilot CLI.

**Cursor**, in `~/.cursor/mcp.json`:

```json
{ "mcpServers": { "ganttfather": { "url": "https://mcp.ganttfather.com/" } } }
```

**Windsurf** and **Antigravity**, in `mcp_config.json` (they read `serverUrl`):

```json
{ "mcpServers": { "ganttfather": { "serverUrl": "https://mcp.ganttfather.com/" } } }
```

**Codex**

```bash
codex mcp add ganttfather --url https://mcp.ganttfather.com/
```

**Gemini CLI**, in `settings.json` (it needs `httpUrl`; a plain `url` means an older transport there):

```json
{ "mcpServers": { "ganttfather": { "httpUrl": "https://mcp.ganttfather.com/" } } }
```

**OpenCode**, in `opencode.json`, then run `opencode mcp auth ganttfather`:

```json
{ "$schema": "https://opencode.ai/config.json", "mcp": { "ganttfather": { "type": "remote", "url": "https://mcp.ganttfather.com/", "enabled": true } } }
```

Guides for ChatGPT, Gemini, Goose, n8n and others are at https://ganttfather.com/mcp/. Of the clients above, we have tested Claude end to end; reports from the others are welcome in Issues.

## Tools

27 tools. Every tool sets `readOnlyHint`, `destructiveHint` and `openWorldHint` explicitly; writes that can overwrite or remove data are marked destructive, so your client can ask before running them.

| Tool | Title | Kind |
| --- | --- | --- |
| `draft_support_email` | Draft support email (never sends it) | read |
| `get_critical_path` | Get critical path | read |
| `get_overdue_tasks` | Get overdue tasks | read |
| `get_project` | Get project | read |
| `get_project_summary` | Get project summary | read |
| `get_project_timeline` | Get project timeline | read |
| `get_task` | Get task | read |
| `list_dependencies` | List dependencies | read |
| `list_members` | List members | read |
| `list_projects` | List projects | read |
| `list_resources` | List resources | read |
| `list_tasks` | List tasks | read |
| `render_gantt_image` | Render Gantt image (SVG or Mermaid) | read |
| `show_gantt_chart` | Show Gantt chart (interactive widget) | read |
| `add_dependency` | Add dependency | write, destructive |
| `add_resource` | Add resource | write |
| `add_task_image` | Add image to task | write |
| `create_task` | Create task | write |
| `delete_resource` | Delete resource | write, destructive |
| `delete_task` | Delete task | write, destructive |
| `remove_dependency` | Remove dependency | write, destructive |
| `reorder_tasks` | Reorder tasks | write, destructive |
| `set_task_assignees` | Set task assignees | write, destructive |
| `set_task_dependencies` | Set task dependencies | write, destructive |
| `update_project_context` | Update project context | write, destructive |
| `update_resource` | Update resource | write, destructive |
| `update_task` | Update task | write, destructive |

## Privacy and support

The assistant sees only the projects the signed-in account can see, and you can revoke its access at any time in GanttFather, under AI Agents & API. Privacy policy: https://ganttfather.com/privacy/. Support: support@ganttfather.com.

## License

The documentation and configuration in this repository are under the MIT License. The GanttFather service itself is proprietary.
