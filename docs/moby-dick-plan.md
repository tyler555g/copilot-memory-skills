# Moby Dick Literary Analysis — Basic Memory Skills Test Case

## Context

Stress-test basic-memory-skills by ingesting a complete literary work (Moby Dick, ~215K words, 135 chapters) into a structured Basic Memory knowledge graph. This exercises multiple skills together — ingest, schema, notes, tasks, metadata-search, lifecycle — at scale. The workflow is documented as a reusable `memory-literary-analysis` skill.

## Deliverables

1. **`memory-literary-analysis/SKILL.md`** — New skill documenting the full literary analysis pipeline
2. **`docs/moby-dick-plan.md`** — This plan document
3. **`moby-dick` Basic Memory project** — The fully populated knowledge graph
4. **Updated `README.md`** — New skill listed in the skills table

---

## Phase 0: Setup

1. Create `moby-dick` Basic Memory project via `create_memory_project`
2. Download full text from Project Gutenberg (`https://www.gutenberg.org/files/2701/2701-0.txt`)
3. Write 6 schema notes to `schema/` directory

### Schemas

| Schema | Key Fields | Observation Categories | Relation Types |
|--------|-----------|----------------------|----------------|
| **Character** | role, description, first_appearance, status, rank, crew_role | `[trait]` `[motivation]` `[arc]` `[quote]` `[appearance]` `[relationship]` `[symbolism]` `[fate]` | appears_in, contrasts_with, allied_with, commands, symbolizes, associated_with |
| **Theme** | description, prevalence, first_introduced | `[definition]` `[manifestation]` `[evolution]` `[counterpoint]` `[quote]` `[interpretation]` | embodied_by, contrasts_with, reinforced_by, explored_in, expressed_through |
| **Chapter** | chapter_number, pov, setting, narrative_mode | `[summary]` `[event]` `[tone]` `[technique]` `[quote]` `[significance]` `[foreshadowing]` | features, set_in, explores, contains, employs, follows, precedes, parallels |
| **Location** | description, location_type, real_or_fictional | `[description]` `[atmosphere]` `[symbolism]` `[significance]` `[geography]` | setting_for, associated_with, symbolizes, contains, part_of |
| **Symbol** | description, symbol_type, primary_meaning | `[meaning]` `[appearance]` `[ambiguity]` `[interpretation]` `[quote]` `[evolution]` | represents, associated_with, appears_in, contrasts_with, located_at |
| **LiteraryDevice** | description, device_type, frequency | `[definition]` `[usage]` `[effect]` `[example]` `[significance]` | used_in, characterizes, expresses, related_to |

### Directory Structure

```
moby-dick/
  schema/            # 6 schema definitions
  chapters/          # 136 chapter notes (135 + epilogue)
  characters/
    major/           # ~15 major characters
    minor/           # ~25 minor characters
  themes/            # ~10 themes
  locations/         # ~10 locations
  symbols/           # ~12 symbols
  literary-devices/  # ~10 device notes
  analysis/          # Cross-cutting synthesis notes
  tasks/             # Processing tracker
```

## Phase 1: Seed Entities

Create stub notes for known major entities before chapter processing:
- **~15 major characters**: Ishmael, Ahab, Queequeg, Starbuck, Stubb, Flask, Tashtego, Daggoo, Pip, Fedallah, Father Mapple, Bildad, Peleg, Elijah, Moby Dick
- **~10 core themes**: Obsession, Nature/Sublime, Fate/Free Will, Race/Class, Knowledge/Limits, Religion/Mythology, Revenge, Isolation, The Unknowable, Masculinity
- **~8 key locations**: The Pequod, Nantucket, New Bedford, Spouter-Inn, The Chapel, Pacific Ocean
- **~8 core symbols**: The White Whale, The Doubloon, The Coffin/Life-Buoy, Whiteness, The Try-Works, Queequeg's Tattoos

## Phase 2: Chapter Processing (batches of ~10)

| Batch | Chapters | Focus |
|-------|----------|-------|
| 1 | 1-9 | Shore: New Bedford, Inn, Chapel, Sermon |
| 2 | 10-23 | Shore: Queequeg, Nantucket, boarding the Pequod |
| 3 | 24-35 | Early voyage, cetology begins |
| 4 | 36-42 | Quarter-Deck, Sunset, Whiteness (pivotal) |
| 5-13 | 43-130 | Groups of ~10, the voyage and encounters |
| 14 | 131-Epilogue | The Chase and aftermath |

Per chapter: `write_note` for chapter note, `edit_note` to enrich related entities.

## Phase 3: Cross-Referencing Pass

1. Enrich character `[arc]` observations with full trajectory summaries
2. Finalize theme `[evolution]` observations
3. Add `parallels` and `contrasts_with` relations between chapters
4. Create 3 analysis notes: narrative-structure, moby-dick-overview, critical-reception
5. Discover and create minor characters/symbols that emerged during processing

## Phase 4: Validation

1. `schema_validate` for all 6 entity types
2. `schema_diff` to check for drift
3. Fix issues via `edit_note`
4. Spot-check bidirectional relation consistency

## Phase 5: Visualization

Generate canvas files via `canvas` tool for character web, theme map, and chapter timeline.

## Expected Output Scale

~221 notes, ~1,815 relations across the knowledge graph.

## Verification

1. `list_directory` on each folder to confirm note counts
2. `schema_validate` passes for all 6 types
3. `build_context` on Ahab returns rich connected context
4. `search_notes` finds notes by metadata filters
5. `canvas` generates meaningful visualizations
6. The skill SKILL.md follows existing skill conventions
