# Vault Integration Standards

Note format standards and integration patterns for the Obsidian vault.

## Frontmatter Template

```yaml
---
created: YYYY-MM-DD
tags:
  - type/research
  - status/draft        # or status/incomplete for low-quality fallback
  - topic/[main-topic]  # e.g., topic/ai, topic/behavioral-economics
aliases: [alternative name, English name, 中文别名]
---
```

### Tag Guidelines

**Type tags** (required):
- `type/research` - Standard for research notes

**Status tags** (required):
- `status/draft` - New research, needs review
- `status/incomplete` - Low-quality fallback
- `status/active` - Reviewed and verified (user upgrades)

**Topic tags** (at least one):
- `topic/[category]` - Main topic area
- Use existing tags when possible (check other 6_研究/ notes)

## Wiki Link Rules

From vault CLAUDE.md:
1. **Only link existing notes** - Never create speculative links
2. **Use aliases for readability**: `[[behavioral economics|BE research]]`
3. **Link to headings when specific**: `[[note name#section]]`

### Link Discovery Pattern

```
# Search for linkable notes
Grep("keyword", path="6_研究/", output_mode="files_with_matches")
Grep("keyword", path="2_AI/", output_mode="files_with_matches")
Grep("keyword", path="3_背景/", output_mode="files_with_matches")

# Read _index.md for context
Read("6_研究/_index.md")
```

## Folder Structure

Default placement: `6_研究/`

Other options:
- `2_AI/` - AI-specific research
- `3_背景/` - Personal/career context
- `4_教学/` - Teaching-related research
- Custom via `--folder` argument

## Filename Conventions

1. **Chinese topics**: Use Chinese filename
   - Topic: "行为经济学" → `行为经济学.md`

2. **English topics**: Use English filename
   - Topic: "quantum computing" → `quantum computing.md`

3. **Mixed**: Follow primary language
   - "AI在中国的发展" → `AI在中国的发展.md`

4. **Special characters**: Remove or replace
   - `:` `?` `*` `"` `<` `>` `|` `/` `\` → remove
   - `&` → "and" or "与"

5. **Duplicate names**: Add date suffix
   - `Topic_2026-01-05.md`

## Index Update Pattern

After creating a note, update the folder's `_index.md`:

```markdown
# Append to _index.md

- [[New Note Name]]: One-sentence summary of research findings.
```

### Index Entry Guidelines

- Keep to one line
- Start with key topic/concept
- End with period
- No wiki links within the description

Example:
```markdown
- [[量子计算研究]]: 量子计算原理、当前进展与商业应用前景的综合分析。
- [[AI Ethics Framework]]: Comprehensive analysis of ethical frameworks for AI development and deployment.
```

## Note Template (Complete)

```markdown
---
created: 2026-01-05
tags:
  - type/research
  - status/draft
  - topic/[main-topic]
aliases: [alt name 1, alt name 2]
---

# [Research Title]

> **Summary**: [200-300 word standalone executive summary. This should be
> readable independently and capture the key findings, significance, and
> main conclusions of the research. Written in clear, accessible language.]

---

## Research Background

[Context for why this topic matters. Connection to user's research interests.
Brief literature/knowledge positioning. 150-250 words.]

## Main Findings

### [Subtopic 1: Most Important]

[Comprehensive findings with:
- Key data and statistics
- Expert quotes with attribution
- Analysis and implications
300-400 words per subtopic]

### [Subtopic 2]

[Similar depth as above]

### [Subtopic 3]

[Additional subtopics as needed for comprehensive coverage]

## Key Data

| Metric | Data | Source |
|--------|------|--------|
| [Stat 1] | [Value] | [Source name] |
| [Stat 2] | [Value] | [Source name] |
| [Stat 3] | [Value] | [Source name] |

## Core Conclusions

[Synthesized insights from all findings. Implications for user's research
or professional interests. Potential future directions. 200-300 words.]

---

## Related

- [[Related Note 1]] - Brief context for why related
- [[Related Note 2]]
- [[Related Note 3]]

## References

1. [Author/Org. "Title." Source, Date.](URL)
2. [Author/Org. "Title." Source, Date.](URL)
3. [Author/Org. "Title." Source, Date.](URL)
... (10+ sources)

---

*Research Date: 2026-01-05*
```

## Quality Checklist

Before finalizing note:

- [ ] Frontmatter valid YAML with all required fields
- [ ] Summary is 200-300 words, standalone readable
- [ ] Total word count 1500+
- [ ] 10+ authoritative sources cited
- [ ] 3+ wiki links to existing notes (verified to exist)
- [ ] No broken links or speculative links
- [ ] Filename follows conventions
- [ ] Index entry prepared
