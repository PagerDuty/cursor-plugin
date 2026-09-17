---
name: pagerduty-mcp-setup
description: REQUIRED setup for how to use the PagerDuty MCP server. IMPORTANT If you want to use PagerDuty MCP tools, read these instructions BEFORE checking tool schemas or doing any PagerDuty investigation because the MCP may not work until the API token is configured.
---

IMPORTANT: Before using the PagerDuty MCP or doing any other investigation related to PagerDuty, you must follow these directions and make sure that the following requirements are met.

### Context

The PagerDuty MCP authenticates with a PagerDuty User API token. The token is supplied through the `PAGERDUTY_API_TOKEN` plugin variable declared in `.cursor-plugin/plugin.json`, which the user sets in Cursor's plugin settings. Cursor substitutes that variable into the `Authorization` header when it starts the MCP server.

The plugin's `mcp.json` stores the header as a template:

```json
{
  "Authorization": "Token ${PAGERDUTY_API_TOKEN}"
}
```

IMPORTANT: `${PAGERDUTY_API_TOKEN}` remains in `mcp.json` even after the token is configured, because substitution happens at runtime and never rewrites the file. Do not read `mcp.json` to decide whether the MCP is configured — the placeholder is present in both the configured and non-configured states. Do not ask the user to hand-edit `mcp.json` either, since the file is restored on every plugin update.

### Steps

1. Confirm the MCP is authenticated by making one cheap read call, such as `browse_incidents` with action `list_workflows` and `limit` 1.
2. If the call succeeds, the token is configured. Continue on to the PagerDuty task.
3. If the call fails with an authentication or authorization error (HTTP 401 or 403), stop. Tell the user the PagerDuty MCP is not configured yet, and in that message do all of the following:
   - Tell them to open Cursor Settings, find the PagerDuty plugin, and set the **PagerDuty API Token** variable.
   - Tell them to supply only the token value, since the `Authorization` header already includes the `Token ` prefix.
   - Tell them they can follow PagerDuty's API token instructions here: `https://support.pagerduty.com/main/docs/pagerduty-mcp-server-integration-guide#generate-your-pagerduty-api-token`
   - Do not ask them to send you the token.
   - Do not continue the PagerDuty task yet.
4. Once the user has set the variable, tell them to refresh Cursor by opening the Command Palette (`⌘⇧P` on Mac or `Ctrl+Shift+P` on Windows/Linux) and running `Reload Window`. Use the current operating system to decide what keybinding to show. Then retry step 1.

### Reference

- PagerDuty API token setup instructions: `https://support.pagerduty.com/main/docs/pagerduty-mcp-server-integration-guide#generate-your-pagerduty-api-token`
- PagerDuty hosted MCP setup guide: `https://support.pagerduty.com/main/docs/pagerduty-mcp-server-integration-guide`
- PagerDuty developer docs: `https://developer.pagerduty.com/docs/mcp-tooling-remote-server`
