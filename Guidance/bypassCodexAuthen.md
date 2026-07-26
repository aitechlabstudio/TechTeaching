# 一键导出 ChatGPT 登录凭证，自动生成 `auth.json`

本教程将演示如何使用开源工具 **Codex Auth Helper**，一键导出 ChatGPT 登录凭证，并自动生成 `auth.json` 文件。

> **开源项目：**
>
> https://github.com/zhishile/codex-auth-helper

---

## 第一步：下载工具

1. 打开 GitHub 项目页面：
   https://github.com/zhishile/codex-auth-helper

2. 点击页面右上角绿色的 **Code** 按钮。

3. 选择 **Download ZIP**，下载整个项目压缩包。

4. 解压 ZIP 文件到任意目录。

---

## 第二步：安装 浏览器 插件

### 1. 打开扩展程序页面

Chrome 浏览器，在地址栏输入：

```
chrome://extensions/
```
Edge浏览器， 在地址栏输入：
```
edge://extensions/
```

然后按 **Enter**。

---

### 2. 开启开发者模式

在页面右上角打开：

**Developer mode（开发者模式）**

---

### 3. 加载插件

点击左上角：

**Load unpacked（加载已未打包的扩展程序）**

然后选择刚刚解压后的项目中的：

```
extension
```

文件夹（也就是包含 `manifest.json` 的目录）。

安装完成后，你会看到 **Codex 认证助手** 已成功安装。

---

### 4. 固定插件

点击浏览器右上角的 **拼图** 图标（Extensions）。

找到 **Codex 认证助手**，点击右侧的 **图钉** 图标，将插件固定到工具栏，方便后续使用。

---

# 第三步：使用插件导出 `auth.json`

## 1. 登录 ChatGPT

确保当前 Chrome 浏览器已经登录：

> https://chatgpt.com

## 2. 打开插件 并点击导出身份信息

---

# 第四步：把auth.json文件拷贝到.codex目录里

Windows:
```
C:\Users\<你的用户名>\.codex\
```
macOS / Linux
```
~/.codex/
```

里面通常会包含：
```
.codex
│
├── auth.json          ← 登录凭证（用导出的文件替换这个）
├── config.toml        ← Codex 配置文件
```

如何快速打开（Windows）

直接在文件浏览器输入
```
%USERPROFILE%\.codex
```
