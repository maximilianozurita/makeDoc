---
name: makeDoc
description: Generates or updates professional technical documentation for GitHub projects. Use /makeDoc to generate from scratch, /makeDoc --update to update, /makeDoc --agent to run in a subagent.
argument-hint: [--update] [--agent]
allowed-tools: [Read, Write, Glob, Grep, LS, Bash]
---

Read and follow the skill at `~/.claude/skills/makeDoc-skill/SKILL.md`.

Detect the received flags:
- No flags → creation mode
- `--update` → update mode
- `--agent` → delegate to the `makeDoc-agent` agent
- `--agent --update` → delegate to the agent with the `--update` flag

### If the command includes `--agent`:

Delegate the entire task to the `makeDoc-agent` agent using the subagent tool.

Pass as prompt:
- The current working directory (absolute path)
- The received flags without `--agent`

Example prompt to the agent:
```
Run the makeDoc skill in the directory: /path/to/project
Flags: --update
```

Do not perform any exploration or generation yourself. Everything is handled by the agent.

### If the command does NOT include `--agent`:

Read and follow the skill at `~/.claude/skills/makeDoc-skill/SKILL.md`.

Explore the current project before writing any file.
Do not generate generic content: everything must be specific to the code you are reading.
