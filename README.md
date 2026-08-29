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
| `index.html` | `/`（主域名首页） | ✅ 买家（宣传落地页：Ignition v2 卖点 + 下载 + 购买 + FAQ） | ✅ 2026-08-29 更新到 v1.2.2（Signal Journal / 会话感知 / 板块地图卖点） |
| `download.html` | `/download.html` | 买家（下载/激活说明） | ✅ 已更新：v1.2.2 下载链接（134MB）+ FAQ |
| `seller.html` | `/seller.html` | 卖家（激活码生成器，原 index.html 备份） | ✅ 已创建（备份原生成器） |
| `nacl.min.js` | `/nacl.min.js` | 生成器依赖 | — |

⚠️ 注意：seller.html 是卖家工具，**不要把链接转发给买家**；私钥只在本机浏览器粘贴（页面本身无私钥，安全）。

## 部署方式（重要）

- **没有 git 仓库**（`not a git repository`）——Vercel 上是 CLI 手动项目，非 Git 集成
- 部署命令：`cd vercel-license-generator && vercel --prod --yes`
- 每次 CLU 部署都会生成新的 Deployment URL，但会自动 alias 到正式域名
- 最新部署：2026-08-29 12:40（v1.2.2 发布：落地页 + 下载页同步更新）

## 产品版本状态（2026-08-29）

- 桌面版 **v1.2.3**：安装包 `installer/StockScreenerPro_Setup.exe`（134,434,037 bytes，2026-08-29 17:58 UTC 覆盖）
- GitHub Release：`naiping87/stock-screener` tag **v1.2.3**（资产已用 --clobber 覆盖为最新含图表修复版；v1.2.0/v1.2.1 保留作回滚）
- 下载链接（网页已更新）：`https://github.com/naiping87/stock-screener/releases/download/v1.2.2/StockScreenerPro_Setup.exe`（HTTP 200 已验证）
- v1.2.2 新增（14 提交 + 本次）：Ignition v2（Bursa 板块地图 + 会话感知 CLV）、Signal Journal（Edge Report 标签页）、KDJ 26/5、图表十字光标 + D/W 快捷键、列提示 tooltip、低价股精度、Phase-1 回测工具；本次再加：K 线红绿高对比（#22C55E/#EF4444）、动态宽度、周线/日线 OHLC 数据修复、快速显示（不等 meta 即出结果）
- v1.2.1 曾新增：会话感知、Fusion 修复。累计：Ignition、penny 防护、语言互斥、i18n 三语、性能优化、图表修复、分步进度条

## 待办（按优先级）

1. ✅ ~~移走生成器~~：index.html 已重写为宣传落地页；原生成器备份到 seller.html
2. ✅ ~~建 git 仓库~~：已推 `naiping87/vercel-license-generator`（c6aeeb4 之后每次改动 commit 再部署）
3. ✅ ~~宣传页截图~~：已有 3 张（ignition_tab/chart_pivot/app_main）；🟡 待做：回测对比图（Top20 vs Random vs Market）+ Edge Report 截图
4. ✅ ~~README（主项目）补 Ignition 说明~~：桌面项目已更新。🟡 待办：攒 3-5 条真实买家评价替换占位评论（旧站已下线）

## 关键安全事实

- 私钥**只在本机浏览器粘贴**（index.html 内注释明确），页面文件本身不含私钥 → 页面可公开托管；但生成器页面不该让买家看到（易被误解/社工）
- `seller_tools/*.pem` 在 stock-screener 项目内、已 gitignore（`.pem` 全局排除）
- 激活验证在桌面端本地完成（Ed25519 签名校验，无服务器）