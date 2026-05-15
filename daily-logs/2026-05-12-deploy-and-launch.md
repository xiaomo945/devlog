---
title: "部署日：域名解析、Vercel上线、Google收录"
date: 2026-05-12
category: 建站
slug: deploy-and-launch
---

## 今日概览

第二天。核心任务是把昨天写好的代码推上线，配置域名解析，让 `useaitools.me` 真正被全球访问。这天的关键词是“忍耐”——在DNS配置和Git推送中反复试错。

- **地点**：中国保定某网吧
- **心态**：在挫折中坚持，在坚持中突破

## 关键事件

- ✅ **Vercel 部署成功**：连接 GitHub 仓库 `xiaomo945/useaitools-me`，自动构建并部署 Next.js 项目。
- ✅ **Cloudflare DNS 配置**：在阿里云修改 NS 服务器指向 Cloudflare，配置 A 记录和 CNAME 记录。
- ✅ **自定义域名绑定**：`useaitools.me` 成功指向 Vercel，SSL 证书自动签发。
- ✅ **Google Search Console 验证**：通过 TXT 记录完成域名所有权验证。
- ✅ **Sitemap 提交成功**：解决 404 问题后，Google 成功读取 sitemap，首页被收录。

## 技术挑战

### DNS 配置的反复折腾
- 阿里云 NS 服务器修改：将 `dnsXX.hichina.com` 替换为 Cloudflare 的 `anastasia.ns.cloudflare.com` 和 `harley.ns.cloudflare.com`。
- A 记录指向 Vercel IP `216.198.79.1`，CNAME 记录指向 `cname.vercel-dns.com`。
- Vercel 验证一直显示 "Invalid Configuration"，排查后发现是 DNS 服务器还没完全切换到 Cloudflare。

### Sitemap 404 问题的终极修复
- 使用 `next-sitemap` 生成静态 sitemap，但部署到 Vercel 后始终 404。
- 尝试了动态 sitemap (`app/sitemap.ts`)，同样不生效。
- 最终解决方案：创建 `vercel.json` 重写规则 + `app/api/sitemap/route.ts` API 路由，手动返回 XML 内容。
- 提交到 Google Search Console，状态变为“成功”。

## 行动日志

| 时间 | 操作 | 成果 |
|:---|:---|:---|
| 上午 | Vercel 导入 GitHub 仓库 | 项目自动构建并部署 |
| 上午 | 绑定自定义域名 | SSL 证书自动签发 |
| 中午 | Cloudflare DNS 配置 | NS 修改 + A/CNAME 记录添加 |
| 下午 | Google Search Console 验证 | TXT 记录验证通过 |
| 晚上 | Sitemap 提交 | 解决 404 问题，成功提交 |

## 金句时刻

> "DNS 生效需要时间，不要反复改，改完等几分钟再验证。"
>
> "Vercel 的 Invalid Configuration 通常不是代码问题，是 DNS 还没生效。"

## 明日计划

1. 申请 PartnerStack 联盟营销账号
2. 注册 AppSumo Affiliate
3. 探索 ElevenLabs 直接联盟申请
4. 继续优化网站视觉设计

---

*本日志由 xiaomo 记录于中国保定某网吧*
