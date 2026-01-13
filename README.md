# 🤖 AI 原生笔记系统

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/Xueheng-Li/AiNote)

中文 | [English](./README_EN.md)

用 [Claude Code](https://claude.com/claude-code) + [Obsidian](https://obsidian.md/) 搭建的个人知识库。

## 🎯 它是什么

把笔记甩给 Claude Code，它会：

- 🔍 分析主题、关键词和类型
- 📁 放进合适的文件夹
- 🔗 建立相关笔记的 wiki 链接
- 📋 维护文件夹索引和 MoC
- 🧠 记住你的习惯，越用越顺手

---

## ⚡ 核心：CLAUDE.md

> 这个文件是系统的大脑。Claude Code 处理笔记的所有规则都在这里。

- 笔记处理流程
- 文件夹结构和命名规则
- 链接规则和安全限制
- 你的个人偏好

**你可以随意修改 `CLAUDE.md`，让系统更符合你的使用习惯。**

---

## 🚀 快速上手

### 1️⃣ 安装

1. 复制 `ai-takenote/` 到你想放的位置
2. 用 Obsidian 打开这个文件夹
3. 编辑 `3_profile/Personal Profile.md` 填写你的信息
4. 在这个目录下启动 Claude Code

### 2️⃣ 启用命令

**第一次使用前，必须把命令文件复制到 Claude 的命令目录：**

```bash
# macOS/Linux
cp .claude/commands/takenote.md ~/.claude/commands/

# Windows
copy .claude\commands\takenote.md %USERPROFILE%\.claude\commands\
```

### 3️⃣ 开始记笔记

```bash
/takenote 关于社交媒体网络效应的研究想法...
```

或者直接说话，Claude Code 也会处理。

它会自动：
1. 分析内容
2. 创建格式正确的笔记
3. 放进合适的文件夹
4. 加标签、建链接
5. 更新文件夹索引

### 4️⃣ 快捷指令

- `@inbox` — 放进收件箱稍后处理
- `@merge note name` — 合并到已有笔记
- `@type:research` — 指定分类
- `@link note` — 链接到指定笔记

```bash
/takenote @type:research 行为经济学的新发现...
```

### 5️⃣ 全局使用

想在任何目录都能记笔记？

1. 复制 `system_config/takenote.md`
2. 把里面的 `YOUR_VAULT_PATH` 改成你的实际路径
3. 复制到 `~/.claude/commands/`

这样在任何项目里都能用 `/takenote`。

---

## 📁 文件夹结构

```
ai-takenote/
├── .claude/commands/    # 命令文件
├── CLAUDE.md           # 系统核心配置
├── README.md           # 说明文档
├── README_EN.md        # 英文版
├── 0_inbox/            # 收件箱
├── 1_navigation/       # 外部资源索引
├── 2_ideas/            # 想法笔记
├── 3_profile/          # 个人信息
├── 4_teaching/         # 教学材料
├── 5_meetings/         # 会议记录
├── 6_research/         # 研究笔记
├── 7_admin/            # 行政文档
├── 8_code/             # 代码片段
├── 9_attachments/      # 附件
├── 10_bookmarks/       # 书签
├── workspace/          # 临时文件
└── system_config/      # 系统配置
```

你可以改这些文件夹名，记得同步更新 `CLAUDE.md`。

---

## ✨ 特性

**Obsidian 集成**
- Wiki 链接、别名、标签、frontmatter

**自动维护**
- 每个文件夹的 `_index.md` 自动更新
- 相关笔记超过 5 篇时建议建 MoC
- 用 `lessons_learned.md` 记录使用偏好

---

## 📖 示例

vault 里有一篇 [AI原生笔记系统作为个性化学习中心](2_ideas/AI原生笔记系统作为个性化学习中心.md)，展示了这套系统的理念：

- 记忆延伸：跨时间连接、模式识别
- 智能连接：自动发现隐藏关联
- 上下文理解：从个人档案中"认识"你
- 自我改进：记住什么有效、什么无效

这条笔记本身也是通过工作流生成的——系统可以处理关于系统的内容，形成自我文档化的知识库。

---

## 📦 需要

- [Obsidian](https://obsidian.md/)（查看编辑用）
- [Claude Code](https://claude.com/claude-code) CLI
- Claude API

## 🛡️ 安全

- 修改笔记前会确认
- 不会删除任何内容
- 保留原始输入
- 显示所有待应用的修改

---

## 💡 建议

1. 自然输入就好，不用管格式
2. 定期清理 `0_inbox/`
3. 多建链接，知识才有价值
4. 保持 `3_profile/` 最新
5. 把 `workspace/` 里的东西归类

---

## 👨‍💻 作者

[Xueheng Li](https://github.com/Xueheng-Li)

## 📜 MIT

---

<p align="center">
Made with ❤️ by <a href="https://github.com/Xueheng-Li">Xueheng Li</a>
</p>
