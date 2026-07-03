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

# 安装方法一：让 AI Agent 自动安装（推荐）

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

# 安装方法二：使用 Skills CLI 安装

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

# 安装方法三：手动安装

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



# 如何使用

安装完成并重新启动 Claude Code 或 Codex 后，就可以直接使用 Humanizer。

## 方法一：使用 Slash Command（推荐）

英文版：

```text
/humanizer
```

中文版：

```text
/humanizer-zh
```

输入命令后，再粘贴需要处理的文章即可。

例如：

```text
/humanizer

This innovative solution not only enhances productivity but also delivers a seamless user experience.
```

中文版：

```text
/humanizer-zh

这款软件不仅提升了效率，而且优化了用户体验。此外，它还提供了丰富的功能，使用户能够更加轻松地完成任务。
```

---

## 方法二：自然语言调用

如果你不喜欢使用 Slash Command，也可以直接告诉 AI 使用 Humanizer Skill。

英文：

```text
Use the Humanizer skill to rewrite the following article.

...
```

中文：

```text
请使用 Humanizer-zh Skill 对下面内容进行处理。

...
```

AI 会自动调用对应的 Skill。

---
# 指定写作风格
如果希望生成结果更符合自己的写作风格，可以先提供自己写过的文章。

例如：
```
这是我写的两个段落
（粘贴自己的文章）
 按照我的风格，帮我重写下面的文章
（AI文章）
```
```text
Use the Humanizer skill.

Here are two paragraphs written by me:

（粘贴自己的文章）

Now rewrite the following text in my writing style.

（AI文章）
```

## 测试：按照我的写作风格重写文章

```text
使用 Humanizer-zh skill。

这是我写的两个段落：

沿着荷塘，是一条曲折的小煤屑路。这是一条幽僻的路；白天也少人走，夜晚更加寂寞。荷塘四面，长着许多树，蓊蓊郁郁的。路的一旁，是些杨柳，和一些不知道名字的树。没有月光的晚上，这路上阴森森的，有些怕人。今晚却很好，虽然月光也还是淡淡的。


按照我的风格，帮我重写下面的文章：

人工智能正在快速改变我们的工作方式。通过使用先进的大语言模型，用户可以更高效地完成内容创作、代码编写以及数据分析等任务。此外，这些工具还能显著提升工作效率，帮助用户节省大量时间，从而专注于更有价值的工作。然而，在使用 AI 生成内容时，也需要注意生成结果可能存在不准确或缺乏个性化的问题，因此建议用户结合自身经验进行修改和完善。
```
```
Use the Humanizer skill.

Here are two paragraphs written by me:

When I try a new AI tool, I don't just read the documentation. I install it, test it myself, and see where people are likely to get stuck. If something is confusing or doesn't work as expected, I'll figure out a simpler way and include it in my tutorial. That way, people can follow along without wasting time.

I like to keep my guides practical and beginner-friendly. If a task can be done with one command instead of ten, I'll always choose the simpler approach. My goal is to help people get results quickly, not overwhelm them with unnecessary details.

Now rewrite the following text in my writing style:

Artificial intelligence is transforming the way people work by enabling faster content creation, software development, and data analysis. These advanced technologies significantly improve productivity while reducing the time required to complete complex tasks. However, users should carefully review AI-generated content to ensure its accuracy and adapt it to their specific needs before using it in real-world scenarios.
```

