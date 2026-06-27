# ImageGen 安装与使用教程

## 1. 下载程序

下载并解压 ImageGen 程序压缩包。
https://drive.google.com/file/d/1I-KFUHHIAQN-ZTizlrpMHwx6fYG-Lqtl/view?usp=sharing

---

## 2. 安装 Python 3.11（仅需一次）。 必须是这个版本，最新版的不支持

### 方法一：官网下载

https://www.python.org/downloads/release/python-31113/

### 方法二：winget 安装

```bash id="p1"
winget install Python.Python.3.11
```

---

## 3. 创建并激活虚拟环境

每次运行前执行：

```bash id="p2"
py -3.11 -m venv .venv
.venv\Scripts\activate
```

---

## 4. 安装 Python 依赖库（仅需一次）

```bash id="p3"
pip install selenium undetected-chromedriver pyperclip
```

---

## 5. 使用程序生成图片（核心步骤）

完成依赖安装后，直接运行程序即可开始生成图片。

程序会自动执行以下流程：

* 读取配置文件 `configs.json`
* 读取 Prompt 文件
* 打开 Chrome 并访问目标网站
* 自动输入提示词生成图片
* 下载图片到本地目录

---
## ⚙️ Google Flow 配置
必须选择gird，不要选batch
可以自己选择图片的比例，选择Nano banano   
设置一次只生成一张图片  

```
## ⚙️ 关键配置说明（configs.json）

配置文件路径：

```
ImageGen\input\configs\configs.json
```

### 重要参数说明：

* `CHROME_USER_DATA_DIR`
  Chrome 用户数据目录，用于保存登录状态与 Cookie
  👉 路径：`C:\ImageGen\chrome-data`

* `INPUT_FILE`
  提示词文件路径
  👉 `input\prompts\image_prompts.txt`

* `START_LINE`
  从第几行开始执行（从 1 开始）

* `START_IMAGE_NUMBER`
  图片编号起始值，用于避免覆盖已有图片

---

## 💡 提示词文件说明

路径：

```
input\prompts\image_prompts.txt
```

规则：

* 每一行是一个 Prompt
* 程序按顺序逐行生成图片
* 可通过 `START_LINE` 控制从哪一行开始

---

## 🛑 防止程序中断（重要）

如果需要无人值守运行：

### 方法一（推荐）

关闭睡眠模式：

* Windows 设置 → 电源与睡眠 → 设为“从不”

### 方法二（可选）

使用 AutoHotkey：

https://www.autohotkey.com/

每分钟模拟一次鼠标操作，防止系统进入待机。

---

## 📁 程序运行结果

生成的图片会自动保存到：

```
C:\ImageGen\Download
```

如果目录不存在会自动创建。

---

## ⚡ 使用流程总结

1. 解压程序
2. 安装 Python 3.11
3. 创建虚拟环境
4. 安装依赖
5. 配置 `configs.json`
6. 编辑 Prompt 文件
7. 运行程序生成图片
