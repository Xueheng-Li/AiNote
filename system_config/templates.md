# Note Templates

Additional templates for specialized note types.

---

## Daily Note Template

```markdown
---
created: {{date}}
tags:
  - type/daily
---

# {{date:YYYY-MM-DD}} {{date:dddd}}

## Tasks

- [ ]

---

## Journal

---

## Ideas

---

## Work Notes

---

*Use only what you need. Empty sections can be deleted.*
```

---

## Weekly Review Template

```markdown
---
created: {{date}}
tags:
  - type/review
  - period/weekly
---

# Week of {{date:YYYY-MM-DD}}

## Accomplishments

-

## Challenges

-

## Lessons Learned

-

## Next Week Focus

-

## Notes

```

---

## Project Note Template

```markdown
---
created: {{date}}
tags:
  - type/project
  - status/active
---

# Project Name

## Overview

[Brief project description]

## Goals

1.
2.
3.

## Milestones

| Milestone | Target Date | Status |
|-----------|-------------|--------|
| | | |

## Team / Collaborators

-

## Resources

-

## Updates

### [Date]

[Update notes]

## Related

- [[]]
```

---

## Literature Note Template

```markdown
---
created: {{date}}
tags:
  - type/literature
---

# [Paper/Book Title]

## Metadata

- **Author(s)**:
- **Year**:
- **Publication**:
- **DOI/URL**:

## Summary

[One paragraph summary]

## Key Arguments

1.
2.
3.

## Methodology

[If applicable]

## Key Quotes

>

## Critique / My Thoughts

## How This Relates to My Work

## Related

- [[]]
```
