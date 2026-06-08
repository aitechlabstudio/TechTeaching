# Codex CLI × OpenRouter

> 通过 OpenRouter 使用 Codex CLI，可以访问 GPT、Claude、Gemini 等数百个模型，支持自动故障转移和统一账单管理。

Codex CLI 是 OpenAI 开源的本地 AI 编程助手，在终端里直接使用。它原生支持 OpenRouter 作为模型提供商，配置非常简单。

---

## 第一步：安装 Codex CLI

参考官方仓库：https://github.com/openai/codex

### Windows 安装（推荐：官方一键脚本）

在 PowerShell 中运行以下命令，无需手动安装 Node.js：

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://chatgpt.com/codex/install.ps1 | iex"
```

安装完成后验证：

```powershell
codex --version
```

### Windows 安装（备选：通过 npm）

如果你已安装 Node.js 22 或以上版本，也可以用 npm 安装：

```powershell
npm install -g @openai/codex
```

> ⚠️ 注意：npm 包名必须是 `@openai/codex`，不是 `codex`。`codex` 是 npm 上一个 2012 年的无关旧项目，安装后无法使用。

安装 Node.js 可前往：https://nodejs.org，下载 LTS 版本（22+）。

### macOS / Linux 安装

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

或通过 npm：

```bash
npm install -g @openai/codex
```

---

## 第二步：注册 OpenRouter，获取 API Key

1. 打开 [openrouter.ai](https://openrouter.ai)，注册或登录账号
2. 进入 [API Keys 页面](https://openrouter.ai/keys)
3. 点「Create Key」，填写名称后创建
4. 复制 API Key（格式为 `sk-or-...`）

> OpenRouter 有免费额度，也支持按量付费，价格透明。

---

## 第三步：配置 Codex 连接 OpenRouter

Codex 使用 `config.toml` 作为配置文件，路径如下：

- **Windows**：`C:\Users\<用户名>\.codex\config.toml`
- **macOS / Linux**：`~/.codex/config.toml`

**Windows PowerShell 一键创建配置文件：**

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.codex" -Force | Out-Null
@'
model_provider = "openrouter"
model_reasoning_effort = "high"
model="poolside/laguna-m.1:free"

[model_providers.openrouter]
name = "openrouter"
base_url="https://openrouter.ai/api/v1"
env_key="OPENROUTER_API_KEY"
'@ | Set-Content -Path "$env:USERPROFILE\.codex\config.toml"
```

也可以用记事本手动编辑：

```powershell
notepad "$env:USERPROFILE\.codex\config.toml"
```

写入以下内容：

```toml
model_provider = "openrouter"
model_reasoning_effort = "high"
model="poolside/laguna-m.1:free"

[model_providers.openrouter]
name = "openrouter"
base_url="https://openrouter.ai/api/v1"
env_key="OPENROUTER_API_KEY"
```

**参数说明：**

| 参数 | 说明 |
|---|---|
| `model_provider` | 指定使用 OpenRouter 作为提供商 |
| `model` | 模型 ID，可在 [openrouter.ai/models](https://openrouter.ai/models) 查询 |
| `model_reasoning_effort` | 推理强度：`low` / `medium` / `high` / `xhigh` |
| `base_url` | OpenRouter API 地址，固定填此值 |
| `env_key` | 读取 API Key 的环境变量名称 |

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

看到 Codex 界面启动，说明配置成功！现在所有请求都会通过 OpenRouter 路由。

---

## 可选：项目信任级别配置

可以为不同项目设置不同的权限级别，添加到 `config.toml`：

```toml
[projects."/path/to/trusted/project"]
trust_level = "trusted"

[projects."/path/to/untrusted/project"]
trust_level = "untrusted"
```

- `trusted`：Agent 有完整权限（执行命令、编辑文件等）
- `untrusted`：限制访问，更安全

---

## 为什么选择 OpenRouter？

- **多模型支持**：一个 Key 访问 GPT、Claude、Gemini、DeepSeek 等数百个模型，只需修改 `config.toml` 中的 `model` 字段即可切换
- **自动故障转移**：某个提供商不可用时自动切换，保证编码会话不中断
- **用量可视化**：在 [OpenRouter Activity Dashboard](https://openrouter.ai/activity) 实时查看 token 消耗和费用
- **隐私保护**：默认不记录源代码内容，除非主动开启 prompt logging
## 用阿里百炼 API
适用于支持 OpenAI Responses API 的模型（如 qwen3.7-max），可使用最新版 Codex。

 ```
model_provider = "Model_Studio"
model = "qwen3.7-max"
[model_providers.Model_Studio]
name = "Model_Studio"
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
env_key = "OPENAI_API_KEY"
wire_api = "responses"
```
