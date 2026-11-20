# PagerDuty Cursor Plugin

A Cursor plugin that connects your AI assistant to PagerDuty's hosted MCP server, enabling incident management, on-call lookups, service management, and more directly from your IDE.

## Overview

This plugin connects Cursor to PagerDuty's hosted MCP server at `https://mcp.pagerduty.com/mcp`. It authenticates with OAuth: you sign in to PagerDuty from Cursor, and no credentials are stored in the plugin.

## Installation

1. Open Cursor Settings
2. Navigate to **Plugins**
3. Click **Browse Marketplace**
4. Search for **PagerDuty**
5. Click **Install**

## Setup (OAuth)

1. In PagerDuty, register an OAuth app for Cursor, following [Choose an authorization method](https://docs.pagerduty.com/ai-automation/advance/pagerduty-mcp-server#step-1-choose-an-authorization-method).
2. Add the redirect URL(s) for the surfaces you authenticate from:
   - `http://localhost:8787/callback` (Cursor desktop)
   - `https://www.cursor.com/agents/mcp/oauth/callback` (Cursor web and Cursor Agents)
3. In Cursor, open **Plugins → PagerDuty → Configure** and enter the app's **Client ID** and **Client Secret**.
4. Reload Cursor, then click **Connect** / **Login** on the PagerDuty MCP server and approve access in PagerDuty.

## Skills

| Skill | Description |
|-------|-------------|
| `pagerduty-mcp-setup` | Walks you through registering a PagerDuty OAuth app and connecting the MCP server. |

## Support

- PagerDuty MCP Server Documentation: https://docs.pagerduty.com/ai-automation/advance/pagerduty-mcp-server
- PagerDuty Support: https://support.pagerduty.com
