# Merge Patterns

Duplicate detection and auto-merge logic for the research-save skill.

## Duplicate Detection

### Search Strategy

1. **Exact match search**:
   ```
   Glob("6_研究/**/*.md") + Glob("2_AI/**/*.md") + Glob("3_背景/**/*.md")
   ```
   Then filter by filename containing topic keywords.

2. **Content match search**:
   ```
   Grep(pattern: "[topic keywords]", path: "6_研究/")
   ```
   Check for notes with substantial topic overlap.

3. **Exclusions**:
   - Skip `_index.md` files
   - Skip `CLAUDE.md` files
   - Skip files in `临时工作区/`

### Overlap Calculation

A note is considered a duplicate when:
- Filename contains >50% of topic keywords, OR
- First 500 words contain >70% overlap with search terms

### Detection Results

| Result | Action |
|--------|--------|
| No match | Proceed with new note creation |
| Single match | Auto-merge into existing note |
| Multiple matches | Ask user which note to merge into |

## Auto-Merge Strategy

### Preserve Original Structure

1. **Frontmatter**:
   - Keep original `created` date
   - Add `modified: [current date]`
   - Merge tags (add new, keep existing)
   - Merge aliases (add new, keep existing)

2. **Original content**:
   - Preserve all existing sections
   - Do not modify original text

### Add New Research

1. **Insert update marker**:
   ```markdown
   ---

   ## Research Update: [YYYY-MM-DD]

   > New research findings integrated from comprehensive web research.
   ```

2. **Add new sections**:
   - Structure new findings under update header
   - Use ### subheadings for organization

3. **Merge references**:
   - Append new sources to existing References section
   - Number continuation: if original has 1-5, new sources start at 6

4. **Update Related**:
   - Add newly discovered related notes
   - Avoid duplicate links

### Merge Template

```markdown
---

## Research Update: 2026-01-05

> New research findings integrated via research-save skill.

### New Findings: [Subtopic]

[New research content]

### Additional Data

| Metric | Data | Source |
|--------|------|--------|
| ... | ... | ... |

### Updated Conclusions

[How new research updates/reinforces original conclusions]

---

## Updated References

6. [New Source 1](URL)
7. [New Source 2](URL)
...

## New Related Notes

- [[Newly Discovered Note]]
```

## Merge Confirmation

For auto-merge mode, provide brief confirmation:

```
Found existing note: [[Existing Note Name]]
Location: 6_研究/Existing Note Name.md
Created: 2025-06-15
Word count: 1234

Auto-merging new research...
✓ Added "Research Update: 2026-01-05" section
✓ Integrated 8 new sources (sources 6-13)
✓ Added 2 new related note links
✓ Updated tags with #topic/new-subtopic
```

## Conflict Resolution

When new research contradicts existing note content:

### Detection
- Compare key claims, statistics, and conclusions
- Flag if new data differs significantly from original

### Resolution Strategy

1. **Preserve both versions** with timestamps:
   ```markdown
   ### [Topic] (Updated View)

   > **Note**: This section updates earlier findings from [original date].

   [New research content with current data]

   <details>
   <summary>Previous findings (for reference)</summary>

   [Original content preserved here]
   </details>
   ```

2. **Add conflict marker** when facts directly contradict:
   ```markdown
   > ⚠️ **Conflicting Information**: New research suggests [X], while
   > the original note stated [Y]. This discrepancy may be due to
   > [temporal changes / methodology differences / source reliability].
   > Manual review recommended.
   ```

3. **Flag for user review**:
   - Add `#needs-review` tag to frontmatter
   - Mention conflict in merge report

### When NOT to Merge

If conflicts are severe (>50% of key claims contradict):
- Suggest creating a new note instead
- Cross-link both notes with conflict context
- Let user decide which to keep as primary

## Edge Cases

| Case | Handling |
|------|----------|
| Very old note (>1 year) | Note recency in update, suggest full rewrite if needed |
| Conflicting information | Use conflict resolution strategy above |
| Same topic, different angle | Create separate note with cross-link |
| Note is a MOC | Add to MOC rather than merge |
| Source reliability changed | Update citations, note credibility shifts |
