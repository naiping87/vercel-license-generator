# Stock Screener Pro — Web 项目状态记录

> 这份文件是「项目记忆」：记录已经确认的事实与待办，任何会话打开即得完整背景。
> 每次改动网页/部署后，请同步更新本文件。

## 项目是什么

`vercel-license-generator` = Stock Screener Pro 的 **Web 静态站**（Vercel 托管，纯静态 HTML，无后端）。

Vercel 项目：`naiping87s-projects/vercel-license-generator`
正式域名：`https://vercel-license-generator-zeta.vercel.app`

## 页面结构（当前状态）

| 文件 | 线上路径 | 面向谁 | 状态 |
|---|---|---|---|
| `index.html` | `/`（主域名首页） | ✅ 买家（宣传落地页：Ignition 卖点 + 下载 + 购买 + FAQ） | ✅ 2026-08-26 重写为新版 |
| `download.html` | `/download.html` | 买家（下载/激活说明） | ✅ 已更新：Ignition 卖点 + v1.2.0 下载链接 + FAQ |
| `seller.html` | `/seller.html` | 卖家（激活码生成器，原 index.html 备份） | ✅ 已创建（备份原生成器） |
| `nacl.min.js` | `/nacl.min.js` | 生成器依赖 | — |

⚠️ 注意：seller.html 是卖家工具，**不要把链接转发给买家**；私钥只在本机浏览器粘贴（页面本身无私钥，安全）。

## 部署方式（重要）

- **没有 git 仓库**（`not a git repository`）——Vercel 上是 CLI 手动项目，非 Git 集成
- 部署命令：`cd vercel-license-generator && vercel --prod --yes`
- 每次 CLU 部署都会生成新的 Deployment URL，但会自动 alias 到正式域名
- 最新部署：2026-08-26 01:42（download.html 更新那次）

## 产品版本状态（2026-08-26）

- 桌面版 v1.2.0：`dist/StockScreenerPro.exe`（02:17:40）+ 安装包 `installer/StockScreenerPro_Setup.exe`（02:17:59，117,709,254 bytes）
- GitHub Release：`naiping87/stock-screener` tag `v1.2.0`（资产已用 --clobber 覆盖为最新）
- 下载链接：`https://github.com/naiping87/stock-screener/releases/download/v1.2.0/StockScreenerPro_Setup.exe`（HTTP 200）
- 版本内容：Ignition 起爆点检测器（RS 排名/板块强度/Setup/Breakout 子分/CLV 收盘强势/measured-move R:R）、penny 股防护、语言互斥、i18n 三语、性能优化（golden 验证）、分步进度条

## 待办（按优先级）

1. ✅ ~~移走生成器~~：index.html 已重写为宣传落地页；原生成器备份到 seller.html
2. 🔴 **建 git 仓库**：`git init` + 推 GitHub（如 `naiping87/vercel-license-generator`），解决「没有版本记录」，之后每次改动先 commit 再部署
3. 🟡 宣传页做「截图文案占位」：回测对比图（Top20 vs Random vs Market）可做宣传素材
4. 🟡 README（主项目）补 Ignition 说明（桌面项目已更新部分，Web 侧未做）

## 关键安全事实

- 私钥**只在本机浏览器粘贴**（index.html 内注释明确），页面文件本身不含私钥 → 页面可公开托管；但生成器页面不该让买家看到（易被误解/社工）
- `seller_tools/*.pem` 在 stock-screener 项目内、已 gitignore（`.pem` 全局排除）
- 激活验证在桌面端本地完成（Ed25519 签名校验，无服务器）
