# DeepSeek V4 Flash 接入 Codex 完全教程

> 本教程将指导您通过 **官方脚本** 或 **CC Switch**，将 **DeepSeek V4 Flash** 接入 **Codex AI 编程助手**，无需复杂配置，几分钟即可完成。

---

# 📋 目录

- 前提准备
- 方法一：官方一键配置脚本（推荐）
- 方法二：CC Switch 图形化管理（多供应商切换）
- 方法三：手动配置文件
- 免费 API 获取
- 常见问题与故障排除
- 总结

---

# 前提准备

## 1. 安装 Codex 客户端
https://chatgpt.com/zh-Hans-CN/download/   
确保已经安装以下至少一种 Codex 客户端，并且**至少启动过一次**（确保 `~/.codex` 目录已经生成）。

支持：

- Codex CLI（命令行）
- ChatGPT Desktop（官方桌面版）
- VS Code Codex 扩展

> **重要提示**
>
> 目前 **仅 `deepseek-v4-flash` 支持接入 Codex**。
>
> `deepseek-v4-pro` 预计 **2026 年 8 月初**支持。

---

## 2. 获取 DeepSeek API Key

登录 **DeepSeek Platform** 
https://platform.deepseek.com/   
步骤：

1. 注册或登录账号
2. 打开 API 管理页面
3. 创建新的 API Key（`sk-` 开头）
4. 保存密钥，后续配置需要使用

---

# 方法一：官方一键配置脚本（推荐）
参考： https://api-docs.deepseek.com/zh-cn/quick_start/agent_integrations/codex
DeepSeek 官方提供了一键配置脚本，可以自动完成全部配置，是目前最简单的方法。

---

## macOS / Linux

终端执行：

```bash
bash <(curl -fsSL https://cdn.deepseek.com/api-docs/codex-deepseek-setup.sh)
```

---

## Windows

PowerShell：

```powershell
irm https://cdn.deepseek.com/api-docs/codex-deepseek-setup-en.ps1 | iex
```

---

## 首次运行流程

脚本会依次询问：

1. 输入 API Key（sk- 开头）
2. 选择模型

```
deepseek-v4-flash（推荐）

deepseek-v4-pro（即将支持）
```

随后脚本自动完成：

- ✅ 备份当前配置到

```
~/.codex/backup-deepseek/
```

- ✅ 创建

```
~/.codex/models.json
```

- ✅ 修改

```
~/.codex/config.toml
```

- ✅ 自动检查配置文件语法

---

## 再次运行脚本

再次执行脚本时，可以：

- 切换模型
- 恢复 OpenAI 默认配置（菜单第 3 项）
- 重新生成配置

---

## 官方脚本做了什么？

### ① 注册模型

向 Codex 注册：

- 模型名称
- Context Window（1M）
- Tool Calling
- Reasoning Level
- Verbosity

---

### ② 修改配置

自动修改：

```
config.toml
```

仅修改必要字段。

不会覆盖：

- MCP Server
- Trusted Projects
- 其它自定义配置

---

### ③ 自动处理冲突

如果存在冲突字段：

- 自动删除旧配置
- 保留兼容字段
- 输出修改说明

---

# 方法二：CC Switch 图形化管理（推荐多供应商）

如果需要：

- OpenAI
- Claude
- DeepSeek
- Kimi
- Gemini

之间快速切换，推荐使用 **CC Switch**。

---

## 1. 下载

GitHub Releases：

```
https://github.com/farion1231/cc-switch/releases
```

根据系统下载：

Windows：

```
.exe
```

macOS：

```
.dmg
```

Linux：

```
.AppImage
.deb
```

---

## 2. 首次启动

CC Switch 会：

自动检测：

```
~/.codex
```

如果没有配置：

会自动引导完成初始化。

---

## 3. 添加 DeepSeek

### 方法 A（推荐）

点击：

```
+
```

或者：

```
添加供应商
```

选择：

```
DeepSeek
```

填写：

API Key

模型：

```
deepseek-v4-flash
```

点击：

```
保存
```

即可。

> 从 **v3.19.1** 开始，DeepSeek 默认采用 **Responses API**，无需本地路由。

---

### 方法 B（手动填写）

供应商：

```
DeepSeek
```

API：

```
https://api.deepseek.com/v1
```

API Key：

```
sk-xxxx
```

Wire API：

```
Responses
```

模型：

```
deepseek-v4-flash
```

Context Window：

```
1048576
```

---

## 4. 切换供应商

点击供应商卡片：

```
设为当前
```

CC Switch 会自动：

- 备份配置
- 修改 config.toml
- 修改 auth.json
- 切换 Provider

无需重新登录。

---

## 5. 会话管理

CC Switch 可以统一管理所有 Provider 的历史聊天。

例如：

```
codex resume
```

仍然可以看到：

- OpenAI
- DeepSeek
- Claude

所有历史记录。

支持：

- 搜索
- 删除
- 继续聊天

---

## 官方脚本 VS CC Switch

| 功能 | 官方脚本 | CC Switch |
|------|---------|-----------|
| 一键配置 | ✅ | ✅ |
| 多供应商切换 | ❌ | ✅ |
| 图形界面 | ❌ | ✅ |
| 会话统一管理 | ❌ | ✅ |
| 用量统计 | ❌ | ✅ |
| MCP 管理 | ❌ | ✅ |
| 自动同步价格 | ❌ | ✅ |

### 推荐

只使用一个 Provider：

👉 官方脚本

多个 Provider 来回切换：

👉 CC Switch

---

# 方法三：手动配置

适合高级用户。

---

## 1. 创建 models.json

创建：

```
~/.codex/models.json
```

内容：

```json
{
  "models": [
    {
      "slug": "deepseek-v4-flash",
      "prefer_websockets": false,
      "support_verbosity": true,
      "default_verbosity": "low",
      "apply_patch_tool_type": "freeform",
      "web_search_tool_type": "text",
      "input_modalities": ["text"],
      "supports_parallel_tool_calls": true,
      "context_window": 1048576,
      "max_context_window": 1048576,
      "display_name": "DeepSeek-V4-Flash",
      "description": "Latest frontier agentic coding model.",
      "default_reasoning_level": "high",
      "supported_reasoning_levels": [
        {
          "effort": "low",
          "description": "Fast responses with lighter reasoning"
        },
        {
          "effort": "high",
          "description": "Extra high reasoning depth for complex problems"
        },
        {
          "effort": "max",
          "description": "Maximum reasoning depth for the hardest problems"
        }
      ],
      "supported_in_api": true
    }
  ]
}
```

---

## 2. 修改 config.toml

编辑：

```
~/.codex/config.toml
```

添加：

```toml
preferred_auth_method = "apikey"
forced_login_method = "api"

[model_providers.deepseek]
api_key = "sk-你的APIKey"
base_url = "https://api.deepseek.com/v1"
wire_api = "responses"
```

---

## 3. 重启 Codex

重新启动：

- Codex CLI
- ChatGPT Desktop
- VS Code

即可生效。

---

# 免费 API 获取

DeepSeek 提供免费测试 Endpoint。

适用于：

- 学习
- 测试
- Demo

注意：

- 免费额度有限
- 不建议生产环境
- 正式项目建议购买官方 API

---

# 常见问题（FAQ）

## Q1：运行官方脚本后 Codex 无法启动？

解决：

- 检查 `models.json`
- 检查 JSON 是否合法
- Codex CLI ≥ 0.144.0
- 使用脚本菜单第 3 项恢复配置
- 或使用 CC Switch 修复配置

---

## Q2：切换供应商需要重新登录吗？

不需要。

CC Switch 会自动切换：

- auth.json
- config.toml

无需再次：

```
codex login
```

---

## Q3：为什么会话不能跨供应商继续？

原因：

Codex 的推理内容（`encrypted_content`）只能由生成它的后端解密。

因此：

- 同一 Provider 可以继续
- 跨 Provider 无法恢复

属于 Codex 的设计限制。

---

## Q4：为什么用量统计不准确？

CC Switch **v3.19.1** 已修复：

- Claude Desktop 双计问题
- 自动校正最近 30 天数据
- 可手动执行：

```
重建 Codex 用量
```

---

## Q5：DeepSeek V4 Pro 为什么不能使用？

目前：

```
deepseek-v4-pro
```

预计 **2026 年 8 月初**支持接入 Codex。

现阶段建议：

```
deepseek-v4-flash
```

---

# 总结

三种方式对比：

| 方法 | 适合人群 | 难度 | 推荐指数 |
|------|---------|------|----------|
| 官方脚本 | 单供应商、快速配置 | ⭐ | ⭐⭐⭐⭐⭐ |
| CC Switch | 多供应商、图形化管理 | ⭐⭐ | ⭐⭐⭐⭐☆ |
| 手动配置 | 高级用户、自定义需求 | ⭐⭐⭐ | ⭐⭐⭐☆☆ |

## 推荐方案

- **只使用 DeepSeek**：推荐官方一键脚本，简单快捷。
- **需要在 OpenAI、DeepSeek、Claude、Kimi 等模型之间频繁切换**：推荐 CC Switch，提供图形界面、统一会话管理和配置切换，使用体验更佳。
- **有特殊需求或希望完全掌控配置**：可以选择手动配置方式。

---

