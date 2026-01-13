# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Purpose

AI-Native Note-Taking System. Claude Code processes every note input through analysis, filing, and integration using Obsidian features.

## Note Processing Workflow

1. **Analyze** - Topic, keywords, note type
2. **Context** - Read Personal Profile (if exists); for research notes, read source files first
3. **Search** - Find related notes for linking
4. **Place** - Select subfolder; **ASK USER** if uncertain
5. **Create/Update** - Write with links, tags, formatting
6. **Connect** - Add `links`; suggest MoC for 5+ related notes
7. **Report** - Confirm actions and connections made

## Folder Structure

```text
ai-takenote/
├── 0_inbox/          # Inbox for unprocessed notes
├── 1_navigation/     # External file index (optional)
├── 2_ideas/          # Ideas, thoughts, AI notes
├── 3_profile/        # Personal profile & status
├── 4_teaching/       # Teaching materials
├── 5_meetings/       # Meeting notes
├── 6_research/       # Research notes
├── 7_admin/          # Admin reports
├── 8_code/           # Code snippets
├── 9_attachments/    # Attachments (images, PDFs)
├── 10_bookmarks/     # Web bookmarks
├── workspace/        # Temp files & AI outputs
└── system_config/    # System config & lessons
```

**Root Directory Rule**: Only `CLAUDE.md` belongs at root level. All other files MUST go into subfolders.

## Obsidian Features

### Wiki Links `[[]]`

- **Only link existing notes** - Do not create empty links for institutions, concepts, or journals unless the note exists or user requests creation
- **Aliases** - `display text` for custom display text
- **Headings** - `[[note name#section]]` for precise references

### Tags `#`

Use sparingly. Primary tags in frontmatter (type, status); contextual tags inline.

```text
#type/idea    #type/reference    #status/draft    #project/main
```

### Maps of Content

For topics with 5+ related notes, create a MoC note (e.g., `Topic MOC.md`) as a navigation hub.

### Folder Index Files

Each folder contains an `_index.md` file with one-sentence descriptions for each note.

## Note Format Standard

```markdown
---
created: YYYY-MM-DD
tags:
  - type/idea
  - status/draft
aliases: [alternative name]
---

# Title

[Content with natural wiki links to related concepts]

## Related

- Related Note 1

## Source

[If applicable: URL, paper citation, origin]
```

## Quick Commands

- **Raw text**: Process and file automatically
- **`@inbox`**: Force placement in inbox folder for manual review
- **`@merge note name`**: Integrate content into existing note
- **`@type:[category]`**: Override automatic categorization
- **`@link note`**: Explicitly request linking to specific note

## Safety Rules

- Confirm before merging/modifying existing notes
- Never delete content without permission
- Preserve original input
- Show proposed links/tags before applying
- Only read (don't modify) files outside this vault

## Workspace Folder

For AI-generated scripts, pipeline processing, and intermediate results. Use prefixes: `temp_`, `pipeline_`, `script_`, `draft_`, `test_`. Review and clean regularly; move important results to proper folders.

## Continuous Improvement

Capture reusable insights in `system_config/lessons_learned.md`. Read it before applying learned preferences.

## Customization

### Personalization Steps

1. Edit `3_profile/Personal Profile.md` with your information
2. Customize folder names to match your workflow
3. Add your own quick commands in this file
4. Update `system_config/lessons_learned.md` as you work

### Optional Subagents

You can configure custom subagents in your Claude Code settings for specialized tasks (e.g., academic writing, meeting summarization).

## Documentation Maintenance

Update this file whenever the vault's directory structure changes.
