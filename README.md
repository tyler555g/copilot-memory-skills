# basic-memory-skills

OpenClaw skills for AI memory management. Works with [Basic Memory](https://github.com/basicmachines-co/basic-memory) and the [`@openclaw/basic-memory`](https://github.com/basicmachines-co/openclaw-basic-memory) plugin.

## Skills

### memory-tasks

Structured task tracking that survives context compaction. Creates typed `Task` notes with steps, status, and context — queryable via the BM knowledge graph and validatable against a Picoschema definition.

**When to use:** Multi-step work (3+ steps), anything that might outlast a context window, or after compaction to resume.

### memory-schema

Schema lifecycle management for Basic Memory. Covers discovering unschemaed notes, inferring schemas, creating/editing definitions, validating notes, and detecting drift.

**When to use:** When structured note types emerge (Task, Person, Meeting, etc.) and you want consistency across the knowledge graph.

### memory-reflect

Sleep-time memory reflection. Reviews recent conversations and daily notes, extracts insights, and consolidates into long-term memory.

Inspired by [sleep-time compute](https://www.letta.com/blog/sleep-time-compute) — memory formation works best *between* active sessions, not during them.

**When to use:** Schedule via cron (1-2x daily), trigger from heartbeat, or run on demand.

### memory-defrag

Memory defragmentation. Reorganizes memory files: splits bloated ones, merges duplicates, removes stale information, restructures the hierarchy.

**When to use:** Run weekly/biweekly via cron, or on demand when memory feels messy.

## Installation

### Bundled with the plugin (recommended)

If you use the [`@openclaw/basic-memory`](https://github.com/basicmachines-co/openclaw-basic-memory) plugin, all 4 skills are bundled automatically — no extra install step needed.

### Via npx skills

Install or update skills using the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills
npx skills add basicmachines-co/basic-memory-skills --agent openclaw

# Install a specific skill
npx skills add basicmachines-co/basic-memory-skills --name memory-tasks --agent openclaw
```

### Manual install

```bash
cp -r memory-tasks ~/.openclaw/skills/
cp -r memory-reflect ~/.openclaw/skills/
cp -r memory-defrag ~/.openclaw/skills/
cp -r memory-schema ~/.openclaw/skills/
```

Use `~/.openclaw/skills/` for global (shared across workspaces) or `skills/` in your project directory for project-scoped.

## Works With

- **Basic Memory plugin** — full knowledge graph search + schema validation + indexing
- **Plain OpenClaw** — works with native memory files (MEMORY.md, memory/)
- **Any markdown-based memory** — skills operate on plain text files

## Development

See [DEVELOPMENT.md](./DEVELOPMENT.md) for testing and plugin integration details.

## License

MIT
