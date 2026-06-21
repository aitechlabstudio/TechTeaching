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

文本模型 Agnes-2.0-Flash 目前在 Claw-Eval 榜单排第 9 名。
Claw-Eval 不是传统的数学、知识问答、代码类刷题榜单。它测试的是模型在真实 Agent 场景中的综合执行能力。可以说是「最接近 AI Agent 实战能力」的评测之一。

图像模型 Agnes-Image-2.0-Flash 目前在第三方测评机构 Artificial Analysis 的图片编辑榜单排第 19 名。
视频模型 Agnes-Video-V2.0 同样进入了 Artificial Analysis 视频（带音频）榜单。

并且，支持原生音画同出。意味着你不需要单独配音，Agnes 直接一步到位。

对于内容创作者来说，最有价值的是图片和视频模型。

---

## 注册 Agnes 账号获取API Key
官网地址如下, 注意： 网页版账号和 API 平台账号需要分别注册。   
```text
https://agnes-ai.com/
```
---
## 使用场景一： 文本模型接入 Codex 和 Claude Code 等智能体
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

## 使用场景二：通过Claude Code或Codex调用图片和视频模型

---

### 准备工作

* 下载并解压 Skill 压缩包， 地址：   
https://github.com/aitechlabstudio/TechTeaching/raw/main/Guidance/agnes-image-video.zip
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
## 使用场景三：直接执行Python脚本生成图片和视频
## 文本生成图片

```bash
python scripts/agnes_image.py --version 2.1 --prompt "穿粉色牛仔裙的白色小猫，3D 真实电影风格，柔和自然光，浅景深，毛发细节清晰，背景咖啡店露台" --output outputs/cat.png --size 1024x768

```

## 图片生成图片

```bash
python scripts/agnes_image.py --version 2.1 --prompt "将图片里小猫穿的裙子改成蓝色牛仔裙，其他不变。" --image "input/cat.png" --output outputs/catinjeans.png --size 1024x768
```

## 文本生成视频

```bash
python scripts/agnes_video.py --prompt "亚洲女性模特在白色摄影棚中展示黑色连衣裙，从全景缓缓切到半身特写，模特自然转身，有轻柔背景音乐" --num-frames 121 --frame-rate 24 --output outputs/aisionmodel.mp4
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
