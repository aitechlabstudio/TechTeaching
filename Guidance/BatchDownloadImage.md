# ImageGen 安装与使用教程

## 1. 下载程序

请先下载并解压本项目的压缩包（ImageGen 程序）。
https://drive.google.com/file/d/1I-KFUHHIAQN-ZTizlrpMHwx6fYG-Lqtl/view?usp=sharing
---

## 2. 安装 Python 3.11（仅需一次）

### 方法一：官网下载

https://www.python.org/downloads/release/python-31113/

### 方法二：使用 winget 安装（推荐）

```bash id="1a9k3x"
winget install Python.Python.3.11
```

---

## 3. 创建并激活虚拟环境

每次运行程序前需要执行一次（在项目目录中运行）：

```bash id="v2k9q1"
py -3.11 -m venv .venv
.venv\Scripts\activate
```

---

## 4. 安装 Python 依赖库（仅需一次）

```bash id="p7x3ld"
pip install selenium undetected-chromedriver pyperclip
```

---

## 5. 防止程序中断（重要）

如果需要无人值守运行，请确保电脑不会进入睡眠状态，否则下载会中断。

### 方法一：关闭睡眠模式（推荐）

Windows 设置：

* 设置 → 电源与睡眠 → 睡眠 → 设为“从不”

---

### 方法二：使用 AutoHotkey 保持唤醒

下载地址：

https://www.autohotkey.com/

可以使用脚本每分钟模拟一次鼠标活动，从而保持窗口活跃，防止系统进入待机状态。

---

## 6. 程序目录说明

### 📁 C:\ImageGen\chrome-data

Chrome 浏览器用户数据目录，用于保存：

* 登录状态
* Cookie
* 浏览器配置

#### ⚠️ 常见问题处理

如果出现以下情况，可以删除该目录：

* 无法访问目标网站
* 登录失效
* 页面加载异常
* 浏览器异常

程序会在下次启动时自动重新创建。

---

### 📁 C:\ImageGen\Download

图片下载目录：

* 所有生成的图片都会保存到这里
* 如果目录不存在会自动创建

---

### 📁 ImageGen\input\configs\configs.json

程序配置文件路径

---

## 7. 配置文件说明（configs.json）

```jsonc id="c8m2kq"
{
    // AI 图片生成网页地址（通常无需修改）
    "TARGET_URL": "https://labs.google/fx/tools/flow",

    // Chrome 浏览器路径
    "CHROME_BINARY_PATH": "Chrome\\chrome-win64\\chrome.exe",

    // ChromeDriver 路径（需与 Chrome 版本匹配）
    "CHROME_DRIVER_PATH": "Chrome\\chromedriver-win64\\chromedriver.exe",

    // Chrome 主版本号
    "CHROME_VERSION_MAIN": 149,

    // Chrome 用户数据目录（保存登录信息）
    "CHROME_USER_DATA_DIR": "C:\\ImageGen\\chrome-data",

    // 输入提示词文件
    "INPUT_FILE": "input\\prompts\\image_prompts.txt",

    // 从第几行开始执行（从 1 开始）
    "START_LINE": 2,

    // 图片编号起始值（避免覆盖旧图片）
    "START_IMAGE_NUMBER": 2
}
```

---

## 8. 使用流程总结

1. 解压程序
2. 安装 Python 3.11
3. 创建虚拟环境
4. 安装依赖
5. 修改 configs.json（如需要）
6. 运行程序
7. 图片自动下载到 `C:\ImageGen\Download`

---

## 9. 总结

* Python 只需安装一次
* 依赖库只需安装一次
* 虚拟环境每次运行都要激活
* 下载目录自动创建
* Chrome 数据异常可删除 `chrome-data`
