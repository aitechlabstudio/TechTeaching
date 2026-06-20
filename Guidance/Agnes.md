# 使用Agnes API免费生成图片和视频   支持 Claude、Codex
---
## 什么是 Agnes AI
> Agnes AI 是新加坡本土模型公司。他的模型家族专为 OpenClaw、Hermes 等智能体工具而生, 同时提供文生图、图生图与图生视频等能力，呈现电影级画面与同步音画生成，并兼顾高速表现——让你顺畅完成 AI 内容的创作、转化与部署。

目前提供的主要模型：

| 模型                    | 功能        |
| --------------------- | --------- |
| agnes-2.0-flash       | 文本生成      |
| agnes-image-2.0-flash | 图片生成      |
| agnes-image-2.1-flash | 图片生成（最新版） |
| agnes-video-v2.0      | 视频生成      |

对于内容创作者来说，最有价值的是图片和视频模型。

---

## 步骤一 注册 Agnes 账号获取API Key
官网地址如下。 网页版可以直接聊天、生成图片和视频。
```text
https://agnes-ai.com/
```
API 平台：
```text
https://platform.agnes-ai.com/
```
注意： 网页版账号和 API 平台账号需要分别注册。   
---
## 1. 接入 Agnes Claude Code 等智能体

* 安装 Claude Desktop
```text
https://claude.com/download
```
* 安装 CC-Switch
```text
https://github.com/farion1231/cc-switch/releases
```
* 在 CC-Switch 中， 添加 自定义配置的供应商
* API Base URL 填写：

```text
https://apihub.agnes-ai.com/v1
```
* 输入API Key；
* API 格式选择 OpenAI Chat Completions；
* 开启模型映射：
```text
Sonnet -> agnes-2.0-flash
Opus -> agnes-2.0-flash
Haiku -> agnes-2.0-flash
```
* 个人不太推荐直接把 Agnes 当 Claude Code 的主模型； 响应速度偏慢，编码体验一般
---

## 2. Claude Code 调用图片和视频模型

---

### 准备工作

* 下载并解压 Skill 压缩包。
* 打开 Claude Code。
* 将 Skill 所在目录设置为工作目录。
---

### 从文本生成图片
* 在 Claude Code 中输入：

```text
阅读SKILL.md，根据使用指南帮我调用python程序，从文本生成图片。
api key 已经在 .env 文件里。
提示词：
梦幻般的森林，阳光透过树叶洒下，小鹿在溪边饮水，宫崎骏动画风格，柔和的色彩，高清细节
```
### 从一张图片生成另一张图片

```text
阅读SKILL.md，根据使用指南帮我调用Python程序，从一张图片生成另一张图片。
api key 已经在 .env 文件里。
输入图片：  input/1.png
提示词：
把图片里的人物的着装改成职业装。
```
### 从文本生成视频

```text
阅读SKILL.md，根据使用指南帮我调用python程序，生成一个视频。
api key 已经在 .env 文件里。
提示词：
第一人称球迷视角，世界杯决赛现场，手持摄像机晃动效果，周围球迷疯狂庆祝，举杯欢呼，烟火表演，真实现场音效氛围
```
---
## 3. 直接使用 Python
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

## 我的建议

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
