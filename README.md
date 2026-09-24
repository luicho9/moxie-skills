# moxie-skills

Agent skills for the Moxie team. Written in the standard `SKILL.md` format so they work in Claude Code / Claude desktop and Codex.

## Skills

| Skill | For | What it does |
|---|---|---|
| [pm-explore](skills/pm-explore/SKILL.md) | PMs | Explores the codebase read-only from a product request and creates an engineer-ready draft task in Orkestrr |

## Setup

### 1. Orkestrr MCP

```bash
uv tool install orkestrr-mcp   # or: pipx install orkestrr-mcp
okr login                      # browser SSO, once
okr status
```

Register the server:

- **Claude Code:**
  ```bash
  claude mcp add --scope user orkestrr \
    --env ORKESTRR_BASE_URL=https://api.orkestrr.com \
    -- okr mcp
  ```
- **Claude desktop / Codex desktop:** add an MCP server with command `okr`, args `["mcp"]`, and env `ORKESTRR_BASE_URL=https://api.orkestrr.com`.

### 2. Install the skill

Copy or symlink `skills/pm-explore` into:

- Claude: `~/.claude/skills/` (all projects) or `<repo>/.claude/skills/` (one repo)
- Codex: the skills directory Codex reads (`~/.agents/skills/` or `<repo>/.agents/skills/`)

### 3. Use it

Open a Moxie repo in the app and describe what you want, e.g. "Use pm-explore: patients can't see their next appointment on the home screen."
