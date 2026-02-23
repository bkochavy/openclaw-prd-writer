# openclaw-prd-writer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue.svg)](https://openclaw.ai)

![openclaw-prd-writer](https://raw.githubusercontent.com/bkochavy/openclaw-prd-writer/main/.github/social-preview.png)

You have a rough idea. You tell your agent. It asks the right questions, drafts an architecture plan, writes a full PRD to disk, and hands off to a coding agent — all with two approval gates so nothing gets built without your say-so.

This is a skill for [OpenClaw](https://openclaw.ai), the self-hosted AI agent platform. It works across any channel OpenClaw supports: Telegram, Discord, iMessage, and more.

## Install

```bash
git clone https://github.com/bkochavy/openclaw-prd-writer.git ~/.openclaw/workspace/skills/openclaw-prd-writer
```

Or just tell your agent: *"install the prd-writer skill from github.com/bkochavy/openclaw-prd-writer"*

## 👤 For Humans

Say something like *"spec this"*, *"write a PRD for X"*, *"plan this feature"*, or just `/spec` — the agent takes it from there.

It starts by restating your idea and asking 3-7 clarifying questions as tappable polls, so you pick options instead of typing paragraphs. Once it understands what you want, it proposes a lightweight Master Plan — the architecture and task breakdown at a glance. You approve, tweak, or scrap it.

After you approve the plan, the agent writes a detailed PRD to `projects/[name]/PRD.md` — specific enough that a coding agent can build from it with zero guesswork. You review that too. Two gates, two thumbs-up, then it hands off to [openclaw-coding-loops](https://github.com/bkochavy/openclaw-coding-loops) to start building.

The PRD file is yours. It's a Markdown file on disk, portable to any coding agent — Codex, Claude Code, or whatever comes next.

## 🤖 For Agents

### Quick start

1. Clone into the skills directory:
   ```bash
   git clone https://github.com/bkochavy/openclaw-prd-writer.git \
     ~/.openclaw/workspace/skills/openclaw-prd-writer
   ```
2. The skill activates on triggers: `"spec this"`, `"write a PRD"`, `"plan this feature"`, `"build me X"`, `"/spec"`
3. Read `SKILL.md` for the full runbook

### Pipeline

```
IDEA → Understand → Plan → [Gate 1] → Spec → [Gate 2] → Handoff
```

### Key behaviors

- **Understand** — Restate the idea, identify unknowns, ask 3-7 clarifying questions via polls/buttons
- **Plan** — Generate a Master Plan (architecture + task groups + success criteria). Await explicit approval before proceeding
- **Spec** — Write a detailed PRD to `projects/[name]/PRD.md` using `references/prd-template.md`. Await explicit approval
- **Handoff** — Set up and launch [openclaw-coding-loops](https://github.com/bkochavy/openclaw-coding-loops), or let the user take it from here

### Non-negotiables

1. Never skip the clarify-first questioning phase
2. Never spec before the Master Plan is approved (Gate 1)
3. Never hand off before the PRD is approved (Gate 2)
4. Never pad questions — each one must resolve genuine ambiguity
5. Always write the PRD to disk at `projects/[name]/PRD.md`

### Cross-thread execution

When driving a PRD interview from a different thread than where it was triggered: drive from the calling session, include full context in button callbacks, and prefer compact answer formats (`"1C, 2B, 3A"`). See `SKILL.md` for details.

### Requirements

- OpenClaw instance with any configured channel
- `projects/` directory writable in the workspace
- [openclaw-coding-loops](https://github.com/bkochavy/openclaw-coding-loops) (optional, for automated handoff)

### Project structure

```
SKILL.md                    # Full runbook — start here
references/prd-template.md  # PRD template with all sections
examples/example-prd.md     # Sample PRD for reference
```

## License

[MIT](LICENSE)
