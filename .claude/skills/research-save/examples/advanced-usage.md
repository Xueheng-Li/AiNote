# Advanced Usage Examples

Complex scenarios including folder overrides, explicit linking, and merge situations.

## Example 1: Custom Folder

**User input:**
```
research AI ethics frameworks --folder 2_AI/
```

**What happens:**
1. Research on AI ethics frameworks
2. Note saved to `2_AI/AI ethics frameworks.md` instead of default `6_研究/`
3. Updates `2_AI/_index.md`

---

## Example 2: Explicit Linking

**User input:**
```
deep dive game theory applications --link [[博弈论MOC]] --link [[Research Portfolio Analysis]]
```

**What happens:**
1. Research on game theory applications
2. Note includes specified links in Related section (in addition to auto-discovered links)
3. These links are added regardless of auto-discovery results
4. If linked note doesn't exist, it's skipped with a warning

**Related section in output:**
```markdown
## Related

- [[博弈论MOC]] - explicitly requested
- [[Research Portfolio Analysis]] - explicitly requested
- [[Behavioral Economics]] - auto-discovered
- [[实验经济学]] - auto-discovered
```

---

## Example 3: Auto-Merge Scenario

**User input:**
```
研究并保存 行为经济学实验设计
```

**Existing note found:** `6_研究/行为经济学.md`

**What happens:**
1. Skill detects existing note with high topic overlap
2. Displays notification:
   ```
   Found existing note: [[行为经济学]]
   Location: 6_研究/行为经济学.md
   Created: 2025-08-20 | Words: 1,450

   Auto-merging new research...
   ```
3. Adds new section to existing note:
   ```markdown
   ---

   ## Research Update: 2026-01-05

   > New research on experimental design methods integrated.

   ### Experimental Design Methods

   [New comprehensive research content...]
   ```
4. Appends new sources to References
5. Reports merge results

---

## Example 3b: Merge with Conflict Detection

**User input:**
```
研究并保存 量子计算进展
```

**Existing note found:** `6_研究/量子计算.md` (from 2024)

**What happens:**
1. Skill detects existing note
2. New research reveals some data has changed significantly:
   - Original: "50 qubits achieved by leading labs"
   - New: "1000+ qubits now available commercially"
3. Skill applies conflict resolution:
   ```markdown
   ---

   ## Research Update: 2026-01-05

   > New research on quantum computing progress integrated.

   ### Computing Power (Updated View)

   > **Note**: This section updates earlier findings from 2024-03-15.

   Current state: 1000+ qubit systems now commercially available...

   <details>
   <summary>Previous findings (for reference)</summary>

   Original note stated 50 qubits as the frontier...
   </details>

   > ⚠️ **Significant Progress**: The quantum computing field has
   > advanced rapidly since original research. Original metrics
   > are now outdated.
   ```
4. Adds `#needs-review` tag
5. Report highlights conflict:
   ```
   ✓ Merged into: 6_研究/量子计算.md
   ⚠ Conflict detected: 2 data points significantly outdated
   → Added #needs-review tag for manual verification
   ```

---

## Example 4: Combination Arguments

**User input:**
```
research-save 实验经济学方法论 --folder 6_研究/ --link [[博弈论研究]] --link [[Behavioral Economics]]
```

**What happens:**
1. Research on experimental economics methodology
2. Saved to specified folder `6_研究/`
3. Includes both explicit links
4. Also discovers and adds other related notes

---

## Example 5: Low Quality Fallback

**Scenario:** Research on obscure topic yields only 4 sources

**User input:**
```
research and save ancient Mesopotamian game theory
```

**What happens:**
1. Web research finds limited authoritative sources
2. Skill triggers low quality fallback:
   ```
   ⚠ Limited sources found (4 of 10 target)
   Creating note with #status/incomplete tag...
   ```
3. Note created with modifications:
   - Tag: `#status/incomplete` instead of `#status/draft`
   - Added Limitations section
4. Report includes recommendations:
   ```
   ✓ Note created: 6_研究/ancient Mesopotamian game theory.md
   ⚠ Status: incomplete (4 sources, below 10 threshold)

   Recommendations:
   - Search academic databases manually (JSTOR, Google Scholar)
   - Consult specialized history journals
   - Consider contacting domain experts
   ```

---

## Example 6: Multiple Related Notes (MOC Suggestion)

**User input:**
```
research and save neural network architectures
```

**Related notes found:** 7 notes

**What happens:**
1. Normal research and note creation
2. Additional suggestion in report:
   ```
   ✓ Found 7 related notes:
     - [[深度学习]]
     - [[Transformer研究]]
     - [[AI研究]]
     - [[Machine Learning MOC]]
     - [[CNN应用]]
     - [[RNN与序列模型]]
     - [[注意力机制]]

   💡 Suggestion: Consider creating [[Neural Network Architectures MOC]]
      to organize these related notes.
   ```

---

## Quick Reference Table

| Scenario | Command Pattern |
|----------|-----------------|
| Basic research | `research and save [topic]` |
| Chinese topic | `研究并保存 [主题]` |
| Custom folder | `research [topic] --folder [path]` |
| Single link | `research [topic] --link [[note]]` |
| Multiple links | `research [topic] --link [[note1]] --link [[note2]]` |
| Full options | `research [topic] --folder [path] --link [[note1]] --link [[note2]]` |

## Error Handling

| Error | Skill Response |
|-------|----------------|
| Invalid folder path | "Folder not found. Create it? [Y/n] Or use default 6_研究/" |
| Linked note doesn't exist | "Note [[X]] not found, skipping link. Continue? [Y/n]" |
| Web research fails | "Unable to complete web research. Save partial results? [Y/n]" |
| Topic too broad | "Topic may be too broad. Suggestions: [narrower topics]" |
