# Training Coach for Claude Code

Turns Claude Code into your coach, with live access to your own training plan, workouts and
logs. It reads what you actually did, and rewrites what you are about to do — always showing
you the change before it writes it.

## Two ways to use it

**On your phone (or claude.ai):** add the training server as a connector once, and every
Claude Code cloud session — and every chat — has your coach's tools.

1. Sign in at [claude.ai](https://claude.ai) in a browser (on a phone it pushes you to download
   the app: ignore that and stay on the site; the app itself cannot add connectors). Then open
   [claude.ai/customize/connectors](https://claude.ai/customize/connectors) → *Add custom
   connector* → URL `https://alephknot-training.fly.dev/mcp` → *Add*, then *Connect* and sign in
   with your training-app username and password (or create an account right there).
2. Tap **Ask your coach** in the training app, or the `</>` on any workout. It opens Claude Code
   on this repo with the coach persona loaded and the workout or a prompt ready for your question.
3. Optional, to have those taps open the Claude **app** straight into a session: create a routine at
   [claude.ai/code/routines](https://claude.ai/code/routines) with this repo, the Training connector
   and an API trigger, and paste its URL and token into the training app's Settings. The prompt to
   save on the routine is shown there.

**In the terminal:**

```
/plugin install training-coach --marketplace r-wedeen/training-coach-plugin
```

Then `/mcp` → `training` → *Authenticate*: a browser page asks for your training-app username
and password. No API key, nothing in your shell profile. Your token lives in the system keychain.

On older Claude Code versions, add the marketplace first:

```
/plugin marketplace add r-wedeen/training-coach-plugin
/plugin install training-coach@training-coach
```

If you run your own server, `/plugin configure training-coach` has a **Server address** field.

## Use it

Just talk to it.
