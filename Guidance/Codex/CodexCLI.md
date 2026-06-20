# Codex CLI 接入 阿里百炼API 免费使用每个模型100 万个 token 

> 本教程介绍如何将 Codex CLI 接入阿里百炼的 API，从而免费使用 Codex 的 CLI 模式。   
> 阿里百炼为每个模型免费提供了 100 万额度的 token，总共有 100 多个模型可以使用。 
---

## 第一步：安装 Codex CLI

参考官方安装指南：https://github.com/openai/codex/blob/53b501974545547b26680b40ba2bb03903b2da44/README.md

### 方法一：官方一键脚本（无需安装 Node.js）

在 Windows PowerShell 中运行：

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

### 方法二：通过 npm 安装（需要 Node.js）

以**管理员身份**运行 PowerShell，先安装 Node.js：

```powershell
winget install OpenJS.NodeJS.LTS
```

然后安装 Codex：

```powershell
npm install -g @openai/codex
```

> ⚠️ 包名必须是 `@openai/codex`，不是 `codex`。`codex` 是 npm 上一个无关的旧项目。

安装完成后验证：

```powershell
codex --version
```

---

## 第二步：开通百炼，获取 API Key

1. 打开 [bailian.aliyun.com](https://bailian.aliyun.com)
2. 用手机号登录阿里云账号
3. 首次进入会提示开通百炼服务，点「开通」（免费）
4. 首页找到「API Key 管理」，点「创建 API Key」
5. 选择默认业务空间，填写一个名称即可

> **注意：** 华北、新加坡、美国各有独立的 API，不可互用。
>  只有华北区有免费的100 万额度的 token。

---

## 第三步：修改配置文件

Codex 使用 `config.toml` 作为配置文件：

- **Windows**：`C:\Users\<用户名>\.codex\config.toml`
- **macOS / Linux**：`~/.codex/config.toml`

### Windows：用记事本打开编辑

```powershell
notepad "$env:USERPROFILE\.codex\config.toml"
```
写入内容如下，只需修改 `model` 为你想使用的模型：

```toml
model_provider = "Model_Studio"
model = "qwen3.7-max"

[model_providers.Model_Studio]
name = "Model_Studio"
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
env_key = "OPENAI_API_KEY"
wire_api = "responses"
```

> **注意：** 最新版 Codex 要求模型支持 Responses API，以下模型可直接使用：  
> `qwen3.7-max`、`qwen3.7-plus`、`qwen3.6-plus`、`qwen3.6-flash`  
>
> 其他模型需通过 Chat/Completions API 接入，需安装旧版本 Codex（如 `0.80.0`）。  
支持的模型（最新版 Codex，Responses API）：


| 模型 ID | 说明 |
|---|---|
| `qwen3.7-max` | 旗舰模型，效果最好 |
| `qwen3.7-plus` | 均衡性能 |
| `qwen3.6-plus` | 轻量高效 |
| `qwen3.6-flash` | 速度最快 |

---

## 第四步：设置 API Key 环境变量

将 `你的百炼APIKey` 替换为第二步获取的 API Key。

**Windows PowerShell（永久生效，推荐）：**

```powershell
[System.Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "你的百炼APIKey", "User")
```

设置完后关闭并重新打开 PowerShell 生效。

**Windows PowerShell（临时生效，当前会话有效）：**

```powershell
$env:OPENAI_API_KEY = "你的百炼APIKey"
```

**macOS / Linux，在 `~/.zshrc` 或 `~/.bashrc` 中添加：**

```bash
export OPENAI_API_KEY="你的百炼APIKey"
```

然后使配置生效：

```bash
source ~/.zshrc
```

验证环境变量是否设置成功：

```powershell
echo $env:OPENAI_API_KEY
```

输出你的 Key 说明设置成功。

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

看到 Codex 界面启动，说明配置成功！现在就可以免费使用百炼的模型进行编码了。

---

## 常见问题

**`codex` 命令找不到**
- 关闭并重新打开 PowerShell 后再试
- 用 npm 安装的，确认 npm 全局路径已加入系统 PATH：`npm config get prefix`

**API Key 无效或认证失败**
- 确认 `OPENAI_API_KEY` 环境变量已正确设置：`echo $env:OPENAI_API_KEY`
- 重新打开 PowerShell 窗口后再试

**模型不支持 / 报错**
- 最新版 Codex 只支持 `qwen3.7-max`、`qwen3.7-plus`、`qwen3.6-plus`、`qwen3.6-flash`
- 其他模型请安装旧版：`npm install -g @openai/codex@0.80.0`
---

## 参考链接

- [Codex CLI GitHub 仓库](https://github.com/openai/codex)
- [阿里百炼官网]([https://bailian.aliyun.com](https://bailian.console.aliyun.com/cn-beijing?tab=doc#/doc/?type=model&url=3031966))
