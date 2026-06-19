---
name: update-vault
description: "Maintain this notebook vault using parallel subagents: refresh all _index.md files across folders, repair or remove broken wiki links, and update CLAUDE.md if the folder structure has changed. Use when the user invokes /update-vault or asks to tidy up / re-index the notebook."
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, Task, TaskOutput, AskUserQuestion
model: sonnet
---

Perform a comprehensive update of this notebook vault using parallel subagents.

The vault is the current project directory (the folder containing `CLAUDE.md`).
All paths below are relative to that root — do not hardcode any absolute or
machine-specific path.

## Phase 0: Set up a tracking list for the phases below.

---

## Phase 1: Date & Structure Check

1. Run `date` for the current timestamp.
2. Scan the actual folder structure and compare it against `CLAUDE.md`.
3. Note any discrepancies for Phase 4.

---

## Phase 2: Parallel Index Updates (up to 10 agents)

Refresh every `_index.md` so it reflects the notes currently in its folder.

**Constraints:**
- Max 10 subagents in parallel.
- Each handles 1-3 folders (balance by size).
- Skip: `.git/`, `.claude/`, `.obsidian/`, `.trash/`, `临时工作区/`.
- Launch all in one message with `run_in_background: true`.

**Process:**
1. Discover all `_index.md` locations (Glob `**/_index.md`).
2. Group folders into balanced batches (≤10).
3. Launch one parallel agent per batch.
4. Collect results with `TaskOutput`.

**Subagent task:** Update the assigned `_index.md` files, preserve the existing
format, and return a row: | Folder | Added | Removed | Status |

**Output:** A master summary table.

---

## Phase 3: Link Analysis

For each broken `[[wiki link]]` (target note does not exist):

1. **Search for a match**: use Grep/Glob to find existing notes with a similar
   name, keyword, or topic.
2. **If a match is found**: repoint the link to the existing note
   (e.g. `[[broken|correct name]]` or a direct `[[correct name]]`).
3. **If no match is found**: remove the wiki-link syntax but keep the text
   (e.g. `[[Broken Link]]` → `Broken Link`).

Report: | Original Link | Action Taken | New Target/Reason |

---

## Phase 4: Update CLAUDE.md

If the folder structure changed, update `CLAUDE.md` to match the current state.

---

## Phase 5: Final Report

```
## Vault Update Report - {DATE}

- Index Updates: {summary}
- Broken Links: {count} or None
- Link Suggestions: {top 5}
- CLAUDE.md: Updated / No changes

### Recommendations
{any maintenance suggestions}
```
