---
name: connect
description: >-
  Connect this plugin to the athlete's training app account, or diagnose why the training
  tools are missing, returning 401/403, or failing to reach the server. Use when the coach
  tools are unavailable, authentication fails, or the athlete is setting the plugin up for
  the first time.
---

# Connect the coach to the training app

The plugin talks to the athlete's own training server over MCP. Both values it needs are
plugin settings, entered in a dialog at install time and stored in the system keychain:

| setting | meaning |
|---|---|
| **Training app API key** | the server's `TRAINING_API_KEY` (the operator sets it with `fly secrets set`; it is *not* the username/password the app itself signs in with) (required, stored as a secret) |
| **Server address** | the MCP endpoint; only changed if they run their own server |

To change either, the athlete runs `/plugin configure training-coach`. Nothing needs to go in
a shell profile, and Claude Code does not need restarting after a change.

## Diagnosing

- **No `training` tools at all** — the plugin is installed but the server never started. Check
  `/mcp`. If the key was never entered, `/plugin configure training-coach` will ask for it.
- **401, or "the bearer key was rejected"** — the key is wrong or was rotated. Copy it again
  from the operator (`fly secrets set TRAINING_API_KEY=…` on the server) and re-enter it with
  `/plugin configure training-coach`. The app's own username and password do not open the MCP endpoint.
- **Connection refused or a timeout** — the server is unreachable. Check the Server address is
  the base URL with `/mcp` on the end. A self-hosted server that sleeps when idle may need one
  retry to wake.
- **Tools work but return nothing** — the account is reachable but has no plan imported yet.
  Say so plainly rather than inventing a plan.

Never ask the athlete to paste their API key into the conversation. It belongs in the plugin
settings, and you do not need to see it to use the tools.
