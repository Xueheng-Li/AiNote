# Basic Usage Examples

Simple examples for using the research-save skill.

## Example 1: English Topic

**User input:**
```
research and save quantum computing applications
```

**What happens:**
1. Skill confirms current date
2. Checks for existing quantum computing notes in vault
3. Delegates research to a `general-purpose` subagent (or does it inline if no subagent is available)
4. Creates comprehensive note at `6_研究/quantum computing applications.md`
5. Updates `6_研究/_index.md`
6. Reports: file path, 1800 words, 12 sources, 4 wiki links

**Output location:** `6_研究/quantum computing applications.md`

---

## Example 2: Chinese Topic

**User input:**
```
研究并保存 大语言模型在社会科学研究中的应用
```

**What happens:**
1. Date confirmation
2. Searches for existing LLM/social science notes
3. Web research with Chinese and English sources
4. Creates note at `6_研究/大语言模型在社会科学研究中的应用.md`
5. Links to related notes like `[[AI研究]]`, `[[Research Portfolio Analysis]]`

**Output location:** `6_研究/大语言模型在社会科学研究中的应用.md`

---

## Example 3: Alternative Trigger Phrases

All of these work the same way:

```
# English variants
research and save climate economics
deep dive carbon pricing and save
research carbon markets to vault
save research on emissions trading

# Chinese variants
研究并保存 碳市场
深度研究 碳定价机制
研究 碳交易 到笔记库
保存关于 气候经济学 的研究
```

---

## Example 4: Short Topic

**User input:**
```
research and save RLHF
```

**What happens:**
1. Skill understands RLHF = Reinforcement Learning from Human Feedback
2. Researches the full topic comprehensively
3. Creates `6_研究/RLHF.md` with aliases including "Reinforcement Learning from Human Feedback"
4. Finds related notes on AI, machine learning

---

## Expected Output Report

After successful research:

```
✓ Research completed: RLHF

File created: 6_研究/RLHF.md
Word count: 1,650 words
Sources: 11 authoritative sources
Wiki links:
  - [[AI研究]]
  - [[Machine Learning MOC]]
  - [[Research Portfolio Analysis]]
Index updated: 6_研究/_index.md

Suggested next steps:
- Review and upgrade to #status/active when verified
- Consider creating [[AI Training Methods MOC]] (5 related notes found)
```

---

## What Makes a Good Topic

**Good topics:**
- Specific enough for focused research: "transformer attention mechanisms"
- Clear academic/professional relevance: "behavioral economics in policy design"
- Defined scope: "AI governance in EU vs US"

**Topics that might need refinement:**
- Too broad: "artificial intelligence" → suggest narrowing
- Too narrow: "specific paper X findings" → manual approach better
- Breaking news: "today's announcement" → wait for analysis or use manual approach
