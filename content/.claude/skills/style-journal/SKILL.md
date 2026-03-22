---
name: style-journal
description: Style a D&D character journal page by adding header links, wikilinks to known entities, and section breaks. Use when creating or editing journal entries.
argument-hint: [path-to-journal.md]
allowed-tools: Read, Edit, Write, Glob, Grep
---

You are styling a D&D journal page for a Quartz wiki. The journal file is `$ARGUMENTS`.

Read the file first, then apply the following transformations in order.

## 1. Header Links

Every journal page MUST start with exactly 4 lines of navigation links before any content:

```
[[YYYY]]
[[MM-YYYY]]
[[DD-MM-YYYY]]
[[Character Name]]
```

- Derive the date from the filename (format: `CharacterName DD-MM-YYYY.md`)
- Derive the character name from the filename or containing folder name
- If these header lines already exist, leave them as-is. Do not duplicate them.
- There should be a blank line after the character name link before the journal content begins.

## 2. Auto-link Known Entities

Scan the journal text and add `[[wikilinks]]` to recognized entities. Use `[[Page Name|Display Text]]` when the display text differs from the page name.

Before linking, verify the target page exists by checking the project files. Use Glob to confirm.

**Only link the first occurrence** of each entity in the journal. Do not over-link — repeated mentions should stay as plain text.

Do NOT link an entity if it is already linked nearby, and do NOT nest links inside existing links.

### Known Entity Categories

Search the project for pages matching these directories to find linkable entities:

- `Characters/**/*.md` — player characters and NPCs
- `Locations/**/*.md` — places, cities, regions, kingdoms
- `Factions/**/*.md` or `Organizations/**/*.md` — orders, guilds, factions
- `Religions/**/*.md` — faiths and religious groups
- `Bestiary/**/*.md` — creatures and monsters
- `History/**/*.md` — historical events

### Common Aliases

When linking, use display aliases that match how the character's author refers to them. Common patterns from existing journals:

| Page Name | Common Aliases |
|---|---|
| William Cromwell | William, Scot, the Scot |
| Frigg Oden | Frigg, Pagan, the Pagan |
| Allistair Ashworth | Allistair, Singer, the Singer |
| Kunrad Valencius | Kunrad |
| Baldwin Greystone | Baldwin |
| Islam | Saracen, Saracens |
| Order of the Radiant Cross | Radiant Cross, Order (when context is clear) |
| Order Of the Black Hand | Black Hand |

Use the alias as display text: `[[Frigg Oden|Pagan]]`, `[[Islam|Saracen]]`, etc. If the text already uses the exact page name, a simple `[[Page Name]]` is fine.

## 3. Section Breaks

If the journal is long enough (roughly more than 3-4 paragraphs), add `## Section Title` headers to break it into logical sections.

- Choose short, descriptive titles that reflect the events in that section (e.g., `## Morning`, `## The Riots`, `## The Interrogation`, `## Back at the Castle`)
- Place headers at natural narrative breaks — changes in time, location, or activity
- Do NOT add section breaks to short journals (1-3 paragraphs). Leave them as continuous text.
- If section breaks already exist, leave them as-is unless they need adjustment.

## 4. Final Checks

- Preserve the author's voice and writing style exactly. Do NOT rewrite, rephrase, or edit the journal content itself.
- Do not add YAML frontmatter.
- Do not add trailing whitespace to lines.
- Ensure there is a single newline at the end of the file.
