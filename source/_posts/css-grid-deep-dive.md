---
title: CSS Grid 深入指南：从基础到复杂布局
date: 2026-03-20 14:30:00
tags:
  - CSS
  - Grid
  - 前端
  - 布局
categories:
  - 技术笔记
photos:
  - https://picsum.photos/seed/cssgrid/800/400
---

CSS Grid 是现代 Web 布局的核心工具。本文通过大量实例演示如何用 Grid 实现各种复杂布局。

<!-- more -->

## 基础概念

Grid 布局由**容器**和**项目**组成：

```css
.container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  grid-template-rows: auto 1fr auto;
  gap: 16px;
}
```

### fr 单位

`fr`（fraction）是 Grid 独有的弹性单位，表示可用空间的份数：

```css
/* 三列等宽 */
grid-template-columns: 1fr 1fr 1fr;

/* 侧边栏 + 主内容 */
grid-template-columns: 250px 1fr;

/* 左窄右宽 */
grid-template-columns: 1fr 3fr;
```

## 命名网格线

用命名网格线让布局语义更清晰：

```css
.layout {
  display: grid;
  grid-template-columns:
    [sidebar-start] 250px
    [sidebar-end content-start] 1fr
    [content-end];
  grid-template-rows:
    [header-start] 60px
    [header-end main-start] 1fr
    [main-end footer-start] 80px
    [footer-end];
}

.header {
  grid-column: sidebar-start / content-end;
  grid-row: header-start / header-end;
}
```

## Grid Areas

更直观的区域定义方式：

```css
.layout {
  display: grid;
  grid-template-areas:
    "header  header"
    "sidebar content"
    "footer  footer";
  grid-template-columns: 250px 1fr;
  grid-template-rows: 60px 1fr 80px;
}

.header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
.content { grid-area: content; }
.footer  { grid-area: footer; }
```

## 响应式 Grid

### auto-fill 与 auto-fit

```css
/* 自动填充，每列最少 250px */
grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));

/* auto-fit 会拉伸现有项填满空间 */
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
```

### 媒体查询配合

```css
.gallery {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 640px) {
  .gallery {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .gallery {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

## 对齐控制

Grid 提供了完整的对齐控制：

```css
.container {
  /* 水平方向对齐所有项目 */
  justify-items: center;

  /* 垂直方向对齐所有项目 */
  align-items: center;

  /* 水平方向对齐整个网格 */
  justify-content: center;

  /* 垂直方向对齐整个网格 */
  align-content: center;
}

/* 单个项目覆盖 */
.item {
  justify-self: end;
  align-self: start;
}
```

## 实战：瀑布流布局

利用 `grid-row: span` 实现简单的瀑布流效果：

```css
.masonry {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 20px;
  gap: 16px;
}

.masonry-item.tall {
  grid-row: span 3;
}

.masonry-item.medium {
  grid-row: span 2;
}
```

## Grid vs Flexbox

两者不是替代关系，而是互补：

- **Grid**：二维布局（行+列同时控制）
- **Flexbox**：一维布局（行或列）

经验法则：**组件内部用 Flexbox，页面级布局用 Grid**。

> Grid 和 Flexbox 配合使用，才是现代 CSS 布局的完整解决方案。
