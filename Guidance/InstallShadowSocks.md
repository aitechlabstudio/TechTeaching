# Shadowsocks 安装教程

## 环境要求

- Ubuntu 16.10 及以上版本

---

## 第一步：安装 shadowsocks-libev

```bash
sudo apt install shadowsocks-libev
```
如果提示找不到这个程序，需要执行下面的命令更新apt 再安装
```bash
sudo apt update
```

---

## 第二步：修改配置文件

使用 `cat` 命令覆写配置文件 `/etc/shadowsocks-libev/config.json`：

```bash
cat > /etc/shadowsocks-libev/config.json << 'EOF'
{
    "server":["::1", "YOUR_SERVER_IP"],
    "mode":"tcp_and_udp",
    "server_port":443,
    "local_port":1080,
    "password":"YOUR_PASSWORD",
    "timeout":86400,
    "method":"aes-128-gcm"
}
EOF
```

### 配置项说明

| 参数 | 说明 |
|------|------|
| `server` | 服务器监听地址，`::1` 为 IPv6 本地，`YOUR_SERVER_IP` 为服务器公网 IP |
| `mode` | 传输模式，`tcp_and_udp` 同时支持 TCP 和 UDP |
| `server_port` | 服务端口，此处为 `443` |
| `local_port` | 本地代理端口，此处为 `1080` |
| `password` | 连接密码 |
| `timeout` | 超时时间（秒） |
| `method` | 加密方式，此处为 `aes-128-gcm` |

---

## 第三步：重启服务

```bash
sudo systemctl restart shadowsocks-libev
```

---

## 第四步：验证服务状态

```bash
sudo systemctl status shadowsocks-libev
```

输出中看到 `active (running)` 表示服务运行正常：

```
● shadowsocks-libev.service - Shadowsocks-libev Default Server Service
     Loaded: loaded (/lib/systemd/system/shadowsocks-libev.service; enabled)
     Active: active (running) since ...
```

---

## 常用管理命令

```bash
# 启动服务
sudo systemctl start shadowsocks-libev

# 停止服务
sudo systemctl stop shadowsocks-libev

# 重启服务
sudo systemctl restart shadowsocks-libev

# 查看服务状态
sudo systemctl status shadowsocks-libev

# 设置开机自启
sudo systemctl enable shadowsocks-libev
```

---

## 客户端配置：v2rayN（Windows）

v2rayN 是 Windows 上常用的代理客户端，支持 Shadowsocks 协议。

### 下载安装

前往 [v2rayN GitHub Releases](https://github.com/2dust/v2rayN/releases) 下载最新版本，解压后运行 `v2rayN.exe`。

### 添加 Shadowsocks 服务器

1. 打开 v2rayN，点击顶部菜单 **「服务器」**
2. 选择 **「添加Shadowsocks服务器」**
3. 按以下信息填写：

| 字段 | 填写内容 |
|------|----------|
| 别名 | 随意填写，如 `My SS` |
| 地址 | `YOUR_SERVER_IP` |
| 端口 | `443` |
| 密码 | `YOUR_PASSWORD` |
| 加密方式 | `aes-128-gcm` |

4. 点击 **「确定」** 保存

### 启动代理

1. 在服务器列表中选中刚添加的节点
2. 右键点击系统托盘图标（任务栏右下角）
3. 选择 **「系统代理」→「自动配置系统代理」**
4. 状态栏显示连接成功即可

---

## 验证代理是否生效

配置完成后，通过以下方法确认流量是否走代理。

### 方法一：浏览器访问

打开浏览器，访问以下任意网站：

| 网站 | 地址 |
|------|------|
| ipinfo.io | https://ipinfo.io |
| ip.sb | https://ip.sb |
| ip-api.com | https://ip-api.com |

**判断方法：** 页面显示的 IP 地址如果是 `YOUR_SERVER_IP`，说明代理生效 ✓  
如果显示的是本机宽带 IP，说明代理未生效 ✗

### 方法二：终端命令验证

```bash
curl ipinfo.io
```

输出示例（代理生效）：

```json
{
  "ip": "YOUR_SERVER_IP",
  "city": "...",
  "region": "...",
  "country": "...",
  "org": "..."
}
```

若 `ip` 字段显示为 `YOUR_SERVER_IP`，即代理配置正确。
