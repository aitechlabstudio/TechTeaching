# Shadowsocks 安装教程

## 环境要求

- Ubuntu 16.10 及以上版本

---

## 第一步：安装 shadowsocks-libev

```bash
sudo apt update
sudo apt install shadowsocks-libev
```

---

## 第二步：修改配置文件

使用 `cat` 命令覆写配置文件 `/etc/shadowsocks-libev/config.json`：

```bash
cat > /etc/shadowsocks-libev/config.json << 'EOF'
{
    "server":["::1", "IP地址"],
    "mode":"tcp_and_udp",
    "server_port":443,
    "local_port":1080,
    "password":"Hello123",
    "timeout":86400,
    "method":"aes-128-gcm"
}
EOF
```

### 配置项说明

| 参数 | 说明 |
|------|------|
| `server` | 服务器监听地址，`::1` 为 IPv6 本地，`IP地址` 为服务器公网 IP |
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
