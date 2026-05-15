---
title: "安全加固日：许可证、环境变量与Git历史清理"
date: 2026-05-16
category: 安全 + 运维
slug: security-and-polish
---

## 今日概览

今天是项目上线以来第一次全面的安全审查和加固。核心目标是把之前不小心暴露在公开仓库中的敏感信息彻底清除，同时建立长期的安全防护机制。

- **地点**：家中 + 手机端
- **心态**：沉稳排雷，一劳永逸

## 关键事件

### 🔒 开源许可证部署
- 为公开仓库 `useaitools-me` 添加 **AGPL-3.0** 许可证
- 核心条款：任何人如果用你的代码搭建网站并对外服务，必须开源其修改后的全部代码

### 🔐 联盟链接迁移
- 将 `data/tools.json` 中硬编码的 Rytr 联盟链接迁移到 **Vercel 环境变量**
- 环境变量命名规则：`AFFILIATE_{工具名大写}`（如 `AFFILIATE_RYTR`）
- 代码修改涉及 5 个文件，实现环境变量优先读取，JSON 回退的兼容逻辑
- Vercel 环境变量已配置：`AFFILIATE_RYTR = https://rytr.me/?via=xiaomo`

### 🧹 Git 历史深度清理
- 使用 `git filter-repo` 从全部提交历史中彻底删除 `data/tools.json` 的旧版本
- 强制推送到 GitHub，重写远程仓库历史
- 公开仓库中不再存在任何联盟链接的历史痕迹

### 🛡️ 安全审查
- 对公开仓库进行全面搜索：`ghp_`、`sk-`、`api_key`、`token`、`secret` 等关键词
- 确认无 API Key、Token 或个人信息泄露
- 确认私有仓库 `devlog-private` 中敏感信息存储安全
- 制定了定期安全审查清单

## 遇到的坑与解决方案

### Git filter-repo 安装与使用
- **问题**：网吧环境未预装 `git-filter-repo`
- **解决**：通过 `pip install git-filter-repo` 安装
- **经验**：`--path` + `--invert-paths` 组合可以精确删除指定文件的历史

### Personal Access Token 丢失
- **问题**：强制推送需要 Token，但旧 Token 的值已不可见
- **解决**：重新生成新的 Token（`trae-push-now`），并记录保存
- **教训**：Token 生成时立即复制保存，GitHub 只显示一次

## 今日金句

> "开源不是非黑即白的二选一，而是一道可以精细控制的灰度开关。AGPL-3.0 保护你的代码不被闭源商用，环境变量藏好你的核心机密，公开日志分享你的建站故事——三位一体，才是独立开发者最安全的 Build in Public。"

## 明日计划

1. 关注 Jasper / Copy.ai 联盟申请的邮件回复
2. 继续在 Twitter 发内容，Reddit 养号
3. 扩展 Video、Audio 等分类的效果展示
4. 写单工具深度评测文章，丰富博客内容
5. 研究如何在 Vercel 上实现私有仓库 Submodule 引入核心数据

---

*本日志由 xiaomo 记录*
