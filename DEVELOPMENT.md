# Development

## Repository Structure

```
basic-memory-skills/
├── memory-tasks/SKILL.md      # Task tracking skill
├── memory-reflect/SKILL.md    # Memory consolidation skill
├── memory-defrag/SKILL.md     # Memory cleanup skill
├── memory-schema/SKILL.md     # Schema lifecycle skill
└── README.md
```

Each skill is a single `SKILL.md` file with YAML frontmatter (`name`, `description`) and markdown instructions.

## Plugin Integration

These skills are bundled in the [`@openclaw/basic-memory`](https://github.com/basicmachines-co/openclaw-basic-memory) plugin. The plugin copies skill files into its `skills/` directory and declares them in `openclaw.plugin.json`:

```json
{
  "skills": [
    "skills/memory-tasks",
    "skills/memory-reflect",
    "skills/memory-defrag",
    "skills/memory-schema"
  ]
}
```

When updating skills here, also copy the updated files to the plugin repo:

```bash
# From the plugin repo root
cp ../basic-memory-skills/memory-tasks/SKILL.md skills/memory-tasks/
cp ../basic-memory-skills/memory-reflect/SKILL.md skills/memory-reflect/
cp ../basic-memory-skills/memory-defrag/SKILL.md skills/memory-defrag/
cp ../basic-memory-skills/memory-schema/SKILL.md skills/memory-schema/
```

Users can also update skills independently via [npx skills](https://github.com/vercel-labs/skills):

```bash
npx skills add basicmachines-co/basic-memory-skills --agent openclaw
```

## Testing the Plugin Install

### Prerequisites

- Basic Memory CLI (`bm`) installed
- OpenClaw installed with plugin support
- `bun` available

### Install the plugin locally

```bash
git clone https://github.com/basicmachines-co/openclaw-basic-memory.git
cd openclaw-basic-memory
bun install
openclaw plugins install -l "$PWD"
```

### Configure OpenClaw

```json5
{
  plugins: {
    entries: {
      "basic-memory": { enabled: true }
    },
    slots: {
      memory: "basic-memory"
    }
  }
}
```

### Restart and verify

```bash
openclaw gateway stop && openclaw gateway start
```

### Test Checklist

#### Plugin loads
```bash
openclaw plugins list
openclaw plugins info basic-memory
```
- [ ] Plugin appears in list
- [ ] Plugin shows as enabled with memory slot

#### Bundled skills load
```bash
openclaw skills list
```
- [ ] `memory-tasks` appears
- [ ] `memory-reflect` appears
- [ ] `memory-defrag` appears
- [ ] `memory-schema` appears

#### Task schema seeded on first startup

After first startup with the plugin enabled:
- [ ] `memory/schema/Task.md` exists in the project directory
- [ ] Schema has `type: schema` and `entity: Task` in frontmatter
- [ ] Schema includes expected fields (description, status, steps, current_step, context, etc.)

#### Schema not overwritten on restart

1. Edit `memory/schema/Task.md` — add a comment or custom field
2. Restart gateway
3. Check the file
- [ ] Custom edit is preserved

#### Schema validation works

1. Create a task note via the agent or `bm_write`
2. Run `bm_schema_validate({ noteType: "Task" })`
- [ ] Validation runs without errors
- [ ] Task note passes validation

#### npx skills update path
```bash
npx skills add basicmachines-co/basic-memory-skills --agent openclaw
```
- [ ] Skills install/update successfully
- [ ] Updated skills picked up on next session

## Adding a New Skill

1. Create a new directory: `memory-<name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description`
3. Write skill instructions in markdown
4. Update the plugin repo:
   - Copy `SKILL.md` to `skills/memory-<name>/`
   - Add path to `skills` array in `openclaw.plugin.json`
5. Commit and push both repos
