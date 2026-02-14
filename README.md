# basic-memory-skills

OpenClaw skills for AI memory management. Works with [Basic Memory](https://github.com/basicmachines-co/basic-memory) or plain OpenClaw memory files.

## Skills

### memory-reflect

Sleep-time memory reflection. Reviews recent conversations and daily notes, extracts insights, and consolidates into long-term memory.

Inspired by [sleep-time compute](https://www.letta.com/blog/sleep-time-compute) — memory formation works best *between* active sessions, not during them.

**When to use:** Schedule via cron (1-2x daily), trigger from heartbeat, or run on demand.

### memory-defrag

Memory defragmentation. Reorganizes memory files: splits bloated ones, merges duplicates, removes stale information, restructures the hierarchy.

**When to use:** Run weekly/biweekly via cron, or on demand when memory feels messy.

## Installation

Copy skill directories into your OpenClaw workspace skills folder, or install via ClawHub (coming soon).

```bash
# Manual install
cp -r memory-reflect ~/.openclaw/workspace/skills/
cp -r memory-defrag ~/.openclaw/workspace/skills/
```

## Works With

- **Basic Memory plugin** — full knowledge graph search + indexing
- **Plain OpenClaw** — works with native memory files (MEMORY.md, memory/)
- **Any markdown-based memory** — skills operate on plain text files

## License

MIT
