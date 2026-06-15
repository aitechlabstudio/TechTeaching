# Codex 桌面 App 接入低价甚至免费的国产模型教程
> 适用于  
> 阿里百炼：每个模型 **100 万 token** 免费额度   
> 字节火山引擎：每个模型每天最多 **200 万 token** 免费额度
> 还有其他众多模型可选

本教程介绍三种方法将 Codex 桌面 App 接入国产大模型，免费使用百万 token 额度。

> 教程里的链接命令和代码，可一键复制。

---

## 三种方案对比

| 方案 | 适用模型 | 难度 | 推荐指数 |
|---|---|---|---|
| 方法一：直接修改配置文件 | 仅兼容 OpenAI 格式的模型 | ★☆☆☆☆ | ★★★☆☆ |
| 方法二：CC-Switch | 几乎所有模型 | ★★★☆☆ | ★★★★★ |
| 方法三：Codex++ | 多模型统一管理 | ★★☆☆☆ | ★★★★★ |

---

## 准备步骤1：下载并安装Codex 桌面 App

前往官网下载安装
```
https://chatgpt.com/zh-Hans-CN/codex/
```

## 方法一：直接修改配置文件

适合模型：`qwen3.7-max`、`qwen3.7-plus`、`qwen3.6-plus`、`qwen3.6-flash` 以及它们的子版本。    

这些模型兼容 OpenAI 格式，只需修改配置文件即可直接使用。

### 1. 启动 Codex，修改登录认证方式

打开 Codex 桌面 App。 选择使用其他方式登录，随便输入一个api key
---

### 2. 开通百炼，获取 API Key

1. 打开阿里百炼的官网
```
https://bailian.aliyun.com
```
2. 用手机号登录阿里云账号
3. 首页找到「API Key 管理」，点「创建 API Key」
4. **立即复制保存，API Key 只显示一次**

> ⚠️ 只有**华北区**有每个模型 100 万 token 的免费额度，新加坡和美国区没有。华北、新加坡、美国的 API 各自独立，不可互用。

### 3. 修改配置文件

Codex 配置文件路径：

- **Windows**：`C:\Users\<用户名>\.codex\config.toml`
- **macOS / Linux**：`~/.codex/config.toml`

**先备份配置文件再Windows 用记事本打开：**

```powershell
cp  "$env:USERPROFILE\.codex\config.toml" "$env:USERPROFILE\.codex\config.toml.bak"
```
```powershell
notepad "$env:USERPROFILE\.codex\config.toml"
```

写入以下内容，只需修改 `model` 为你想使用的模型：

```toml
model_provider = "Model_Studio"
model = "qwen3.7-max"

[model_providers.Model_Studio]
name = "Model_Studio"
base_url = "https://dashscope.aliyuncs.com/compatible-mode/v1"
env_key = "OPENAI_API_KEY"
wire_api = "responses"
```

最新版 Codex，需支持 Responses API, 支持这种方式的模型有qwen.3.6 和qwen3.7以及他们的子版本，例如：

| 模型 ID | 说明 |
|---|---|
| `qwen3.7-max` | 旗舰模型，效果最好 |
| `qwen3.7-plus` | 均衡性能 |
| `qwen3.6-plus` | 轻量高效 |
| `qwen3.6-flash` | 速度最快 |

> 其他模型（如 DeepSeek）不兼容 OpenAI 格式，请使用其他方法

### 4. 设置 API Key 环境变量

将 `你的百炼APIKey` 替换为第二步获取的 API Key。

**Windows PowerShell（永久生效，推荐）：**

```powershell
[System.Environment]::SetEnvironmentVariable("OPENAI_API_KEY", "你的百炼APIKey", "User")
```

设置完后关闭并重新打开 PowerShell 生效。

**Windows PowerShell（临时生效，不需要重启窗口）：**

```powershell
$env:OPENAI_API_KEY = "你的百炼APIKey"
```

**macOS / Linux（`~/.zshrc` 或 `~/.bashrc`）：**

```bash
export OPENAI_API_KEY="你的百炼APIKey"
source ~/.zshrc
```

验证是否设置成功：

```powershell
echo $env:OPENAI_API_KEY
```

输出你的 Key 说明设置成功。

---
### 4. 重启Codex App

## 方法二：使用 CC-Switch

CC-Switch 是一个代理工具，可以将任意模型的 API 转换为 OpenAI 兼容格式，适合 DeepSeek 等不直接兼容的模型，也同样支持兼容 OpenAI 格式的模型。

### 1. 下载 CC-Switch

前往 GitHub Releases 页面：https://github.com/farion1231/cc-switch/releases

页面较长，搜索 **Assets**，找到：

```
Windows-Portable.zip
```

下载免安装压缩包，解压即可直接使用，无需安装。

### 2. 启动 CC-Switch 并配置

解压后打开 CC-Switch 程序。

### 3. 开通火山引擎，获取免费额度

1. 打开火山引擎：https://console.volcengine.com/ark/region:ark+cn-beijing/apiKey
2. 登录或注册账号，完成实名认证后可获得更多免费额度 
3. 找到「开通管理」，开通模型 
4. 进入「模型授权」页面，授权你要使用的模型。只有通过授权的接入点调用，数据才会被采集并产生奖励。  
5. 通过授权的接入点调用模型，每日用量会按模型维度累积，**次日 11 点后**获得对应用量的奖励资源包（有效期 30 天）。
6. 在控制台「API Key 管理」页面创建并复制 Key


### 4. 重新启动 Codex

确保 CC-Switch 正在运行，然后打开 Codex 桌面 App 即可使用。

---
### 第三种办法使用codex ++
下载并安装
```
https://github.com/BigPizzaV3/CodexPlusPlus/releases
````
打开Codex++ 管理工具进行配置，不要直接打开codex ++
