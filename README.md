# makeDoc

Claude Code plugin that generates and updates professional technical documentation for GitHub projects.

Analyzes the source code and writes directly to the filesystem:
- `README.md` with navigation index
- `docs/architecture.md`
- `docs/structure.md`
- `docs/installation.md`
- `docs/decisions.md`
- `docs/usage.md` *(if applicable)*
- `docs/api.md` *(if applicable)*
- `docs/testing.md` *(if applicable)*

## Installation

### Via plugin system (recommended)

```
/plugin marketplace add maximilianozurita/makeDoc
/plugin install makeDoc@makeDoc
```

### Manual (standalone)

```bash
git clone https://github.com/maximilianozurita/makeDoc ~/.claude/plugins/makeDoc
mkdir -p ~/.claude/skills && cp -a ~/.claude/plugins/makeDoc/skills/. ~/.claude/skills/
mkdir -p ~/.claude/agents && cp -a ~/.claude/plugins/makeDoc/agents/. ~/.claude/agents/
```

## Usage

When installed via the **plugin system**, skills are namespaced:

```
/makeDoc:makeDoc                    # Generate documentation from scratch
/makeDoc:makeDoc --update           # Update existing documentation
/makeDoc:makeDoc --agent            # Run in a subagent (clean context)
/makeDoc:makeDoc --agent --update   # Combine both modes
```

When installed **manually** (standalone):

```
/makeDoc                    # Generate documentation from scratch
/makeDoc --update           # Update existing documentation
/makeDoc --agent            # Run in a subagent (clean context)
/makeDoc --agent --update   # Combine both modes
```

## What it does

### Creation mode
Explores the project, analyzes the stack and architecture, and generates all documentation files in the current directory.

### Update mode (`--update`)
Reads existing documentation, compares it against the current state of the code, and updates only what changed. Preserves content that is still valid.

### Agent mode (`--agent`)
Spawns a subagent with a clean context to execute the task. Useful for large projects or sessions with a lot of accumulated context.

## Writing rules

- All content is specific to the analyzed code, never generic
- If something has no evidence in the code, the section is omitted
- No warning banners in generated files
- Written in English, except technical names, paths and code

## Plugin structure

```
makeDoc/
├── .claude-plugin/
│   ├── plugin.json         # Plugin manifest
│   └── marketplace.json    # Marketplace catalog
├── skills/
│   └── makeDoc/
│       └── SKILL.md        # Command /makeDoc (user-invoked, contains full logic)
├── agents/
│   └── makeDoc-agent.md    # Subagent for --agent mode (self-contained)
└── README.md
```
