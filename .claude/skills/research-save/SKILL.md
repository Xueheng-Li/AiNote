---
name: research-save
description: Use this skill when the user asks to "research and save [topic]", "deep dive [topic] and save", "research [topic] to vault", "save research on [topic]", "研究并保存 [主题]", "深度研究 [主题]", "研究 [主题] 到笔记库", "保存关于 [主题] 的研究", "note this down", "记下来", "save to vault", "保存到笔记库", "turn this into a note", "make a research note", or mentions keywords like "研究保存", "深度研究并记录", "research to notes", "save findings to vault", "research-save". This skill conducts comprehensive web research (via a general-purpose subagent, or inline web tools as fallback) and creates properly integrated notes in the vault, saving 30-60 minutes of manual research and formatting work. Supports auto-merge for duplicate topics and handles low-quality results with incomplete status tags.
version: 0.1.0
---

# Research Save Skill

Conduct deep web research on academic/professional topics and create properly integrated notes in the Obsidian vault. Saves 30-60 minutes of manual research and formatting work.

## Arguments

Parse from `$ARGUMENTS`:
- `<主题>`: **Required**. The research topic (Chinese or English)
- `--folder <文件夹>`: Optional. Override default folder (default: `6_研究/`)
- `--link [[笔记]]`: Optional. Explicitly link to specified note(s) (can be used multiple times)

## Workflow

### Phase 1: Pre-validation

1. **Confirm current date/time**:
   ```bash
   date "+%Y-%m-%d %H:%M"
   ```

2. **Check for existing notes on topic** (duplicate detection):
   - Search vault for notes matching the topic using Glob and Grep
   - Search locations: `6_研究/`, `2_AI/`, `3_背景/`
   - Exclude `_index.md` and `CLAUDE.md` from matches
   - If duplicate found with >70% topic overlap, switch to **Auto-merge Mode**

3. **Read research context** from `3_背景/`:
   - Check `3_背景/Research Status.md` or similar for current research priorities
   - This helps contextualize the research within the user's academic focus

### Phase 2: Web Research

This phase must work on any machine, so it does **not** depend on a custom
subagent type. Pick the first option that is available:

**Option A — Delegate to a research subagent (preferred).**
Use the `general-purpose` subagent type (always available in Claude Code). If a
dedicated research agent such as `web-researcher` exists on this machine, you may
use it instead — but never assume it exists.

```
Task(
  subagent_type: "general-purpose",   # portable default; swap only if a research agent is known to exist
  prompt: """
  Think hard and conduct deep web research on the topic below.

  Research topic: [topic]

  Use whatever web tools are available (Tavily MCP, Metaso MCP, WebSearch,
  WebFetch, etc.). Do NOT rely on any specific tool being present — fall back
  to whatever this environment provides.

  Requirements:
  - Find 10+ authoritative sources
  - Prioritize: academic papers, official reports, reputable institutions
  - Cross-verify key claims across multiple sources
  - Structure findings with clear sections
  - Include full citations with URLs

  Save your full findings to a file and return only the file path plus a short
  status summary (do not return the entire report to the caller).

  Output format (in the saved file):
  1. Executive summary (200-300 words)
  2. Main findings (organized by 3-5 subtopics)
  3. Key data points, statistics, and quotes
  4. Source list with credibility notes
  5. Suggested tags and keywords
  """
)
```

**Option B — Research directly (fallback when subagents are unavailable).**
If you cannot spawn a subagent, do the research yourself in the main loop using
whatever web tools exist (`WebSearch` / `WebFetch` are always available; prefer
Tavily/Metaso MCP if configured). Aim for the same 10+ sources and cross-verified
findings, then proceed to Phase 3.

### Phase 3: Related Note Discovery

1. **Search vault folders** for related concepts:
   - Use Grep to search `6_研究/`, `2_AI/`, `3_背景/` for topic keywords
   - Read `_index.md` files to identify related notes by description

2. **Compile related notes list**:
   - Identify at least 3 notes for wiki linking
   - Only include notes that actually exist (no speculative links)

3. **Check for MoC candidates**:
   - If 5+ related notes found, suggest creating a Map of Content

### Phase 4: Note Generation

Create note following vault standards:

```markdown
---
created: [YYYY-MM-DD]
tags:
  - type/research
  - status/draft
  - topic/[main-topic]
aliases: [alternative names, English name, 中文别名]
---

# [Research Title]

> **Summary**: [200-300 word standalone executive summary of key findings]

---

## Research Background

[Why this topic matters, context, relevance to user's research]

## Main Findings

### [Subtopic 1]
[Comprehensive findings with data, quotes, analysis]

### [Subtopic 2]
[Comprehensive findings with data, quotes, analysis]

### [Subtopic 3]
[Additional subtopics as needed]

## Key Data

| Metric | Data | Source |
|--------|------|--------|
| ... | ... | ... |

## Core Conclusions

[Synthesized insights and implications]

---

## Related

- [[Related Note 1]]
- [[Related Note 2]]
- [[Related Note 3]]
[Include --link specified notes here]

## References

1. [Source Title 1](URL1)
2. [Source Title 2](URL2)
... (10+ sources)

---

*Research Date: [YYYY-MM-DD]*
```

**Quality Requirements**:
- Word count: 1500+ words (comprehensive coverage)
- Sources: 10+ authoritative sources with full citations
- Standalone summary at beginning: 200-300 words
- Wiki links: 3+ links to existing vault notes

### Phase 5: Vault Integration

1. **Determine target folder**:
   - Use `--folder` if specified
   - Default: `6_研究/`
   - Ask user if uncertain (per vault rules)

2. **Generate filename**:
   - Use topic as filename (Chinese topics use Chinese filenames)
   - Sanitize special characters
   - If duplicate name exists, add date suffix: `Topic_2026-01-05.md`

3. **Save note**:
   - Write to: `<vault-root>/[folder]/[filename].md` (vault root = the current project directory, the folder containing `CLAUDE.md`)

4. **Update folder index**:
   - Append to `[folder]/_index.md`:
   ```markdown
   - [[New Note Name]]: One-sentence description of research findings.
   ```

5. **Report results**:
   - File path created
   - Word count
   - Number of sources cited
   - Wiki links created
   - Suggested follow-up actions

## Auto-Merge Mode

When duplicate note is detected:

1. **Show existing note summary** to user:
   - Display filename and first 500 characters
   - "Found existing note: [[note name]]. Auto-merging new research..."

2. **Merge strategy**:
   - Preserve original frontmatter, update `modified` date
   - Add new research sections under "## Research Update [Date]"
   - Append new sources to References section
   - Add new related notes to Related section
   - Update summary if new findings are significant

3. **Report merge results**:
   - Original file path
   - Sections added/updated
   - New sources integrated
   - Word count increase

## Low Quality Fallback

If research yields insufficient quality results (< 5 authoritative sources):

1. **Save note with incomplete status**:
   - Add `#status/incomplete` tag instead of `#status/draft`
   - Document gaps in note body

2. **Add limitations section**:
   ```markdown
   ## Limitations

   > **Note**: This research yielded fewer authoritative sources than expected.
   > Consider: [specific gaps identified]
   > Suggested follow-up: [recommendations for manual research]
   ```

3. **Report incomplete status** to user with recommendations

## Quick Reference

| Scenario | Command Example |
|----------|-----------------|
| Basic research | `research and save quantum computing` |
| Chinese topic | `研究并保存 行为经济学` |
| Custom folder | `research AI ethics --folder 2_AI/` |
| Explicit link | `deep dive game theory --link [[博弈论MOC]]` |
| Multiple links | `研究保存 实验经济学 --link [[Research Portfolio]] --link [[博弈论]]` |

## Vault Path

The vault root is the current project directory (the folder containing
`CLAUDE.md`). Use paths relative to it; never hardcode an absolute path.

## Related Documentation

- [[references/research-quality]] - Source evaluation criteria
- [[references/merge-patterns]] - Duplicate handling details
- [[references/vault-integration]] - Note format standards
- [[examples/basic-usage]] - Simple examples
- [[examples/advanced-usage]] - Complex scenarios
