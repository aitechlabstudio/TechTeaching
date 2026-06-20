# Agnes AI 免费图片视频 API 教程

免费生成图片、视频，支持 Claude Code、Codex、Cursor 和 Python 自动化调用。

---

## 什么是 Agnes AI

Agnes AI 最近开放了免费的图片、视频和文本 API。

目前提供的主要模型：

| 模型                    | 功能        |
| --------------------- | --------- |
| agnes-2.0-flash       | 文本生成      |
| agnes-image-2.0-flash | 图片生成      |
| agnes-image-2.1-flash | 图片生成（最新版） |
| agnes-video-v2.0      | 视频生成      |

对于内容创作者来说，最有价值的是图片和视频模型。

---

## 注册 Agnes

官网：

```text
https://agnes-ai.com/
```

网页版可以直接聊天、生成图片和视频。

API 平台：

```text
https://platform.agnes-ai.com/
```

注意： 网页版账号和 API 平台账号需要分别注册。

---



## API 地址

```text
https://apihub.agnes-ai.com/v1
```

---

# 方法一：Claude Desktop 接入 Agnes

## 安装 Claude Desktop

```text
https://claude.com/download
```

## 安装 CC-Switch

```text
https://github.com/farion1231/cc-switch/releases
```

在 CC-Switch 中：

* 添加 Custom Provider
* API Base URL 填写：

```text
https://apihub.agnes-ai.com/v1
```

* API Format：

```text
OpenAI Chat Completions
```

* API Key：

```text
YOUR_API_KEY
```

开启模型映射：

```text
Sonnet -> agnes-2.0-flash
Opus -> agnes-2.0-flash
Haiku -> agnes-2.0-flash
```

保存即可使用。

---

# 方法二：Claude Code 调用图片和视频模型

个人不太推荐直接把 Agnes 当 Claude Code 的主模型。

实际测试下来：

* 响应速度偏慢
* 编码体验一般

所以我的方案是：

* Claude Code 使用字节或阿里模型
* 图片和视频使用 Agnes
* 通过 Skill 自动调用 Python 程序

---

## 下载 Skill

下载并解压 Skill 压缩包。

打开 Claude Code。

将 Skill 所在目录设置为工作目录。

---

## 文生图

在 Claude Code 中输入：

```text
阅读SKILL.md，根据使用指南帮我调用python程序，从文本生成图片。
api key 已经在 .env 文件里。
提示词：
梦幻般的森林，阳光透过树叶洒下，小鹿在溪边饮水，宫崎骏动画风格，柔和的色彩，高清细节
```

---

## 图生图

```text
阅读SKILL.md，根据使用指南帮我调用python程序，从一张图片生成另一张图片。
api key 已经在 .env 文件里。
输入图片：
input/1.png
提示词：
把图片里的服装改成职业装。
```

---

## 文生视频

```text
阅读SKILL.md，根据使用指南帮我调用python程序，生成一个视频。
api key 已经在 .env 文件里。
提示词：
第一人称球迷视角，世界杯决赛现场，手持摄像机晃动效果，周围球迷疯狂庆祝，举杯欢呼，烟火表演，真实现场音效氛围
```
---
# 方法三：直接使用 Python

## 文本生成图片

```bash
python scripts/agnes_image.py \
  --version 2.1 \
  --prompt "梦幻般的森林，阳光透过树叶洒下，小鹿在溪边饮水，宫崎骏动画风格，柔和的色彩，高清细节" \
  --output outputs/text-to-image-test.png \
  --size 1024x768
```

---

## 图片生成图片

```bash
python scripts/agnes_image.py \
  --version 2.1 \
  --prompt "将图片转换为梵高油画风格，星月夜色调，厚重的笔触，强烈的色彩对比" \
  --image input/1.png \
  --output outputs/image-to-image-test.png \
  --size 1024x768
```

---

## 生成视频

```bash
python scripts/agnes_video.py \
  --prompt "复古胶片风格，1986年世界杯马拉多纳上帝之手经典瞬间，球场观众沸腾，黑白渐变色彩，颗粒质感，电影镜头感，slow motion" \
  --num-frames 81 \
  --frame-rate 24 \
  --output outputs/world-cup-retro.mp4
```

---

# 我的建议

如果你需要：

* AI 图片生成
* AI 视频生成
* YouTube Shorts
* TikTok 内容创作
* AI Agent 自动化

Agnes 值得尝试。

对于文本模型，我个人还是更推荐：

* Claude
* GPT
* 豆包 DeepSeek

而 Agnes 更适合作为免费的图片和视频生成平台使用。
