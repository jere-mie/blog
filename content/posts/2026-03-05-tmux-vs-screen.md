---
title: Switching from GNU Screen to Tmux for Background Sites
date: 2026-03-05
draft: false
author: Jeremie Bornais (with help from Gemini 3.1 Pro)
---

If you've read my previous post on [Using GNU Screen](./2024-02-07-using-gnu-screen.md), you know I've frequently relied on it as a terminal multiplexer. My primary use case has always been simple: run a website or background service, give the session a specific name, detach from it, and reattach later when the site needs an update.

While `screen` gets the job done, I've recently made the switch to `tmux` (Terminal Multiplexer). It's generally considered more modern, highly configurable, and offers a much better experience for handling windows and split panes.

Here is a quick guide on how to translate a simple background-process workflow from GNU Screen over to Tmux.

## The Core Workflow: Screen vs. Tmux

If your workflow is like mine - starting a server, leaving it running, and occasionally checking in - here is how the commands translate.

### 1. Starting a Named Session

When spinning up a new website, naming the session makes it easy to remember what's running where.

**Screen:**
```bash
screen -S my-website
```

**Tmux:**
```bash
tmux new -s my-website
```

Inside this new session, you can run your start commands for your site or service.

### 2. Detaching from the Session

Once the site is running, you want to leave it active in the background and return to your main terminal.

**Screen:** Press `Ctrl` + `A`, followed by `d`.
**Tmux:** Press `Ctrl` + `B`, followed by `d`.

*Note: `Ctrl+B` is the default "prefix" key in Tmux. Almost every Tmux shortcut starts with this prefix.*

### 3. Listing Active Sessions

When you need to update a site later, you might need a reminder of what sessions are currently running.

**Screen:**
```bash
screen -ls
```

**Tmux:**
```bash
tmux ls
```

### 4. Reattaching to a Session

Ready to pull the latest changes and restart the server? You'll need to reattach.

**Screen:**
```bash
screen -r my-website
```

**Tmux:**
```bash
tmux attach -t my-website
```
*(You can also use the shorthand: `tmux a -t my-website`)*

## Why Make the Switch?

If the commands map so cleanly, why bother switching? 

1. **The Status Bar:** Out of the box, Tmux provides a persistent, customizable status bar at the bottom of your terminal showing your open windows and session name.
2. **Window Panes:** Breaking a single window into vertical and horizontal panes is much more fluid in Tmux (`Ctrl`+`B` then `%` for vertical split, `Ctrl`+`B` then `"` for horizontal split). This lets you see server logs on one side while typing commands on the other.
3. **Configuration:** The `.tmux.conf` file uses a very clean, readable syntax to customize keybindings, colors, and behaviors.
4. **Tool Consolidation:** Rather than using `screen` as a one-off tool exclusively for backgrounding web servers, `tmux` can become the foundation of your entire terminal workflow. With its rich session and pane management, it makes sense to run everything inside `tmux`, letting you context-switch seamlessly instead of juggling separate toolsets for interactive work and background jobs.

If you are just running basic background processes, either tool will serve you well. But if you want to level up your terminal productivity, `tmux` is definitely the right choice!
