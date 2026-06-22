# 使用 Cloudflare 搭建免费“梯子”全攻略

本教程介绍如何巧妙利用 Cloudflare 提供的免费边缘计算服务（Cloudflare Workers / Pages），轻松搭建一个稳定、免费且具备极高伪装性的网络中转通道。

---

## 一、 为什么选择 Cloudflare？它有什么优点？

* **完全免费**：Cloudflare 为免费账户提供每天高达 **100 万次** 的 Workers 请求额度，对于个人日常科学上网而言绰绰有余。
* **极强抗封锁性**：由于你的流量走的是 Cloudflare 的官方正规 CDN 节点，防火墙看到的只是你在访问一个普通的 HTTPS 网站。只要 Cloudflare 的官方 IP 没被完全封锁，你的通道就永远可用。
* **免去购买服务器的费用**：传统的科学上网需要租用海外 VPS（如搬瓦工、Vultr 等），而使用本方法你**不需要购买任何服务器**。
* **任性自选 IP**：Cloudflare 在全球拥有众多数据中心。国内不同网络（电信、联通、移动）可以通过“自选优质 IP”的方法，获得极低的延迟和极高的带宽速度。

---

## 二、 核心原理：它为什么能实现网络加速？

Cloudflare 本质上是一个 **CDN（内容分发网络）** 和**反向代理服务**。

* **正常 CDN 用途**：网站主把网站托管在 CF 上，用户访问该网站时，流量先到达 CF 的边缘节点，再由 CF 转发给真实的网站服务器。
* **我们的“伪装”原理**：我们在 Cloudflare Workers 上部署一段开源代码（通常是 Vless 或 Trojan 协议的轻量实现）。这段代码本质上变成了一个“流量转发器”。
* **流量走向**：当你通过客户端发起网络请求时，客户端会把这些翻墙流量伪装成标准的、加密的 HTTPS 网站流量发送给 Cloudflare。
* **解密与转发**：Cloudflare 收到请求后，误以为这是普通的网页访问，然后通过其 Workers 脚本解密并提取出你的真实目标网址（如 Google、YouTube），由 Cloudflare 的骨干网络帮你去访问，最后再把结果原路返回给你。

> 💡 **总结**：通过这种方式，GFW（防火墙）只能看到你和 Cloudflare 之间在进行合法的 HTTPS 加密通信，从而实现了完美的伪装。

---

## 三、 详细搭建步骤
### Step 1. 下载开源代码
在部署之前，需要先下载用于伪装成网页应用程序的开源项目压缩包：
* **下载地址**：[https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip](https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip)
* *注：请将此 zip 压缩包下载到本地，无需解压。*

### Step 2. 注册 Cloudflare 账号
* 打开 Cloudflare 中文版主页：[https://www.cloudflare.com/zh-cn/](https://www.cloudflare.com/zh-cn/)
* 点击右上角进行注册并登录。
* 登录后，点击页面右上角的 **用户头像图标**。
* 在下拉菜单中选择 **Language（语言）**。
* 选中 **简体中文**。

### Step 3. 创建 KV 命名空间（数据库）
> **什么是 KV 命名空间？** KV 是 Key-Value 的缩写，每一个 key 对应一个 value（键值对映射）。它是一种非关系型的、Serverless（无服务器）数据库。

1. 在左侧导航栏中找到并点击 **存储与数据库** -> **KV**。
2. 点击 **创建命名空间**，输入一个名称（例如 `edgetunnel-db`），点击保存。


### Step 4. 在 Cloudflare 中部署 Pages 应用程序
1. 在左侧导航栏点击计算下面的 **AI 与 Workers (Workers & Pages)**。
2. 点击 **创建** -> 选择 **Pages** 选项卡 -> 点击 **上传资产**。
3. 输入您的项目名称，然后点击 **创建项目**。
4. **上传代码**：直接将刚刚下载的 `main.zip` 包含代码的压缩包拖到网页页面上的上传区域中，完成代码上传。

### Step 5. 绑定 KV 数据库与环境变量
1. 部署完成后，进入该 Pages 项目的后台，点击 设置 -> 绑定-> 添加-> 添加资源绑定->  
2. 找到 **KV 命名空间** 区域，点击 **添加绑定**。
3. 变量名称必须严格填写为：`KV` *(注：应用程序代码中使用的是固定名字，请勿修改)*
4. 在 **KV 命名空间** 下拉菜单中，选择您在 *Step 3* 中创建的那个 KV 数据库。
5. 找到 **环境变量** 区域，点击 **添加变量**，设置管理员密码：
   * **变量名称**：`ADMIN`
   * **值**：`123456` *(注：建议将其修改为您自己复杂的密码)*
6. 点击 **保存**，并重新点击 **创建部署** 让配置生效。

### Step 6. 注册并接管域名
由于 Cloudflare 自带的分配域名（如 `.pages.dev`）在国内部分地区可能被墙，强烈建议绑定自己的自定义域名。

1. **注册免费域名**（任选其一访问）：
   ```
   https://my.dnshe.com/index.php?m=domain_hub&view=tools&invite_code=UUP5ZVLXJ4CH)
   https://my.dnshe.com/index.php?m=domain_hub&view=tools&invite_code=NZLV55V7ZAHF)
   ```
2. **添加域名到 CF**：登录 Cloudflare，点击 **域名** -> **概览** -> **添加站点（连接域名）**。
3. **选择免费套餐**：选择最下方的 **Free $0** 免费套餐。
4. **修改 DNS 服务器**：根据 Cloudflare 的提示，登录你注册域名的网站（DNSHE），把域名的 DNS 服务器修改为 Cloudflare 指定的两个服务器地址。等待解析生效后，Cloudflare 就成功接管了该域名。

### Step 7. 绑定自定义域名
1. 回到 Cloudflare 的 **AI 与 Workers** -> **Workers & Pages**，点击进入你刚才创建的 Pages 项目。
2. 切换到 **自定义域** 选项卡，点击 **设置自定义域**。
3. 输入你在上一步接管的域名（例如 `mydomain.com` 或二级域名 `vpn.mydomain.com`），点击激活绑定。

---

## 四、 获取订阅与客户端配置

### 1. 进入管理后台
等待域名解析完全生效后，在浏览器输入您的域名并加上 `/admin` 后缀：
```text
[https://你的域名.com/admin](https://你的域名.com/admin)
```
页面会提示输入密码，输入您在环境变量中设置的 ADMIN 密码（例如 123456）。

### 2. 复制订阅信息
成功登录后台管理界面后，您可以在页面中直接看到生成的 **Vless 节点配置** 和 **订阅链接**，直接点击一键复制即可。

### 3. 下载客户端进行连接
推荐使用以下客户端添加复制的订阅或节点信息：

* **v2rayN (Windows 推荐)**：
  [https://github.com/2dust/v2rayN/releases](https://github.com/2dust/v2rayN/releases)  
  Android: https://github.com/2dust/v2rayNG/releases

> 🚀 **使用方法**：下载后解压，导入您在后台复制的节点或订阅链接，开启系统代理即可畅享自由网络！
