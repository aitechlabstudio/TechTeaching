# 百度/夸克网盘高速下载教程

## 一、准备工具

### 1. 安装篡改猴测试版
Chrome 商店搜索安装 **Tampermonkey Beta**，
```
https://chromewebstore.google.com
```
或直接访问：
```
https://chromewebstore.google.com/detail/tampermonkey-beta/gcalenpjmijncebpfijmoaglllgpjagf
```

### 2. 安装 Motrix 下载器
访问官网下载安装，保持默认端口 16800：
```
https://motrix.app/download
```

## 二、安装脚本

打开脚本地址，复制全部代码：
```
https://github.com/aitechlabstudio/TechTeaching/blob/main/Code/FastDownload.js
```
这个脚本是来自于
```
http://hd2a.page.gd/assets/min.baidu.user.js
```
我做了修改，绕开了打卡充值的步骤，可以直接使用，不需要充值。   

#### 安装步骤
点击浏览器右上角篡改猴图标 → **添加新脚本** → 粘贴代码 → `Ctrl+S` 保存。

## 三、百度网盘使用

1. 打开百度网盘网页版，切换到**旧版界面**
2. 勾选要下载的文件，点击页面紫色「下载」按钮
3. **大于 300MB 的文件**采用共享中转方式下载：脚本自动创建临时共享文件夹（如 `E4553AF`），文件先移到该目录再解析高速链接
4. 确保 Motrix 运行中，文件会自动推送到 Motrix 高速下载
5. **下载完成后建议**：把文件从临时共享目录移回原位，并取消/删除该共享文件夹，避免长期共享风险

## 四、夸克网盘不建议使用这个办法

> 💡 容易封号
