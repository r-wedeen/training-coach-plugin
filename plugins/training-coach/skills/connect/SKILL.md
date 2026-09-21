---
name: connect
description: >-
  Connect this plugin to the athlete's training app account, or diagnose why the training
  tools are missing, returning 401/403, or failing to reach the server. Use when the coach
  tools are unavailable, authentication fails, or the athlete is setting the plugin up for
  the first time.
---

# Connect the coach to the training app

The plugin talks to the athlete's own training server over MCP, and the athlete signs in to it
**with their app username and password** through a browser page the server shows. There is no
API key anywhere. Claude Code stores the resulting token in the system keychain and refreshes it
on its own.

- **First time:** run `/mcp`, pick `training`, choose *Authenticate*. A browser page opens; they
  sign in, or create an account there if they are new. That's it.
- **Server address** is the only plugin setting (`/plugin configure training-coach`), and only
  changes if they run their own server: the base URL with `/mcp` on the end.

## Diagnosing

- **No `training` tools at all** — the plugin is installed but not signed in. `/mcp` → `training`
  → *Authenticate*.
- **401 / "needs authentication"** — the token expired or every device was signed out (changing
  the password in the app does that). Authenticate again from `/mcp`.
- **The browser page says the link expired** — the sign-in took longer than ten minutes. Start
  again from `/mcp`.
- **Connection refused or a timeout** — the server is unreachable. Check the Server address is
  the base URL with `/mcp` on the end.
- **Tools work but return nothing** — the account is reachable but has no plan yet. A new account
  starts empty: offer to build one with them (`bulk_replace`) or to import a CSV in the app.

Never ask the athlete for their password in the conversation; the browser page is where it goes.
