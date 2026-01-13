# 🤖 AI-Native Note-Taking System

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/Xueheng-Li/AiNote)

An AI-powered note-taking system designed for use with [Claude Code](https://claude.com/claude-code) and [Obsidian](https://obsidian.md/).

## 🎯 Overview

This system transforms your note-taking workflow by having Claude Code automatically:

- 🔍 **Analyze** incoming notes for topics, keywords, and type
- 📁 **File** notes into appropriate folders
- 🔗 **Connect** notes with wiki links to related content
- 📋 **Maintain** folder indexes and Maps of Content
- 🧠 **Learn** your preferences over time

---

## ⚡ The Soul: CLAUDE.md

> 💡 **`CLAUDE.md` is the brain and soul of this entire system.** It contains all the instructions that guide Claude Code's behavior when processing your notes.

- Every note you create flows through the workflow defined in `CLAUDE.md`
- It defines folder structure, note formats, linking rules, and safety protocols
- Customize it to make the system truly yours
- The better your `CLAUDE.md`, the smarter your note-taking becomes

**Think of `CLAUDE.md` as the "operating system" for your AI-native notes.**

---

## 🚀 Quick Start

### 1️⃣ Setup

1. Copy the `ai-takenote/` folder to your desired location
2. Open the folder as an Obsidian vault
3. Edit `3_profile/Personal Profile.md` with your information
4. Start using Claude Code within the vault directory

### 2️⃣ Basic Usage

Use the `/takenote` slash command:

```
/takenote Here's a research idea about network effects in social media platforms...
```

Or simply give Claude Code your raw note content directly.

Claude Code will:
1. 🔍 Analyze the content
2. 📝 Create a properly formatted note
3. 📂 Place it in the appropriate folder (e.g., `6_research/`)
4. 🏷️ Add relevant tags and links
5. ✏️ Update the folder's `_index.md`

### 3️⃣ Slash Command

The `/takenote` command triggers the full note-processing workflow:

```
/takenote <your note content>
```

### 4️⃣ Modifiers

Add modifiers to control note placement:

- **`@inbox`** 📥 — Force placement in inbox for manual review
- **`@merge note name`** 🔄 — Integrate into existing note
- **`@type:[category]`** 📂 — Override automatic categorization
- **`@link note`** 🔗 — Request specific linking

Example:
```
/takenote @type:research New findings on behavioral economics...
```

## 📁 Folder Structure

```
ai-takenote/
├── .claude/
│   └── commands/
│       └── takenote.md # /takenote slash command
├── CLAUDE.md           # 🧠 AI instructions (THE SOUL - core config)
├── README.md           # 📖 This file
├── 0_inbox/            # 📥 Unprocessed notes
├── 1_navigation/       # 🗺️ External resource indexes
├── 2_ideas/            # 💡 Ideas and thoughts
├── 3_profile/          # 👤 Personal profile & status
├── 4_teaching/         # 🎓 Teaching materials
├── 5_meetings/         # 🤝 Meeting notes
├── 6_research/         # 🔬 Research notes
├── 7_admin/            # 📊 Administrative docs
├── 8_code/             # 💻 Code snippets
├── 9_attachments/      # 📎 Images, PDFs, files
├── 10_bookmarks/       # 🔖 Web bookmarks
├── workspace/          # 🛠️ Temp & AI outputs
└── system_config/      # ⚙️ System configuration
```

## ✨ Key Features

### 🔷 Obsidian Integration

- **Wiki Links** 🔗 — `note name` for internal linking
- **Aliases** 🏷️ — `display text` for custom display
- **Tags** 📌 — `#type/idea`, `#status/draft`, `#project/main`
- **Frontmatter** 📋 — YAML metadata for each note

### 📑 Folder Indexes

Each folder contains an `_index.md` with one-sentence descriptions of all notes. Claude Code maintains these automatically.

### 🗺️ Maps of Content

When 5+ notes relate to a topic, Claude Code suggests creating a Map of Content (MoC) as a navigation hub.

### 📈 Continuous Learning

`system_config/lessons_learned.md` stores insights about your preferences, making the system smarter over time.

## 🎨 Customization

### 📂 Rename Folders

Update both the folder names and the structure in `CLAUDE.md`.

### ➕ Add Custom Commands

Add new quick commands to the "Quick Commands" section in `CLAUDE.md`.

### 🤖 Configure Subagents

For specialized tasks (academic writing, meeting summarization), configure custom subagents in your Claude Code settings.

### 🌐 Localization

Folder names and templates can be translated to any language. Update `CLAUDE.md` accordingly.

## 📦 Requirements

- [Obsidian](https://obsidian.md/) (recommended for viewing/editing)
- [Claude Code](https://claude.com/claude-code) CLI tool
- Claude API access

## 🛡️ Safety Features

- ✅ Confirms before modifying existing notes
- 🚫 Never deletes content without permission
- 💾 Preserves original input
- 👀 Shows proposed changes before applying

## 💡 Tips

1. **Start Simple** 🌱 — Use raw text input and let Claude Code handle organization
2. **Review Inbox** 📥 — Periodically check `0_inbox/` for items needing attention
3. **Build Links** 🔗 — The more you link, the more valuable your knowledge graph becomes
4. **Update Profile** 👤 — Keep `3_profile/` current for better AI context
5. **Clean Workspace** 🧹 — Regularly move valuable items from `workspace/` to proper folders

## 👨‍💻 Author

[Xueheng Li](https://github.com/Xueheng-Li)

## 📜 License

MIT License — Feel free to modify and distribute.

## 🤝 Contributing

Contributions welcome! Please submit issues and pull requests on [GitHub](https://github.com/Xueheng-Li/ai-takenote).

---

<p align="center">
Made with ❤️ by <a href="https://github.com/Xueheng-Li">Xueheng Li</a>
</p>
