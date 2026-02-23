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

### memory-notes

How to write well-structured Basic Memory notes. Covers frontmatter, observations with semantic categories, relations with wiki-links, inline references, memory URLs, and best practices for building a rich knowledge graph.

**When to use:** When creating or improving notes, or when you need a reference for the note format.

### memory-metadata-search

Structured metadata search for Basic Memory. Query notes by custom frontmatter fields using equality, range, array, and nested filters instead of free-text content.

**When to use:** When finding notes by status, priority, confidence, or any custom YAML field rather than free-text content.

### memory-defrag

Memory defragmentation. Reorganizes memory files: splits bloated ones, merges duplicates, removes stale information, restructures the hierarchy.

**When to use:** Run weekly/biweekly via cron, or on demand when memory feels messy.

### memory-lifecycle

Entity lifecycle management. Handles status transitions through folder-based organization — archiving completed work, moving entities between status folders, updating frontmatter, and reverting mistakes. Core principle: archive, never delete.

**When to use:** When marking items complete, archiving old entities, or managing any folder-based status workflow.

### memory-ingest

Process unstructured external input into structured Basic Memory entities. Parses meeting transcripts, conversation logs, and pasted documents — extracts entities, searches for existing matches, proposes new entities with approval, and captures action items.

**When to use:** When pasting a meeting transcript, conversation log, or any external document that should become structured knowledge.

### memory-research

Web research synthesized into Basic Memory entities. Researches a subject using web search, checks for existing knowledge, presents structured findings, and creates an entity note with approval.

**When to use:** When asked to research a company, person, technology, or topic — or when a bare name or URL implies a research request.

## Installation

### Bundled with the plugin (recommended)

If you use the [`@openclaw/basic-memory`](https://github.com/basicmachines-co/openclaw-basic-memory) plugin, all 9 skills are bundled automatically — no extra install step needed.

### Via npx skills

Install or update skills using the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills
npx skills add basicmachines-co/basic-memory-skills

# Install a specific skill
npx skills add basicmachines-co/basic-memory-skills --skill memory-tasks

# Install all skills for a specific agent
npx skills add basicmachines-co/basic-memory-skills --agent claude

# List available skills without installing
npx skills add basicmachines-co/basic-memory-skills --list

# Check for updates
npx skills check

# Update installed skills
npx skills update
```

Skills are installed to your agent's skills directory (e.g., `~/.claude/skills/` for Claude Code global, or `.claude/skills/` for project-scoped).

### Manual install

```bash
cp -r memory-tasks ~/.openclaw/skills/
cp -r memory-notes ~/.openclaw/skills/
cp -r memory-reflect ~/.openclaw/skills/
cp -r memory-defrag ~/.openclaw/skills/
cp -r memory-schema ~/.openclaw/skills/
cp -r memory-metadata-search ~/.openclaw/skills/
cp -r memory-lifecycle ~/.openclaw/skills/
cp -r memory-ingest ~/.openclaw/skills/
cp -r memory-research ~/.openclaw/skills/
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
