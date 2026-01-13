# 🤖 AI 原生笔记系统

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/Xueheng-Li/AiNote)

一个专为 [Claude Code](https://claude.com/claude-code) 和 [Obsidian](https://obsidian.md/) 设计的 AI 驱动笔记系统。

## 🎯 概述

这个系统通过 Claude Code 自动化处理，彻底改变您的笔记工作流：

- 🔍 **分析** 笔记的主题、关键词和类型
- 📁 **归档** 笔记到合适的文件夹
- 🔗 **连接** 笔记与相关内容的 wiki 链接
- 📋 **维护** 文件夹索引和内容地图（MoC）
- 🧠 **学习** 您的偏好设置，越用越智能

---

## ⚡ 灵魂：CLAUDE.md

> 💡 **`CLAUDE.md` 是整个系统的大脑和灵魂。** 它包含了指导 Claude Code 处理笔记的所有指令。

- 您创建的每一条笔记都遵循 `CLAUDE.md` 中定义的工作流
- 它定义了文件夹结构、笔记格式、链接规则和安全协议
- 自定义它，让系统真正属于您
- `CLAUDE.md` 越完善，您的笔记体验就越智能

**把 `CLAUDE.md` 看作 AI 笔记系统的"操作系统"。**

---

## 🚀 快速开始

### 1️⃣ 安装设置

1. 将 `ai-takenote/` 文件夹复制到您想要的位置
2. 用 Obsidian 打开该文件夹作为 vault
3. 编辑 `3_profile/Personal Profile.md` 填写您的信息
4. 在 vault 目录内启动 Claude Code

### 2️⃣ 基本用法

使用 `/takenote` 斜杠命令：

```
/takenote 关于社交媒体平台网络效应的研究想法...
```

或者直接给 Claude Code 您的原始笔记内容。

Claude Code 会：
1. 🔍 分析内容
2. 📝 创建格式规范的笔记
3. 📂 放入合适的文件夹（如 `6_research/`）
4. 🏷️ 添加相关标签和链接
5. ✏️ 更新文件夹的 `_index.md`

### 3️⃣ 斜杠命令

`/takenote` 命令触发完整的笔记处理工作流：

```
/takenote <您的笔记内容>
```

### 4️⃣ 修饰符

添加修饰符来控制笔记归档位置：

- **`@inbox`** 📥 — 强制放入收件箱供人工审核
- **`@merge note name`** 🔄 — 整合到已有笔记
- **`@type:[category]`** 📂 — 覆盖自动分类
- **`@link note`** 🔗 — 请求指定链接

示例：
```
/takenote @type:research 行为经济学的新发现...
```

### 5️⃣ 在任何地方使用 `/takenote` 🌍

想在电脑的任何位置向您的 vault 添加笔记？设置全局命令：

1. **复制命令模板** 从 `system_config/takenote.md`
2. **编辑文件**，将 `YOUR_VAULT_PATH` 替换为您的实际 vault 路径：
   ```bash
   # macOS/Linux
   /Users/your-username/path/to/ai-takenote

   # Windows
   C:\Users\your-username\path\to\ai-takenote
   ```
3. **复制到 Claude 命令文件夹**：
   ```bash
   # macOS/Linux
   cp system_config/takenote.md ~/.claude/commands/

   # Windows
   copy system_config\takenote.md %USERPROFILE%\.claude\commands\
   ```

现在您可以在任何目录使用 `/takenote`！

**示例：**
```bash
# 您在完全不同的项目中
cd ~/some-other-project
# 但仍可以向您的 vault 添加笔记
/takenote 刚才想到一个新的研究方向...
```

## 📁 文件夹结构

```
ai-takenote/
├── .claude/
│   └── commands/
│       └── takenote.md # /takenote 斜杠命令
├── CLAUDE.md           # 🧠 AI 指令（核心灵魂 - 核心配置）
├── README.md           # 📖 英文说明
├── 中文README.md       # 📖 本文件
├── 0_inbox/            # 📥 待处理笔记
├── 1_navigation/       # 🗺️ 外部资源索引
├── 2_ideas/            # 💡 想法和思考
├── 3_profile/          # 👤 个人档案和状态
├── 4_teaching/         # 🎓 教学材料
├── 5_meetings/         # 🤝 会议记录
├── 6_research/         # 🔬 研究笔记
├── 7_admin/            # 📊 行政文档
├── 8_code/             # 💻 代码片段
├── 9_attachments/      # 📎 图片、PDF、文件
├── 10_bookmarks/       # 🔖 网页书签
├── workspace/          # 🛠️ 临时文件和 AI 输出
└── system_config/      # ⚙️ 系统配置和命令模板
```

## ✨ 核心功能

### 🔷 Obsidian 集成

- **Wiki 链接** 🔗 — `note name` 用于内部链接
- **别名** 🏷️ — `display text` 自定义显示文本
- **标签** 📌 — `#type/idea`、`#status/draft`、`#project/main`
- **Frontmatter** 📋 — 每条笔记的 YAML 元数据

### 📑 文件夹索引

每个文件夹包含一个 `_index.md`，内有所有笔记的单行描述。Claude Code 自动维护这些文件。

### 🗺️ 内容地图（MoC）

当 5 条以上笔记与某个主题相关时，Claude Code 会建议创建内容地图（MoC）作为导航中心。

### 📈 持续学习

`system_config/lessons_learned.md` 存储关于您偏好的洞察，让系统越用越智能。

## 🎨 自定义

### 📂 重命名文件夹

同时更新文件夹名称和 `CLAUDE.md` 中的结构说明。

### ➕ 添加自定义命令

在 `CLAUDE.md` 的"快速命令"部分添加新的快捷命令。

### 🤖 配置子代理

对于专业任务（学术写作、会议总结），在 Claude Code 设置中配置自定义子代理。

### 🌐 本地化

文件夹名称和模板可以翻译成任何语言。相应更新 `CLAUDE.md`。

## 📦 系统要求

- [Obsidian](https://obsidian.md/)（推荐用于查看/编辑）
- [Claude Code](https://claude.com/claude-code) CLI 工具
- Claude API 访问权限

## 🛡️ 安全特性

- ✅ 修改已有笔记前会确认
- 🚫 未经许可绝不删除内容
- 💾 保留原始输入
- 👀 应用前展示建议的修改

## 💡 使用技巧

1. **从简单开始** 🌱 — 使用原始文本输入，让 Claude Code 处理整理
2. **检查收件箱** 📥 — 定期查看 `0_inbox/` 中需要处理的项目
3. **建立链接** 🔗 — 链接越多，知识图谱越有价值
4. **更新档案** 👤 — 保持 `3_profile/` 最新，以获得更好的 AI 上下文
5. **清理工作区** 🧹 — 定期将 `workspace/` 中的重要内容移至合适的文件夹

## 👨‍💻 作者

[李学恒](https://github.com/Xueheng-Li)

## 📜 许可证

MIT 许可证 — 自由修改和分发。

## 🤝 贡献

欢迎贡献！请在 [GitHub](https://github.com/Xueheng-Li/AiNote) 提交问题和拉取请求。

---

<p align="center">
使用 ❤️ 由 <a href="https://github.com/Xueheng-Li">李学恒</a> 制作
</p>
