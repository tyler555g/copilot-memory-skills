# basic-memory-skills

Skills for [Basic Memory](https://github.com/basicmachines-co/basic-memory) — teach AI coding agents how to use Basic Memory's MCP tools effectively.

## What Are Skills?

Skills are markdown instruction files (`SKILL.md`) that AI agents load for domain-specific guidance. Each skill contains structured knowledge about *when* and *how* to use specific tools, with examples and best practices.

Basic Memory provides the MCP server — tools like `write_note`, `search_notes`, and `build_context` for managing a local-first knowledge graph. These skills teach agents how to use those tools well: when to create tasks vs. notes, how to structure observations for searchability, when to run schema validation, and more.

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

## Basic Memory Cloud

Everything works locally — cloud adds cross-device, team, and production capabilities:

- **Your agent's memory travels with you** — same knowledge graph on laptop, desktop, and hosted environments
- **Team knowledge sharing** — org workspaces let multiple agents and team members build on a shared knowledge base
- **Durable memory for production agents** — persistent memory that survives CI teardowns and container restarts
- **Multi-agent coordination** — multiple agents can read and write to the same graph

Cloud extends local-first — still plain markdown, still yours. Start with a [7-day free trial](https://basicmemory.com) and use code `BMFOSS` for 20% off for 3 months.

## Installation

### Via npx skills (recommended)

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

### Claude Desktop (claude.ai)

Claude Desktop loads skills through **Settings > Capabilities**:

1. Clone or download this repository
2. In Claude, go to **Settings > Capabilities** and ensure both **Code execution** and **Skills** are enabled
3. Click **Upload skill** and upload the `SKILL.md` file (or ZIP the skill folder and upload that)
4. Toggle the skill on — Claude will use it automatically when relevant

Repeat for each skill you want. Custom uploaded skills are private to your account.

> **Tip:** Start with **memory-notes** (core note-writing patterns) and add others as needed. You don't need all 9 at once.

See [Using Skills in Claude](https://support.claude.com/en/articles/12512180-using-skills-in-claude) for more details.

### Manual install

Copy skill directories into your agent's skills folder:

```bash
# Claude Code — global
cp -r memory-tasks ~/.claude/skills/
cp -r memory-notes ~/.claude/skills/
# ... etc.

# Claude Code — project-scoped
cp -r memory-tasks .claude/skills/

# Any agent that reads SKILL.md files
cp -r memory-tasks <agent-skills-dir>/
```

### Bundled with OpenClaw plugin

All 9 skills are also bundled in the [`@basicmemory/openclaw-basic-memory`](https://github.com/basicmachines-co/openclaw-basic-memory) plugin — no extra install step needed if you use OpenClaw.

## Compatible Agents

These skills work with any AI coding agent that supports the SKILL.md format:

- **Claude Desktop** — upload skill ZIPs via Settings > Capabilities
- **Claude Code** — loads skills from `~/.claude/skills/` or `.claude/skills/`
- **Cursor** — AI-powered coding with skill support
- **Windsurf** — agent-based development with skill loading
- **Any agent** supporting markdown-based skill files

## Development

See [DEVELOPMENT.md](./DEVELOPMENT.md) for testing and contribution details.

## License

MIT
