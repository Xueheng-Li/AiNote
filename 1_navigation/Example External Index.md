---
created: 2025-01-01
tags:
  - type/index
---

# External Resource Index

This note indexes files stored outside this vault.

## Structure

```
/path/to/external/folder/
├── subfolder1/
│   ├── file1.pdf
│   └── file2.docx
└── subfolder2/
    └── data.xlsx
```

## Quick Reference

| Resource | Path | Description |
|----------|------|-------------|
| Project Files | `/path/to/projects/` | Main project documents |
| Archives | `/path/to/archives/` | Historical records |

## Search Patterns

```bash
# Find PDFs
**/*.pdf

# Find recent files
find /path -mtime -7
```
