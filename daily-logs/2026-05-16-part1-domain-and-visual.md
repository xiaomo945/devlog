---
title: "第六天公开日志（上）：收尾日：域名跳转与视觉升级 - 2026-05-16"
date: 2026-05-16
category: 建站 + 安全
slug: domain-fix-and-visual-upgrade
---

## 今日概览

第五天结束后的收尾日。把之前遗留的三个域名跳转全部配置成功，修复了 Vercel 构建错误，给分类页和工具详情页做了视觉升级，并完成了第一次安全审查。品牌矩阵彻底锁死，所有入口统一指向主站。

- **地点**：中国保定某网吧 + 手机端
- **心态**：耐心排雷，稳步推进

## 关键事件

### 🌐 域名跳转收尾（苦战）
- 对 `cafeaitools.com`、`useaitools.net`、`useaitools.cn` 使用 **Page Rules** 创建 301 跳转，最终全部生效。
- 此前尝试 Bulk Redirects 和 Redirect Rules 均因 Cloudflare Free 计划限制和格式问题失败，最终用 Page Rules 这条“笨办法”稳稳解决。
- **经验**：Bulk Redirects 的 CSV 格式容易因换行异常导致部分域名无效；单条 Redirect Rule 的开关有时无法启用（UI 问题），而 Page Rules 虽只有 3 条免费规则，但对核心域名跳转最可靠。

### 🎨 视觉与体验升级
- 修复分类标签页 Hero 区域的遮挡问题，背景跟随深色/浅色模式。
- 重新设计分类页 Hero 区域，加入微网格纹理、毛玻璃描述气泡、类别专属色光晕和逐层入场动画。
- 为 Image 分类的工具添加了 `examples` 字段，工具详情页新增“🎨 Examples & Prompts”区块，展示 AI 生图示例和提示词。
- 修复网站 Footer 中 Dev.to 链接的错误（从 `jiongxiaomo` 改为正确用户名 `xiaomo`）。

### 🔧 构建错误修复
- 修复 `CategoryHero` 组件的 TypeScript 类型错误（放宽 prop 类型为 `string`），Vercel 构建恢复正常。

### 🔒 安全审查
- 对 GitHub 公开仓库 `xiaomo945/useaitools-me` 进行安全检查，确认无 API Key、Token 或个人信息泄露。
- 确认私有仓库 `devlog-private` 中的账号信息和密码提示存储安全。
- 制定了安全加固清单，包括定期检查 Git 历史、轮换 Token、确认无 `.env` 文件被提交。

### 📚 记忆库维护
- 将前五天的工作日志全部整理并推送至公开仓库 `devlog`。
- 在私有仓库 `devlog-private` 中创建了账号信息、密码提示、变现进展三个文件。

## 遇到的坑与解决方案

### Cloudflare 跳转配置的漫长排雷
- **问题**：Bulk Redirects 列表中的 CSV 格式因意外换行导致 `cafeaitools.com` 及之后的域名不生效。
- **尝试**：手动编辑 CSV、重新上传、创建单条 Redirect Rule、启用开关（灰色不可点）。
- **最终解决**：放弃 Bulk Redirects 和 Redirect Rules，改用 **Page Rules** 的 Forwarding URL 功能，逐条创建，全部成功。
- **教训**：当自动化工具出现无法解释的 UI 故障时，“手动逐个配”是独立开发者最可靠的底线。

## 今日金句

> “早知道就用这个笨办法了。两天折腾这么点内容……不，这两天不是在折腾，是在排雷。以后任何域名跳转，你闭着眼都能配。”

## 明日计划

1. 关注 Jasper / Copy.ai 联盟申请的邮件回复。
2. 继续在 Twitter 发内容，Reddit 养号。
3. 扩展 Video、Audio 等分类的效果展示。
4. 写单工具深度评测文章，丰富博客内容。

---

*本日志由 xiaomo 记录于中国保定*
