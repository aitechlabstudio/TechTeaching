# Claude Code / Codex 去 AI 味教程（Humanizer Skills）

很多人使用 Claude、ChatGPT 或 Codex 写文章后，都会发现一个问题：

> **AI 味太重。**

例如：

- 太多"此外"、"值得注意的是"
- 喜欢使用"不仅……而且……"
- 句式过于工整
- 总喜欢总结一句大道理
- 缺少真人写作的节奏感

如果你想让 AI 写出来的内容更加自然、更像真人写作，可以安装 **Humanizer Skill**。

目前推荐两个版本：

- 🌎 **Humanizer（英文）**
  https://github.com/blader/humanizer

- 🇨🇳 **Humanizer-zh（中文版）**
  https://github.com/op7418/Humanizer-zh

它们同时支持 Claude Code、Codex，以及其他支持 Skills 的 AI Agent。

---

# 方法一：让 AI Agent 自动安装（推荐）

这是最简单的方法。

如果你使用 Claude Code 或 Codex，可以直接让 AI 帮你安装。

安装英文版：

```text
Install the Humanizer skill from:

https://github.com/blader/humanizer
```

安装中文版：

```text
Install the Humanizer-zh skill from:

https://github.com/op7418/Humanizer-zh
```

或者直接输入：

```text
Please install this Skill.

https://github.com/blader/humanizer
```

Agent 通常会自动完成：

- 下载 GitHub 仓库
- 安装 Skill
- 放到正确目录
- 检查是否安装成功
- 提示重新启动（如果需要）

> **说明：**
>
> Claude Code、Codex CLI 等支持本地文件系统和 Git 的 AI Agent 可以自动完成安装。
>
> 如果你使用的是网页版 ChatGPT 或 Codex，则无法直接安装，需要使用下面的手动安装方法。

---

# 方法二：使用 Skills CLI 安装

如果已经安装 Skills CLI，可以直接执行：

英文版：

```bash
npx skills add https://github.com/blader/humanizer
```

中文版：

```bash
npx skills add https://github.com/op7418/Humanizer-zh
```

安装完成后，重新启动 Claude Code 或 Codex。

---

# 方法三：手动安装

如果不想使用 Skills CLI，也可以手动安装。

## Claude Code

Linux / macOS：

```text
~/.claude/skills/
```

Windows：

```text
%USERPROFILE%\.claude\skills\
```

执行：

```bash
git clone https://github.com/blader/humanizer
```

或

```bash
git clone https://github.com/op7418/Humanizer-zh
```

将仓库放入 `skills` 目录即可。

---

## Codex

Linux / macOS：

```text
~/.codex/skills/
```

Windows：

```text
%USERPROFILE%\.codex\skills\
```

同样将仓库放入 `skills` 目录。

目录结构示例：

```text
.codex
└── skills
    └── humanizer
        ├── SKILL.md
        ├── README.md
        └── ...
```

安装完成后，重新启动 Codex。

---

# 如何确认安装成功

可以直接询问 AI：

```text
What skills are currently installed?
```

或者：

```text
List all installed skills.
```

如果看到类似：

```
Humanizer
Humanizer-zh
```

说明安装成功。

---

# 如何使用

## 英文

直接告诉 AI：

```text
Use the Humanizer skill to rewrite the following article.

<文章内容>
```

或者：

```text
Humanize the following text.
```

---

## 中文

```text
请使用 Humanizer-zh 对下面内容进行处理。

要求：

- 保留原意
- 去掉 AI 味
- 不扩写
- 不删减重要内容
- 保持原来的格式

内容：

（粘贴文章）
```

---

# 推荐 Prompt（英文）

```text
Use the Humanizer skill.

Requirements:

- Preserve the original meaning
- Remove AI writing patterns
- Keep the same length
- Sound natural
- Keep formatting unchanged

Text:

(Paste your article here)
```

---

# 推荐 Prompt（中文）

```text
请使用 Humanizer-zh。

要求：

- 保留原意
- 去掉 AI 味
- 不扩写
- 不删减
- 保持格式
- 更像真人写作

内容：

（粘贴文章）
```

---

# 测试案例（中文）

原文：

> 这款软件不仅提升了效率，而且优化了用户体验。此外，它还提供了丰富的功能，使用户能够更加轻松地完成任务。

输入：

```text
请使用 Humanizer-zh 去掉 AI 味。

这款软件不仅提升了效率，而且优化了用户体验。此外，它还提供了丰富的功能，使用户能够更加轻松地完成任务。
```

可能输出：

> 新版本把几个常用功能整合到了一起，操作步骤也少了不少，用起来更顺手，大多数任务都能更快完成。

---

# 测试案例（英文）

Original：

> This innovative solution not only enhances productivity but also provides a seamless user experience.

输入：

```text
Use the Humanizer skill.

This innovative solution not only enhances productivity but also provides a seamless user experience.
```

可能输出：

> The update makes everyday work faster and easier. The interface feels simpler, and users can get things done with fewer steps.

---

# Voice Calibration（推荐）

如果希望生成结果更符合自己的写作风格，可以先提供自己写过的文章。

例如：

```text
Use the Humanizer skill.

Here are two paragraphs written by me:

（粘贴自己的文章）

Now rewrite the following text in my writing style.

（AI文章）
```

Humanizer 会学习你的：

- 用词习惯
- 句子长度
- 段落节奏
- 写作风格

生成的内容会更接近你的表达方式，而不是通用的人类风格。

---

# 推荐工作流程

建议将 Humanizer 放在文章完成后的最后一步。

```text
生成文章
      │
      ▼
修改内容
      │
      ▼
检查语法
      │
      ▼
Humanizer（去 AI 味）
      │
      ▼
最终版本
```

这样既能保留 AI 的效率，又能有效减少 AI 写作痕迹，使文章更加自然、更符合真人的表达习惯。
