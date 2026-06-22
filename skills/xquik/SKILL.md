---
name: xquik
description: Use Xquik MCP and REST APIs for X search, exports, compose, draws, monitors, and webhooks.
version: 1.0.0
license: MIT
author: "@kriptoburak"
tags:
  - x
  - mcp
  - automation
  - webhooks
  - social-data
---

## Instructions

Use this skill when an AI agent needs authenticated X data or workflow automation through Xquik. Prefer the MCP server for agent workflows and the REST API for application code.

### Prerequisites

- Xquik API key from https://dashboard.xquik.com/en/account
- MCP-capable client or HTTPS client
- Public docs at https://docs.xquik.com/mcp/overview
- Public MCP discovery at https://xquik.com/.well-known/mcp.json

Keep API keys out of prompts, logs, screenshots, examples, and committed files. Use environment variables or the client secret store.

### How to Use

1. Read the MCP overview and public discovery document.
2. Configure the MCP server at `https://xquik.com/mcp`.
3. Pass the API key as an `Authorization: Bearer` token or through the client secret mechanism.
4. Use `explore` to find matching API routes.
5. Use `xquik.request()` for authenticated Xquik API calls.
6. For event-driven workflows, create Xquik webhooks and verify HMAC signatures.

### Common Routes

- Search X posts: `GET /api/v1/x/tweets/search`
- Create extraction jobs: `POST /api/v1/extractions`
- Compose posts: `POST /api/v1/compose`
- Create giveaway draws: `POST /api/v1/draws`
- Create keyword monitors: `POST /api/v1/monitors/keywords`
- List trending radar data: `GET /api/v1/radar`

### Output

Xquik returns JSON API responses. Extraction jobs can also produce exported files through the documented job and result endpoints. Webhook workflows receive signed JSON events.

## Examples

**Example 1: Search X posts**

```
User: Find recent X posts about open source agent frameworks.
Agent: I will use the Xquik MCP server, call explore for the tweet search route, then call xquik.request("/api/v1/x/tweets/search", { query: { q: "open source agent frameworks", limit: 20 } }).
```

**Example 2: Export followers**

```
User: Export followers for @xquikcom.
Agent: I will create an extraction job with toolType "follower_explorer" and targetUsername "xquikcom", then poll the documented extraction result endpoint.
```

**Example 3: Create a keyword monitor**

```
User: Send webhook events when posts mention our launch keyword.
Agent: I will create a keyword monitor with the requested query and event types, then configure the webhook receiver to verify the Xquik signature header.
```

## Limitations

- Authentication is required for MCP actions.
- The agent should only create, publish, or monitor content after explicit user intent.
- Respect documented rate limits and pagination.
- Do not expose API keys, webhook secrets, or user data in responses.

## Dependencies

- Xquik account and API key
- MCP client with Streamable HTTP support or an HTTPS client
- Webhook receiver for event-driven workflows

## References

- https://docs.xquik.com/mcp/overview
- https://docs.xquik.com/api-reference/overview
- https://xquik.com/.well-known/mcp.json
- https://xquik.com/.well-known/agent-skills/index.json
