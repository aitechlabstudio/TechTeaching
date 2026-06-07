# 将Claude Code 接入阿里百炼API，  

> 免费使用 Claude Code CLI · 100+ 模型 · 每个模型 100 万 token 免费额度

阿里百炼为每个模型免费提供了 100 万额度的 token，总共有 100 多个模型可以使用。本教程介绍如何将 Claude Code 接入阿里百炼的 API，从而免费使用 Claude Code 的 CLI 模式（即 Terminal / CLI 模式，非桌面 App 模式）。

---

## 第一步：安装 Claude Code

参考官网安装指南：https://code.claude.com/docs/en/overview#native-install-recommended

推荐使用 **Native Install (Recommended)**，无需安装 Node.js。在 Windows PowerShell 中运行：

```powershell
irm https://claude.ai/install.ps1 | iex
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

## 第三步：跳过 Anthropic 官方登录验证

编辑或新建 `~/.claude.json`（Windows 路径：`C:\Users\<用户名>\.claude.json`），将 `hasCompletedOnboarding` 设为 `true`：

```json
{
  "hasCompletedOnboarding": true
}
```

在 Windows PowerShell 中直接执行以下命令即可：

```powershell
Set-Content -Path "$env:USERPROFILE\.claude.json" -Value '{ "hasCompletedOnboarding": true }'
```

---

## 第四步：配置 settings.json

将 `YOUR_API_KEY` 替换为你的阿里云百炼 API Key。可用模型参见百炼网站的 Anthropic 兼容 API 文档。

### 华北区（默认）

`ANTHROPIC_BASE_URL` 使用：`https://dashscope.aliyuncs.com/apps/anthropic`

### 新加坡区

`ANTHROPIC_BASE_URL` 使用：`https://{WorkspaceId}.ap-southeast-1.maas.aliyuncs.com/apps/anthropic`  
（将 `{WorkspaceId}` 替换为真实的 Workspace ID）

### 在 PowerShell 中一键写入配置（华北区）

```powershell
New-Item -ItemType Directory -Path "$env:USERPROFILE\.claude" -Force | Out-Null
@'
{
    "env": {
        "ANTHROPIC_AUTH_TOKEN": "YOUR_API_KEY",
        "ANTHROPIC_BASE_URL": "https://dashscope.aliyuncs.com/apps/anthropic",
        "ANTHROPIC_MODEL": "qwen3.7-max",
        "ANTHROPIC_DEFAULT_HAIKU_MODEL": "qwen3.6-flash",
        "ANTHROPIC_DEFAULT_SONNET_MODEL": "qwen3.7-max",
        "ANTHROPIC_DEFAULT_OPUS_MODEL": "qwen3.7-max",
        "CLAUDE_CODE_SUBAGENT_MODEL": "qwen3.7-max"
    }
}
'@ | Set-Content -Path "$env:USERPROFILE\.claude\settings.json"
```

也可以用记事本手动编辑：

```powershell
notepad C:\Users\<用户名>\.claude\settings.json
```

### 说明

- 默认模型为 `qwen3.7-max`，可替换为其他 100+ 个免费模型，例如 `deepseek-v3`
- 模型 ID 可在百炼网站查询
- 免费额度通常有效期约 6 个月，过期不返还
- 建议以 `qwen-plus` 或 `deepseek-v3` 为主力日常编码使用，够用且省额度
