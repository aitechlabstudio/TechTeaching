# 将Codex 接入阿里百炼API，免费使用每个模型100万的token

阿里百炼为每个模型免费提供了 100 万额度的 token，总共有 100 多个模型可以使用。本教程介绍如何将 Codex 接入阿里百炼的 API，从而免费使用 Claude Code 的 CLI 模式.
最新版 Codex 要求模型 支持 Responses API，以下模型可以直接使用：
qwen3.7-max、qwen3.7-plus、qwen3.6-plus 和 qwen3.6-flash 
其他模型需通过 Chat/Completions API 接入，需安装旧版本 Codex，如 0.80.0：

---

## 第一步：安装Codex

参考官网安装指南：https://github.com/openai/codex/blob/53b501974545547b26680b40ba2bb03903b2da44/README.md  
Windows上 第一种方法
在 Windows PowerShell 中运行下面的代码，无需安装Node

```powershell
irm https://claude.ai/install.ps1 | iex
```
第二种发放，通过NPM 安装，需要先安装Node 
以管理员的身份运行下面命令
```
winget install OpenJS.NodeJS.LTS
```
```
# Install using npm
npm install -g @openai/codex
```
---

## 第二步：开通百炼，获取 API Key

1. 打开 [bailian.aliyun.com](https://bailian.aliyun.com)
2. 用手机号登录阿里云账号
3. 首次进入会提示开通百炼服务，点「开通」（免费）
4. 首页找到「API Key 管理」，点「创建 API Key」
5. 选择默认业务空间，填写一个名称即可

> **注意：** 北京、新加坡、美国各有独立的 API，不可互用。

---


## 第3步：修改配置文件
> odex 使用 `config.toml` 作为配置文件
打开下面的命令，用记事本编辑配置文件

```powershell
notepad "$env:USERPROFILE\.codex\config.toml"
```
> 写入以下内容，只需要修改选用的模型，最新版codex支持这个机构模型：   
> qwen3.7-max、qwen3.7-plus、qwen3.6-plus 和 qwen3.6-flash 
 ```
model_provider = "Model_Studio"
model = "qwen3.7-max"
[model_providers.Model_Studio]
name = "Model_Studio"
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
env_key = "OPENAI_API_KEY"
wire_api = "responses"
```
---

## 第四步：设置 API Key 环境变量

**macOS / Linux，在 shell 配置文件中添加（`~/.zshrc` 或 `~/.bashrc`）：**

```bash
export OPENROUTER_API_KEY="sk-or-你的Key"
```

然后使配置生效：

```bash
source ~/.zshrc
```

**Windows PowerShell（临时生效，当前会话有效）：**

```powershell
$env:OPENROUTER_API_KEY = "sk-or-你的Key"
```

**Windows PowerShell（永久生效）：**

```powershell
[System.Environment]::SetEnvironmentVariable("OPENROUTER_API_KEY", "sk-or-你的Key", "User")
```

---

## 第五步：启动 Codex

进入你的项目目录，运行：

**Windows PowerShell：**

```powershell
cd C:\path\to\your\project
codex
```

**macOS / Linux：**

```bash
cd /path/to/your/project
codex
```

看到 Codex 界面启动，说明配置成功
