---
name: connect
description: >-
  Connect this plugin to the athlete's training app account, or diagnose why the training
  tools are missing, returning 401/403, or failing to reach the server. Use when the coach
  tools are unavailable, authentication fails, or the athlete is setting the plugin up for
  the first time.
---

# Connect the coach to the training app

The plugin talks to the athlete's own training server over MCP. It needs two values, both
read from the environment at startup:

| variable | meaning |
|---|---|
| `TRAINING_API_KEY` | the API key from the app's Settings screen (required) |
| `TRAINING_MCP_URL` | the server's MCP endpoint; only needed for a self-hosted server |

## Setting them up

The key is in the app under **Settings → API key**. It must be exported before Claude Code
starts, because MCP servers are launched with the session:

```bash
echo 'export TRAINING_API_KEY="paste-the-key-here"' >> ~/.zshrc
source ~/.zshrc
```

Then restart Claude Code and run `/mcp` to confirm the `training` server is connected.

Self-hosted servers also need the endpoint, which is the app's base URL with `/mcp` appended:

```bash
echo 'export TRAINING_MCP_URL="https://your-server.example.com/mcp"' >> ~/.zshrc
```

## Diagnosing

- **No `training` tools at all** — the plugin is installed but the server did not start.
  Check `/mcp`, then confirm `TRAINING_API_KEY` is exported *in the shell that launched Claude Code*
  (`echo $TRAINING_API_KEY`). A key set after launch has no effect until restart.
- **401 or "the bearer key was rejected"** — the key is wrong or was rotated. Copy it again
  from the app's Settings screen.
- **Connection refused or a timeout** — the server is unreachable. If it is self-hosted on a
  platform that sleeps idle machines, the first request can take a few seconds; retry once.
  Otherwise check the URL is the base URL plus `/mcp`.
- **Tools work but return nothing** — the account is reachable but has no plan imported yet.
  Say so plainly rather than inventing a plan.

Never ask the athlete to paste their API key into the conversation. It belongs in the
environment, and you do not need to see it to use the tools.
