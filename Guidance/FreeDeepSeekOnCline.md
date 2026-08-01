# 免费使用 DeepSeek V4 Flash 教程

> 🚀 三步即可上手，无需 API Key，完全免费。

---

## 第一步：安装 Node.js

### 方法一：使用命令行安装（推荐）

打开 **PowerShell**，输入：

```powershell
winget install OpenJS.NodeJS.LTS
```

等待安装完成即可。

---

### 方法二：官网下载

访问官网：

👉 https://nodejs.org/

然后：

1. 点击左侧绿色 **LTS** 按钮下载
2. 双击下载好的 `.msi` 安装包
3. 按照安装向导完成安装

---

### 验证安装

打开 PowerShell，输入：

```powershell
node -v
npm -v
```

如果能够看到版本号，例如：

```text
v22.18.0
10.9.3
```

说明安装成功。

---

# 第二步：安装 Cline

打开 PowerShell，执行：

```powershell
npm install -g cline
```

等待安装完成。

---

# 第三步：启动并配置

## 启动 Cline

```powershell
cline
```

---

## 登录账号

第一次启动会提示登录：

1. 浏览器会自动打开登录页面
2. 注册 Cline 账号，或者直接使用 Google 登录
3. 登录成功后关闭网页
4. 返回终端即可

---

## 选择模型

打开：

**Open → Settings**

找到：

**Cline Provider**

然后选择：

**DeepSeek V4 Flash**

配置完成。

---

# 第四步：测试

在 Cline 中输入：

```text
帮我做一个鹈鹕骑自行车的SVG 动画
```

几秒钟后即可生成完整可运行的代码。

---

# 常见问题（FAQ）

| 问题 | 解决方法 |
|------|----------|
| winget 找不到 | 更新 Windows，或从 Microsoft Store 安装 **应用安装程序（App Installer）** |
| npm 找不到 | 关闭 PowerShell 后重新打开 |
| 安装时报权限错误 | 使用管理员身份运行 PowerShell |
| 登录页面打不开 | 手动复制终端中的链接到浏览器打开 |
| 模型列表找不到 DeepSeek V4 Flash | 确认已成功登录，并检查网络连接 |
| 生成的代码无法运行 | 检查文件是否完整保存，或重新生成一次 |

---

# 相关链接

| 名称 | 地址 |
|------|------|
| Node.js 官网 | https://nodejs.org/ |
| Cline 官网 | https://cline.ai/ |
| DeepSeek 官网 | https://deepseek.com/ |

---

# 总结

整个过程只需四步：

1. 安装 Node.js
2. 安装 Cline
3. 登录并选择 **DeepSeek V4 Flash**
4. 开始使用 AI 编程

整个流程无需申请 API Key，安装完成即可免费体验 DeepSeek V4 Flash。
