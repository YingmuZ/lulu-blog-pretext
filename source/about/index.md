---
title: About
date: 2026-04-01
---

## 关于本站

这是 **hexo-theme-pretext** 主题的展示站点——一款极简风格的 Hexo 博客主题，集成 [@chenglou/pretext](https://github.com/chenglou/pretext) ASCII 文字动态排版效果。

## 主题特色

- **极简设计** — 大量留白，克制的装饰，让内容本身成为焦点
- **亮/暗模式** — 自动检测系统偏好 + 手动切换，支持 localStorage 持久化
- **ASCII 动画** — 基于 pretext 的文字排版引擎，实现首页兔子动画、文章装饰、404 彩蛋等交互效果
- **密码保护文章** — 集成 hexo-blog-encrypt，加密文章的 UI 自动适配主题风格
- **评论系统** — 支持 Giscus、Disqus、Waline 三种方案，按需启用

## 技术实现

- 静态站点生成：[Hexo](https://hexo.io/)
- 样式方案：[Tailwind CSS](https://tailwindcss.com/)，class 策略的暗色模式
- 文字排版引擎：[@chenglou/pretext](https://github.com/chenglou/pretext)，通过 CDN 按需加载，无 JavaScript 时优雅降级
- 模板引擎：EJS，使用 fragment_cache 优化渲染性能
- 部署：GitHub Actions + GitHub Pages

## 安全相关

- 文章密码保护基于 hexo-blog-encrypt 的前端加密，适用于轻度隐私场景，不应用于存储敏感信息
- 评论系统（Giscus）基于 GitHub Discussions，由 GitHub 账号体系保障身份验证
- 全站纯静态输出，无服务端逻辑，无数据库，攻击面极小

## ASCII Bunny Art 致谢

首页的四只兔子 ASCII 艺术作品来自 [asciiart.eu](https://www.asciiart.eu/animals/rabbits)，感谢以下创作者：

- Blazej Kozlowski
- Rowan Crawford
- Scott C. Sullivan
- Unknown

## 联系

- GitHub: [hexo-theme-pretext-with-ascii-bunny](https://github.com/YingmuZ/hexo-theme-pretext-with-ascii-bunny)
