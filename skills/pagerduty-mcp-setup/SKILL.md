---
name: pagerduty-mcp-setup
description: Setup and troubleshooting for the PagerDuty MCP server in Cursor. Use when PagerDuty MCP tools are unavailable, the server shows "Needs login" or an OAuth error, or the user asks how to connect PagerDuty to Cursor.
---

The PagerDuty plugin connects to PagerDuty's hosted MCP server (`../../mcp.json`) using OAuth with a PagerDuty OAuth app that the user (or their admin) registers. The plugin does not contain any credentials, and the agent must never ask the user to paste a client secret into chat.

If PagerDuty MCP tools are available and respond, skip this skill and continue the task.

### Setup steps to give the user

1. Register an OAuth app in PagerDuty, following https://docs.pagerduty.com/ai-automation/advance/pagerduty-mcp-server#step-1-choose-an-authorization-method
2. Add the redirect URL(s) for the surfaces you authenticate from:
   - `http://localhost:8787/callback` (Cursor desktop)
   - `https://www.cursor.com/agents/mcp/oauth/callback` (Cursor web and Cursor Agents)
3. In Cursor, open **Plugins → PagerDuty → Configure** and enter the app's Client ID and Client Secret.
4. Reload Cursor: Command Palette (`⌘⇧P` on Mac, `Ctrl+Shift+P` on Windows/Linux), then `Reload Window`. Use the current OS to pick the keybinding.
5. In Cursor's MCP settings, click **Connect** / **Login** on the PagerDuty server and approve access in the browser.

### Troubleshooting

- **No sign-in prompt, or sign-in fails immediately:** the Client ID or Secret was not entered in Plugins → Configure, or was mistyped.
- **Redirect URI mismatch:** the redirect URL Cursor used is not registered on the OAuth app. Add the redirect URL for the surface you authenticate from. Cursor web and Cursor Agents use the `https://www.cursor.com/...` callback.
- **Signed in, but tools fail with permission errors:** the PagerDuty user or app lacks access to the requested resources.
- **PagerDuty tools missing, or the wrong server responds:** another PagerDuty plugin or MCP server is installed (for example the Claude Code PagerDuty plugin imported into Cursor, or a PagerDuty server in ~/.cursor/mcp.json). Disable it in Customize and reload Cursor.
- For anything else, see https://docs.pagerduty.com/ai-automation/advance/pagerduty-mcp-server#step-1-choose-an-authorization-method
