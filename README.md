# 🚀 edge2
一个功能强大的基于 Cloudflare Workers/Pages 平台的网络工具，支持 VLESS 协议并提供灵活的订阅转换功能。该项目允许用户将 VLESS 配置信息转换为多种订阅格式（如 Clash、Singbox、Base64 等），便于在各类客户端中使用。

主要特点：
- ✅ 支持 Cloudflare Workers 和 Pages 多种部署方式
- ✅ 支持 VLESS 协议和多种订阅格式转换
- ✅ 提供动态 UUID 和密钥验证机制
- ✅ 支持优选 IP/域名和自定义配置
- ✅ 丰富的环境变量配置选项
- ✅ 兼容主流客户端

## 🚦 快速开始

1. **准备工作**
   - 注册 Cloudflare 账户
   - 生成 UUID（可通过在线工具生成）

2. **部署方式选择**（三选一）
   - [Cloudflare Workers 部署](#-workers-部署方法)
   - [Cloudflare Pages 上传文件部署](#-pages-上传-部署方法-最佳推荐)
   - [Cloudflare Pages GitHub 部署](#-pages-github-部署方法)

3. **获取订阅链接**
   ```
   https://[YOUR-URL]/[YOUR-UUID]
   ```

4. **在客户端中使用**
   - 根据客户端类型选择合适的订阅格式（?clash、?sb、?sub 等参数）
   - 将订阅链接导入到对应的客户端中

## 📋 部署方法详解

### 🛠️ Workers 部署方法

1. **创建 Worker**
   - 登录 Cloudflare 控制台 → Workers 和 Pages
   - 点击创建应用 → 创建 Worker
   - 命名并部署
   
2. **编辑代码**
   - 点击编辑代码
   - 复制 `_worker.js` 文件内容并粘贴到编辑器中
   - 保存并部署
   
3. **绑定环境变量**（可选）
   - 前往设置 → 变量 → 环境变量
   - 添加所需变量（如 `PROXY_DOMAIN`、`PROXY_IP` 等）
   - 保存并重新部署

### 📄 Pages 上传部署方法（最佳推荐）

1. **准备文件**
   - 创建文件夹，包含 `_worker.js` 文件（无其他文件）
   - 压缩为 ZIP 文件
   
2. **创建 Pages**
   - Cloudflare 控制台 → Workers 和 Pages → 创建应用 → Pages
   - 点击「上传资产」→ 选择 ZIP 文件
   - 自定义项目名称 → 部署

### 🌐 Pages GitHub 部署方法

1. **准备代码库**
   - 创建 GitHub 仓库，包含 `_worker.js` 文件
   - 推送代码
   
2. **连接 Pages**
   - Cloudflare 控制台 → Workers 和 Pages → 创建应用 → Pages
   - 连接到 Git → 选择仓库
   - 配置构建设置（无需构建命令，输出目录留空）
   - 开始部署

## 🔧 环境变量配置

| 变量名 | 说明 | 默认值 | 示例 |
|--------|------|--------|------|
| `PROXY_DOMAIN` | 域名 | 无 | example.com |
| `PROXY_IP` | IP | 无 | 1.1.1.1 |
| `SUB_PATH` | 订阅路径 | / | /sub |
| `USER_ID` | 用户 ID | 随机 UUID | 550e8400-e29b-41d4-a716-446655440000 |
| `SUBCONVERTER_URL` | 订阅转换服务 | 无 | https://api.subconverter.com/sub |

## 📱 客户端使用指南

### 订阅链接参数说明

```
https://[YOUR-URL]/[YOUR-UUID]?[PARAMS]
```

常用参数：
- `?clash` - 获取 Clash 配置格式
- `?clash=base64` - 获取 Base64 编码的 Clash 配置
- `?sb` - 获取 Singbox 配置格式
- `?sub` - 获取 VLESS 订阅格式
- `?base64` - 获取 Base64 编码

### 推荐客户端

- **Windows**：Clash for Windows、Singbox GUI
- **macOS**：ClashX、Singbox GUI
- **Android**：Clash for Android、v2rayNG
- **iOS**：Quantumult X、Shadowrocket

## ❌ 常见问题与故障排除

### 订阅链接无法访问
- 检查 Worker/Pages 是否正常部署
- 确认 UUID 格式正确
- 查看 Cloudflare 防火墙是否拦截

### 连接不稳定
- 尝试添加 `PROXY_IP` 环境变量使用优选 IP
- 切换不同的 Cloudflare 节点
- 检查域名是否被墙

### 订阅格式错误
- 确认使用了正确的参数格式
- 尝试使用不同的客户端导入
- 检查是否需要 Base64 编码

## 🔍 项目结构说明

- `_worker.js` - 主要代码文件，包含所有核心功能
- `brace_check.js` - 括号检查脚本，用于验证代码括号匹配
- `validate.js` - 代码验证脚本，用于检查语法错误
- `README.md` - 项目说明文档

## ⚙️ 开发与调试

### 本地测试

1. **安装 Wrangler**
   ```bash
   npm install -g wrangler
   ```

2. **登录认证**
   ```bash
   wrangler login
   ```

3. **本地开发服务器**
   ```bash
   wrangler dev --local _worker.js
   ```

4. **测试订阅链接**
   ```
   http://localhost:8787/[YOUR-UUID]
   ```

### 代码贡献指南

1. Fork 项目仓库
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 开启 Pull Request

## 📜 许可证

本项目采用 MIT 许可证 - 详见 LICENSE 文件

## 🎯 免责声明

本项目仅用于学习和研究目的，请勿用于任何非法活动。用户应当遵守所在国家/地区的法律法规，不得侵犯他人合法权益。

## 🌟 鸣谢

感谢所有为本项目做出贡献的开发者和用户！

如有任何问题或建议，欢迎提交 Issues 或 Pull Requests。


作者保留随时更新本免责声明的权利，且不另行通知。最新版本的免责声明将发布在本项目的 GitHub 页面上。

## 🔥 风险提示
- 通过提交虚假的节点配置给订阅服务，避免节点配置信息泄露。
- 另外，您也可以选择自行部署 [WorkerVless2sub 订阅生成服务](https://github.com/cmliu/WorkerVless2sub)，这样既可以利用订阅生成器的便利。
   
## 💡 如何使用?
### ⚙️ Workers 部署方法 [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=191s)

<details>
<summary><code><strong>「 Workers 部署文字教程 」</strong></code></summary>

1. 部署 CF Worker：
   - 在 CF Worker 控制台中创建一个新的 Worker。
   - 将 [worker.js](https://github.com/cmliu/edgetunnel/blob/main/_worker.js) 的内容粘贴到 Worker 编辑器中。
   - 将第 4 行 `userID` 修改成你自己的 **UUID** 。

2. 访问订阅内容：
   - 访问 `https://[YOUR-WORKERS-URL]/[UUID]` 即可获取订阅内容。
   - 例如 `https://vless.google.workers.dev/90cd4a77-141a-43c9-991b-08263cfe9c10` 就是你的通用自适应订阅地址。
   - 例如 `https://vless.google.workers.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://vless.google.workers.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://vless.google.workers.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sb` singbox订阅格式，适用singbox等。

3. 给 workers绑定 自定义域： 
   - 在 workers控制台的 `触发器`选项卡，下方点击 `添加自定义域`。
   - 填入你已转入 CF 域名解析服务的次级域名，例如:`vless.google.com`后 点击`添加自定义域`，等待证书生效即可。
   - **如果你是小白，你现在可以直接起飞，不用再往下看了！！！**

4. 使用自己的`优选域名`/`优选IP`的订阅内容：
   - 如果你想使用自己的优选域名或者是自己的优选IP，可以参考 [WorkerVless2sub GitHub 仓库](https://github.com/cmliu/WorkerVless2sub) 中的部署说明自行搭建。
   - 打开 [worker.js](https://github.com/cmliu/edgetunnel/blob/main/_worker.js) 文件，在第 12 行找到 `sub` 变量，将其修改为你部署的订阅生成器地址。例如 `let sub = 'sub.cmliussss.workers.dev';`，注意不要带https等协议信息和符号。
   - 注意，如果您使用了自己的订阅地址，要求订阅生成器的 `sub`域名 和 `[YOUR-WORKER-URL]`的域名 不同属一个顶级域名，否则会出现异常。您可以在 `sub` 变量赋值为 workers.dev 分配到的域名。

</details>

### 🛠 Pages 上传 部署方法 **最佳推荐!!!** [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=436s)

<details>
<summary><code><strong>「 Pages 上传文件部署文字教程 」</strong></code></summary>

1. 部署 CF Pages：
   - 下载 [main.zip](https://github.com/cmliu/edge2/archive/refs/heads/main.zip) 文件，并点上 Star !!!
   - 在 CF Pages 控制台中选择 `上传资产`后，为你的项目取名后点击 `创建项目`，然后上传你下载好的 [main.zip](https://github.com/cmliu/edge2/archive/refs/heads/main.zip) 文件后点击 `部署站点`。
   - 部署完成后点击 `继续处理站点` 后，选择 `设置` > `环境变量` > **制作**为生产环境定义变量 > `添加变量`。
     变量名称填写**UUID**，值则为你的UUID，后点击 `保存`即可。
   - 返回 `部署` 选项卡，在右下角点击 `创建新部署` 后，重新上传 [main.zip](https://github.com/cmliu/edge2/archive/refs/heads/main.zip) 文件后点击 `保存并部署` 即可。

2. 访问订阅内容：
   - 访问 `https://[YOUR-PAGES-URL]/[YOUR-UUID]` 即可获取订阅内容。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10` 就是你的通用自适应订阅地址。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sb` singbox订阅格式，适用singbox等。
   
3. 给 Pages绑定 CNAME自定义域：[视频教程](https://www.youtube.com/watch?v=LeT4jQUh8ok&t=851s)
   - 在 Pages控制台的 `自定义域`选项卡，下方点击 `设置自定义域`。
   - 填入你的自定义次级域名，注意不要使用你的根域名，例如：
     您分配到的域名是 `fuck.cloudns.biz`，则添加自定义域填入 `lizi.fuck.cloudns.biz`即可；
   - 按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 `lizi`的 CNAME记录 `edge2.pages.dev` 后，点击 `激活域`即可。
   - **如果你是小白，那么你的 pages 绑定`自定义域`之后即可直接起飞，不用再往下看了！！！**
   
4. 使用自己的`优选域名`/`优选IP`的订阅内容：
   - 如果你想使用自己的优选域名或者是自己的优选IP，可以参考 [WorkerVless2sub GitHub 仓库](https://github.com/cmliu/WorkerVless2sub) 中的部署说明自行搭建。
   - 在 Pages控制台的 `设置`选项卡，选择 `环境变量`> `制作`> `编辑变量`> `添加变量`；
   - 变量名设置为`SUB`，对应的值为你部署的订阅生成器地址。例如 `sub.cmliussss.workers.dev`，后点击 **保存**。
   - 之后在 Pages控制台的 `部署`选项卡，选择 `所有部署`> `最新部署最右的 ...`> `重试部署`，即可。
   - 注意，如果您使用了自己的订阅地址，要求订阅生成器的 `SUB`域名 和 `[YOUR-PAGES-URL]`的域名 不同属一个顶级域名，否则会出现异常。您可以在 `SUB` 变量赋值为 Pages.dev 分配到的域名。

</details>

### 🛠 Pages GitHub 部署方法 [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=317s)

<details>
<summary><code><strong>「 Pages GitHub 部署文字教程 」</strong></code></summary>

1. 部署 CF Pages：
   - 在 Github 上先 Fork 本项目，并点上 Star !!!
   - 在 CF Pages 控制台中选择 `连接到 Git`后，选中 `edge2`项目后点击 `开始设置`。
   - 在 `设置构建和部署`页面下方，选择 `环境变量（高级）`后并 `添加变量`
     变量名称填写**UUID**，值则为你的UUID，后点击 `保存并部署`即可。

2. 访问订阅内容：
   - 访问 `https://[YOUR-PAGES-URL]/[YOUR-UUID]` 即可获取订阅内容。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10` 就是你的通用自适应订阅地址。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sub` Base64订阅格式，适用PassWall,SSR+等。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?clash` Clash订阅格式，适用OpenClash等。
   - 例如 `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sb` singbox订阅格式，适用singbox等。

3. 给 Pages绑定 CNAME自定义域：[视频教程](https://www.youtube.com/watch?v=LeT4jQUh8ok&t=851s)
   - 在 Pages控制台的 `自定义域`选项卡，下方点击 `设置自定义域`。
   - 填入你的自定义次级域名，注意不要使用你的根域名，例如：
     您分配到的域名是 `fuck.cloudns.biz`，则添加自定义域填入 `lizi.fuck.cloudns.biz`即可；
   - 按照 CF 的要求将返回你的域名DNS服务商，添加 该自定义域 `lizi`的 CNAME记录 `edge2.pages.dev` 后，点击 `激活域`即可。
   - **如果你是小白，那么你的 pages 绑定`自定义域`之后即可直接起飞，不用再往下看了！！！**

4. 使用自己的`优选域名`/`优选IP`的订阅内容：
   - 如果你想使用自己的优选域名或者是自己的优选IP，可以参考 [WorkerVless2sub GitHub 仓库](https://github.com/cmliu/WorkerVless2sub) 中的部署说明自行搭建。
   - 在 Pages控制台的 `设置`选项卡，选择 `环境变量`> `制作`> `编辑变量`> `添加变量`；
   - 变量名设置为`SUB`，对应的值为你部署的订阅生成器地址。例如 `sub.cmliussss.workers.dev`，后点击 **保存**。
   - 之后在 Pages控制台的 `部署`选项卡，选择 `所有部署`> `最新部署最右的 ...`> `重试部署`，即可。
   - 注意，如果您使用了自己的订阅地址，要求订阅生成器的 `SUB`域名 和 `[YOUR-PAGES-URL]`的域名 不同属一个顶级域名，否则会出现异常。您可以在 `SUB` 变量赋值为 Pages.dev 分配到的域名。

</details>

## 🔑 变量说明

| 变量名 | 示例 | 必填 | 备注 | YT |
|--------|---------|-|-----|-----|
| UUID | `90cd4a77-141a-43c9-991b-08263cfe9c10` |✅| 可输入任意值(非UUIDv4标准的值会自动切换成动态UUID) | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=72s) |
| KEY | `token` |❌| 动态UUID秘钥，使用变量`KEY`的时候，将不再启用变量`UUID`|  |
| TIME | `7` |❌| 动态UUID有效时间(默认值:`7`天)|  |
| UPTIME | `3` |❌| 动态UUID更新时间(默认值:北京时间`3`点更新) |  |
| SCV | `false`或`0` |❌| 是否跳过TLS证书验证(默认`true`开启跳过证书验证) |  |
| PROXYIP | `proxyip.cmliussss.net:443` |❌| 备选作为访问CFCDN站点的节点(支持自定义ProxyIP端口, 支持多ProxyIP, ProxyIP之间使用`,`或`换行`作间隔) | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=166s) |
| HTTP  | `user:password@127.0.0.1:8080`或`127.0.0.1:8080` |❌| 优先作为访问CFCDN站点的HTTP连接(支持多HTTP连接之间使用`,`或`换行`作间隔) | |
| SOCKS5  | `user:password@127.0.0.1:1080`或`127.0.0.1:1080` |❌| 优先作为访问CFCDN站点的SOCKS5连接(支持多socks5, socks5之间使用`,`或`换行`作间隔) | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=826s) |
| GO2SOCKS5  | `blog.cmliussss.com`,`*.ip111.cn`,`*google.com` |❌| 设置`SOCKS5`或`HTTP`变量之后，可设置强制使用socks5访问名单(设置为`*`可作为全局连接) ||
| ADD | `icook.tw:2053#官方优选域名` |❌| 本地优选TLS域名/优选IP(支持多元素之间`,`或`换行`作间隔) ||
| ADDAPI | [https://raw.github.../addressesapi.txt](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt) |❌| 优选IP的API地址(支持多元素之间`,`或 换行 作间隔) ||
| ADDNOTLS | `icook.hk:8080#官方优选域名` |❌| 本地优选noTLS域名/优选IP(支持多元素之间`,`或`换行`作间隔) ||
| ADDNOTLSAPI | [https://raw.github.../addressesapi.txt](https://raw.githubusercontent.com/cmliu/CFcdnVmess2sub/main/addressesapi.txt) |❌| 优选IP的API地址(支持多元素之间`,`或 换行 作间隔) ||
| ADDCSV | [https://raw.github.../addressescsv.csv](https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressescsv.csv) |❌| iptest测速结果(支持多元素, 元素之间使用`,`作间隔) ||
| DLS | `8` |❌| `ADDCSV`测速结果满足速度下限 ||
| CSVREMARK | `1` |❌| CSV备注所在列偏移量 ||
| TGTOKEN | `6894123456:XXXXXXXXXX0qExVsBPUhHDAbXXX` |❌| 发送TG通知的机器人token | 
| TGID | `6946912345` |❌| 接收TG通知的账户数字ID | 
| SUB | `SUB.cmliussss.net` | ❌ | 优选订阅生成器域名 | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=1193s) |
| SUBAPI | `SUBAPI.cmliussss.net` |❌| clash、singbox等 订阅转换后端 | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=1446s) |
| SUBCONFIG | [https://raw.github.../ACL4SSR_Online_Full_MultiMode.ini](https://raw.githubusercontent.com/cmliu/ACL4SSR/main/Clash/config/ACL4SSR_Online_Full_MultiMode.ini) |❌| clash、singbox等 订阅转换配置文件 | [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=1605s) |
| SUBEMOJI | `false` |❌| 订阅转换是否启用Emoji(默认`true`) | |
| SUBNAME | `edge2` |❌| 订阅名称 | |
| RPROXYIP | `false` |❌| 设为 true 即可强制获取订阅器分配的ProxyIP(需订阅器支持)| [Video](https://www.youtube.com/watch?v=s91zjpw3-P8&t=1816s) |
| URL302 | `https://t.me/CMLiussss` |❌| 主页302跳转(支持多url, url之间使用`,`或`换行`作间隔, 小白别用) |  |
| URL | `https://blog.cmliussss.com` |❌| 主页反代伪装(支持多url, url之间使用`,`或`换行`作间隔, 乱设容易触发反诈) |  |
| CFPORTS | `2053`,`2096`,`8443` |❌| CF账户标准端口列表 |  |
| CF_EMAIL | `admin@google.com` |❌| CF账户的邮箱，用于获取 Workers/Pages 请求数 |  |
| CF_APIKEY | `1234567890abcdef1234567890abcdef` |❌| CF账户的`Global API Key`，用于获取 Workers/Pages 请求数 |  |

> **注意：** 只有 `CF_EMAIL` 和 `CF_APIKEY` 变量同时存在时，订阅时才会返回 CF Workers/Pages 的请求数用量信息。

## ❗ 注意事项

### 开启在线编辑优选列表 [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=630s)
- 绑定**变量名称**为`KV`的**KV命名空间**，即可在无`SUB`的前提下，在配置页实现在线编辑`ADD`与`ADDAPI`优选列表；

### **关于`KEY`与`UUID`：**
- 填入`KEY`变量后，将停用`UUID`变量，请确保**二者选其一使用**！
1. 填写`KEY`后，您的**永久订阅**地址为：`https://[YOUR-URL]/[YOUR-KEY]`；
2. 使用动态`UUID`订阅时：
   - 动态`UUID`需手动在永久订阅配置页内获得；
   - 临时订阅地址为：`https://[YOUR-URL]/[动态UUID]`；
   - 订阅有效时间为：**1个`TIME`周期**；
   - 节点可使用时间：**2个`TIME`周期**，即动态`UUID`失效后，节点仍可使用1个额外周期，但无法继续更新订阅。

### **关于`SOCKS5`与`PROXYIP`：**
- 填入`SOCKS5`后，将停用`PROXYIP`。请确保**二者选其一使用**！

### **关于`SUB`与`ADD*`变量：**
- 填入`SUB`后，将停用由`ADD*`类变量生成的订阅内容。请确保**二者选其一使用**！

### **当`SUB`和`ADD*`均为空时：**
- 脚本将自动生成基于CF随机IP的线路，每次更新订阅时会生成不同的随机IP，确保您的订阅不会失联！


## 🔧 实用技巧
本项目提供灵活的订阅配置方案，支持通过URL参数快速自定义订阅内容。
- 示例订阅地址： `https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10`

1. 更换**订阅生成器**的订阅地址 [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=1019s)

   快速切换订阅生成器至 `VLESS.cmliussss.net`：
   ```url
   https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sub=VLESS.cmliussss.net
   ```

2. 更换**PROXYIP**的订阅地址 [视频教程](https://www.youtube.com/watch?v=tKe9xUuFODA&t=1094s)

   快速更换PROXYIP为 `proxyip.cmliussss.net`：
   ```url
   https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?proxyip=proxyip.cmliussss.net
   ```

3. 更换**SOCKS5**的订阅地址

   快速设置SOCKS5连接为 `user:password@127.0.0.1:1080`：
   ```url
   https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?socks5=user:password@127.0.0.1:1080
   ```

- 通过提交多个参数快速修改的订阅地址

   例如同时修改**订阅生成器**和**PROXYIP**：
   ```url
   https://edge2.pages.dev/90cd4a77-141a-43c9-991b-08263cfe9c10?sub=VLESS.cmliussss.net&proxyip=proxyip.cmliussss.net
   ```

4. 该项目部署的节点可通过节点PATH(路径)的方式，使用指定的`PROXYIP`或`SOCKS5`！！！**

- 指定 `PROXYIP` 案例
   ```url
   /proxyip=proxyip.cmliussss.net
   /?proxyip=proxyip.cmliussss.net
   /proxyip.cmliussss.net (仅限于域名开头为'proxyip.'的域名)
   ```

- 指定 `SOCKS5` 案例
   ```url
   /socks5=user:password@127.0.0.1:1080
   /?socks5=user:password@127.0.0.1:1080
   /socks://dXNlcjpwYXNzd29yZA==@127.0.0.1:1080 (默认激活全局SOCKS5)
   /socks5://user:password@127.0.0.1:1080 (默认激活全局SOCKS5)
   ```

- 指定 `HTTP连接` 案例
   ```url
   /http://user:password@127.0.0.1:8080 (默认激活全局SOCKS5)
   ```

5. **当你的`ADDAPI`可作为`PROXYIP`时，可在`ADDAPI`变量末位添加`?proxyip=true`，即可在生成节点时使用优选IP自身作为`PROXYIP`**
- 指定 `ADDAPI` 作为 `PROXYIP` 案例
   ```url
   https://raw.githubusercontent.com/cmliu/WorkerVless2sub/main/addressesapi.txt?proxyip=true
   ```

## ⭐ Star 星星走起
[![Stargazers over time](https://starchart.cc/cmliu/edge2.svg?variant=adaptive)](https://starchart.cc/cmliu/edge2)

## 💻 已适配客户端
### Windows
   - [v2rayN](https://github.com/2dust/v2rayN)
   - clash.meta（[FlClash](https://github.com/chen08209/FlClash)，[mihomo-party](https://github.com/mihomo-party-org/mihomo-party)，[clash-verge-rev](https://github.com/clash-verge-rev/clash-verge-rev)，[Clash Nyanpasu](https://github.com/keiko233/clash-nyanpasu)）
### IOS
   - Surge，小火箭
   - sing-box（[SFI](https://sing-box.sagernet.org/zh/clients/apple/)）
### 安卓
   - clash.meta（[ClashMetaForAndroid](https://github.com/MetaCubeX/ClashMetaForAndroid)，[FlClash](https://github.com/chen08209/FlClash)）
   - sing-box（[SFA](https://github.com/SagerNet/sing-box)）
### MacOS
   - clash.meta（[FlClash](https://github.com/chen08209/FlClash)，[mihomo-party](https://github.com/mihomo-party-org/mihomo-party)）


# 🙏 特别鸣谢
### 💖 赞助支持 - 提供云服务器维持[订阅转换服务](https://sub.cmliussss.net/)
- [NodeLoc](https://www.nodeloc.com/)
- [Alice](https://url.cmliussss.com/alice)
- [EasyLinks](https://www.vmrack.net?ref_code=5Zk7eNhbgL7)
- [ZMTO(VTEXS)](https://zmto.com/?affid=1532)

### 🛠 开源代码引用
- [zizifn/edge2](https://github.com/zizifn/edge2)
- [3Kmfi6HP/EDtunnel](https://github.com/6Kmfi6HP/EDtunnel)
- [SHIJS1999/cloudflare-worker-vless-ip](https://github.com/SHIJS1999/cloudflare-worker-vless-ip)
- [Stanley-baby](https://github.com/Stanley-baby)
- [ACL4SSR](https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash/config)
- [股神](https://t.me/CF_NAT/38889)
- [Workers/Pages Metrics](https://t.me/zhetengsha/3382)
- [白嫖哥](https://t.me/bestcfipas)
- [Mingyu](https://github.com/ymyuuu/workers-vless)