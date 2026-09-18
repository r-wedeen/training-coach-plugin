# Training Coach for Claude Code

Turns Claude Code into your coach, with live access to your own training plan, workouts and
logs. It reads what you actually did, and rewrites what you are about to do — always showing
you the change before it writes it.

## Install

```
/plugin install training-coach --marketplace r-wedeen/training-coach-plugin
```

Claude Code asks for your **API key** as it installs. Copy it from the app's **Settings**
screen and paste it into the dialog. It is stored in your system keychain, not in a file, and
you are never asked again. There is nothing to add to your shell profile.

On older Claude Code versions, add the marketplace first:

```
/plugin marketplace add r-wedeen/training-coach-plugin
/plugin install training-coach@training-coach
```

To change the key later, run `/plugin configure training-coach`. If you run your own server,
the same dialog has a **Server address** field.

## Use it

Just talk to it.

- "How did last week go?"
- "My knees are wrecked, lighten Thursday."
- "Move everything forward a week, I'm travelling."
- "I hit a 150 kg back squat today."
- "Why is my mile time stalling?"

It can rewrite sessions, shift your schedule, record new maxes and re-anchor your pace zones.
Changes to past sessions and to sessions you have already logged are refused by the server,
not just by the model.

## What runs where

The AI runs in **your** Claude Code session on your own subscription. The plugin ships no
model access and no secrets; your server only stores training data. Uninstall with
`/plugin uninstall training-coach`.
