# openclaw-prd-writer

> Turn a rough idea into a build-ready spec through a structured agent conversation.

You describe what you want to build. Your OpenClaw agent asks clarifying questions,
proposes an architecture plan, gets your approval, writes a detailed PRD to disk,
gets your approval again, then hands off to a coding agent to build it.

Two approval gates. Nothing gets specced or built without explicit confirmation.

[![License: MIT][badge-license]]
[![OpenClaw][badge-openclaw]]

## 👤 For Humans

**Say any of these to your agent:**
> "spec this", "write a PRD", "plan this feature", "build me X", "/spec"

**What happens:**
1. Agent restates your idea + asks 3-7 clarifying questions (as polls/buttons)
2. Proposes a lightweight Master Plan — you approve or edit
3. Writes a detailed PRD to `projects/[name]/PRD.md` — you approve or edit
4. Hands off to [openclaw-coding-loops](https://github.com/bkochavy/openclaw-coding-loops) to build

**The PRD file is yours.** It lives on disk and can be handed to any coding agent —
Codex, Claude Code, or a future tool.

## 🤖 For Agents

Use the runbook in `SKILL.md`:
- Pipeline phases: `Understand → Plan → Approve → Spec → Approve → Handoff`
- Polls vs buttons: use polls for rich multi-option questions, inline buttons for quick confirmations
- Cross-thread pattern: drive from caller, include full context in callbacks, prefer compact answer formats
- Five non-negotiables:
  - Never skip clarify-first questioning
  - Never spec before plan approval (Gate 1)
  - Never hand off before PRD approval (Gate 2)
  - Never pad questions; each one must remove ambiguity
  - Always write the PRD to disk

## Install

Drop into your OpenClaw workspace skills folder:

```bash
git clone https://github.com/bkochavy/openclaw-prd-writer.git \
  ~/.openclaw/workspace/skills/openclaw-prd-writer
```

Or tell your agent: "install the prd-writer skill from github.com/bkochavy/openclaw-prd-writer"

## Requirements

- OpenClaw with any channel (Telegram, Discord, iMessage, etc.)
- `projects/` directory writable in your workspace
- openclaw-coding-loops (optional, for handoff)

[badge-license]: https://img.shields.io/badge/License-MIT-yellow.svg
[badge-openclaw]: https://img.shields.io/badge/OpenClaw-Skill-blue.svg
