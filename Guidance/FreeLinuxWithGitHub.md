# 5分钟拥有你的网页云电脑

无需安装任何客户端，只要一个浏览器和 GitHub 账号，就能拥有一台免费的 Linux 云桌面。

## 第一步：创建 GitHub Codespaces

1. 打开 GitHub 并登录账号
2. 点击左上角 **☰ 菜单**
3. 选择 **Codespaces**
4. 创建一个新的 Codespace
   - 推荐选择 **Jupyter Notebook**
   - 或者选择 **Blank（空白）模板**

## 第二步：部署 Linux 桌面

### 获取 Root 权限

```bash
sudo su
```

### 创建 Docker 配置文件

```bash
cat > docker-compose.yml <<EOF
services:
  debian-desktop:
    image: lscr.io/linuxserver/webtop:debian-xfce
    container_name: debian_gui
    privileged: true
    ports:
      - '6080:3000'
EOF
```


### 启动云桌面

```bash
docker-compose up -d
```

> 提示：首次部署需要下载约 1.2GB 的镜像文件，大约需要 5 分钟。

## 第三步：进入网页 Linux 桌面

1. 点击底部 **Ports（端口）**
2. 找到 **6080** 端口
3. 点击右侧的 **🌐 小地球图标**

即可进入 Linux 图形桌面。

## 云电脑休眠怎么办？

重新打开 Codespace 后，在终端执行：

```bash
docker-compose up -d
```

几秒钟后，桌面和数据都会恢复。

## 常用命令

获取 Root 权限：

```bash
sudo su
```

启动云桌面：

```bash
docker-compose up -d
```

查看容器状态：

```bash
docker ps
```

停止云桌面：

```bash
docker-compose down
```

🎉 恭喜！现在你已经拥有了一台运行在浏览器中的免费 Linux 云电脑。
