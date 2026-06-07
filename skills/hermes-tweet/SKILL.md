---
name: hermes-tweet
description: Configure Hermes Tweet for safe X/Twitter search, tweet lookup, threads, trends, social listening, and gated actions in Hermes Agent.
version: 1.0.0
license: MIT
author: "@Xquik-dev"
tags:
  - hermes-agent
  - twitter
  - x
  - social-listening
  - automation
---

## Instructions

Use this skill when a user wants Hermes Agent to work with X/Twitter through the Hermes Tweet plugin. Hermes Tweet is installed as a Hermes Agent plugin and uses Xquik for public X/Twitter automation workflows.

### What the Skill Accomplishes

This skill helps an agent:

1. Install Hermes Tweet through the Hermes Agent plugin manager.
2. Configure `XQUIK_API_KEY` without exposing credentials in chat, logs, issues, or public files.
3. Keep X/Twitter action tools disabled by default.
4. Use read-only workflows for search, tweet lookup, public profiles, threads, trends, monitoring, social listening, and digest generation.
5. Enable posting, replying, liking, reposting, following, or unfollowing only after explicit account-owner approval.

### Prerequisites

- Hermes Agent installed.
- Python 3.12 or newer for the Hermes Tweet package.
- A local or managed secret store containing `XQUIK_API_KEY`.
- Explicit user approval before enabling action tools.

### How to Use

Install and enable the plugin:

```bash
hermes plugins install Xquik-dev/hermes-tweet --enable
```

Configure the API key in the same runtime that starts Hermes Agent:

```bash
read -rsp "Xquik API key: " XQUIK_API_KEY
export XQUIK_API_KEY
```

Keep actions disabled for research and monitoring:

```bash
unset HERMES_TWEET_ENABLE_ACTIONS
```

Verify the plugin is enabled:

```bash
hermes plugins list
```

Use read-only prompts first:

```text
Use Hermes Tweet to find recent X posts about Hermes Agent plugins and summarize the main themes with links.
```

```text
Read this X thread and extract feature requests, objections, and follow-up opportunities.
```

Enable actions only for approved account-changing workflows:

```bash
export HERMES_TWEET_ENABLE_ACTIONS="true"
```

Before performing an action, restate the exact account, target tweet or profile, content, and approval boundary.

### Output

For read-only workflows, return:

- Short summary.
- Source links or tweet identifiers when available.
- Key accounts, themes, trends, or objections.
- Confidence notes when results are incomplete.
- Suggested follow-up searches or monitoring queries.

For action workflows, return:

- Exact action performed.
- Target account, tweet, or profile.
- Content used.
- Returned identifiers or status.
- Reminder to disable action mode after the workflow if it is no longer needed.

## Examples

**Example 1: X/Twitter research**

```text
User: Use Hermes Tweet to find recent posts about Hermes Agent plugins.
Agent: I will keep actions disabled, use Hermes Tweet read tools, summarize the strongest themes, and include source links or tweet identifiers where available.
```

**Example 2: Thread analysis**

```text
User: Read this X thread and tell me what product feedback matters.
Agent: I will use Hermes Tweet read tools to inspect the thread, then group feedback into feature requests, objections, praise, and follow-up opportunities.
```

**Example 3: Approved action**

```text
User: Post this update from my approved account.
Agent: I need action mode enabled with HERMES_TWEET_ENABLE_ACTIONS=true. I will restate the exact post content and account before sending.
```

## Limitations

- `XQUIK_API_KEY` must be configured outside the prompt.
- Action tools are intentionally disabled unless `HERMES_TWEET_ENABLE_ACTIONS=true` is set.
- The skill should not collect X cookies, passwords, recovery codes, or API keys in chat.
- Rate limits and availability depend on the configured Xquik account and runtime environment.
- If a key is exposed in chat or logs, stop the task and rotate the key before continuing.

## Dependencies

- Hermes Agent
- Hermes Tweet plugin: https://github.com/Xquik-dev/hermes-tweet
- Hermes Agent plugin guide: https://hermes-agent.nousresearch.com/docs/user-guide/features/plugins/
- Build a Hermes Plugin guide: https://hermes-agent.nousresearch.com/docs/guides/build-a-hermes-plugin/
- Xquik: https://xquik.com
