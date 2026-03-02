---
layout: post
title: I automated my daily badminton poll with Claude Code
permalink: /badminton-bot
---

Every morning at 11:15 AM, someone in our badminton WhatsApp group needs to post a poll asking who's playing today. For months, that someone has been me.

It's a two-minute task. Open WhatsApp, tap the attach button, create a poll, type "game today", add yes/no/maybe, hit send. Perfectly reasonable. Also perfectly automatable.

So I did.

---

Here's what runs now, every weekday morning while I'm still having coffee:

1. A macOS LaunchAgent fires at 11:15 AM IST
2. It starts a fresh Claude Code session inside a tmux window
3. Claude opens WhatsApp Web via Playwright, creates the poll, and sends it
4. I get a Telegram notification confirming it's done

No browser open. No phone in hand. Poll appears in the group.

---

**The approach**

The core methodology is what I've started calling the *tmux autonomous workflow*. Instead of building a standalone script for each automation, I write a Claude Code skill file (a structured prompt in `~/.claude/skills/`) and use a bash script to open a headless Claude session in tmux, inject the slash command, and watch for it to complete.

The skill file for the badminton poll handles the actual work: kill Chrome, open WhatsApp Web, find the group, create the poll with the right options, and send a Telegram notification at the start and end. Claude handles all the Playwright interaction — clicking, typing, navigating — based on what it sees on screen.

The tmux orchestration script (`claude-tmux.sh`) handles the meta-layer: waiting for Claude to load, handling MCP server dialogs, sending the slash command with the right timing, auto-approving tool permission prompts, and detecting when the skill is complete.

This pattern is now reusable. The same `claude-tmux.sh` script runs my daily email outreach, Meetily leads reports, and now the badminton poll. Adding a new automation means writing a skill file, creating a three-line node wrapper, and setting up a LaunchAgent.

---

**What broke along the way**

Getting here was not smooth. A few things I learned:

**LaunchAgents can't use bash as the entry point.** If you set `/bin/bash` as the program in a LaunchAgent plist, and your script lives under `~/Documents`, you'll get an "Operation not permitted" error due to macOS Full Disk Access restrictions. The fix: use `/usr/local/bin/node` as the entry point. Node gets FDA from the LaunchAgent, and any bash process it spawns inherits it. So the "node wrapper" is just four lines — it calls `execFileSync('/bin/bash', ...)` on the actual bash script.

**The PATH doesn't include Homebrew.** LaunchAgents run with a minimal PATH that doesn't include `/opt/homebrew/bin`, which is where tmux lives on an Apple Silicon Mac. The bash script fails immediately with `tmux: command not found`. Fix: add `/opt/homebrew/bin` to the `EnvironmentVariables` section of the plist.

**Unicode characters break in POSIX locale.** My original script detected Claude's ready state by looking for the `❯` prompt character (U+276F). This works perfectly in a terminal. In a LaunchAgent, the locale is C/POSIX, and the multi-byte Unicode character doesn't match the grep pattern. The fix: match the ASCII string `for shortcuts` instead — it appears at the bottom of Claude's UI whenever it's idle and waiting for input.

**Exit too early, miss the approval prompts.** The first version of the script exited as soon as it detected Claude was running a tool (the `⏺` indicator). But approval prompts can fire mid-skill — after the script had already exited. The fix: don't exit early. Keep watching throughout the entire skill execution. Exit only when the `for shortcuts` text reappears, which signals Claude has returned to idle after completing the skill.

**The timeout needs to cover the whole skill, not just startup.** I initially set a 90-second timeout, thinking that covered Claude's startup time. But the timeout needs to cover startup *plus* full skill execution — WhatsApp loading, poll creation, Telegram notifications. Changed it to 300 seconds.

---

**The skill handles edge cases too**

The skill file checks if a poll was already posted today before creating a new one. If it finds one, it sends a Telegram notification (with the current vote counts) and skips posting. This prevents duplicates if I ever run the skill manually on the same day the cron fires.

If WhatsApp's session has expired (QR code showing instead of the chat list), the skill detects it, sends a Telegram alert asking me to scan the QR code, and aborts cleanly.

---

**The current setup**

- Skill file: `~/.claude/skills/badminton-poll/SKILL.md`
- Node wrapper: `~/Documents/scripts/run-badminton-poll.js`
- Orchestration: `~/Documents/scripts/claude-tmux.sh`
- LaunchAgent: `~/Library/LaunchAgents/com.skg.badminton-poll.plist`
- Schedule: Mon–Sat, 11:15 AM IST

The poll shows up. I vote when I wake up. We play.

<nav style="display: flex; flex-direction: column; gap: 5px; margin-top: 10px; padding-top: 20px; border-top: 1px solid #eee;">
  <div>
    <a href="https://notes.sijokuruvilla.in/singapore" style="text-decoration: none; color: #0366d6;">← Previous: I once travelled to Singapore on a 1 dollar ticket</a>
  </div>
  <div>
    <a href="https://notes.sijokuruvilla.in/" style="text-decoration: none; color: #0366d6;">Notes Home</a>
  </div>
</nav>
