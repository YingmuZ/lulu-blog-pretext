---
title: 设计系统中的排版规范：从字体选择到垂直韵律
date: 2026-03-28 16:00:00
tags:
  - 设计系统
  - 排版
  - CSS
categories:
  - 设计
---

好的排版是阅读体验的基石。本文探讨如何在设计系统中建立一套可维护、可扩展的排版规范。

<!-- more -->

## 字体选择

### 正文字体

正文字体是设计系统中最重要的选择。关键指标：

- **x-height**：字母 x 的高度，直接影响可读性
- **字重覆盖**：至少需要 Regular (400) 和 Bold (700)
- **多语言支持**：CJK（中日韩）字符的覆盖情况
- **等宽数字**：表格中数字是否对齐（tabular figures）

```css
/* 中英混排方案 */
font-family:
  "Noto Serif JP",     /* 日文衬线 */
  "Noto Serif SC",     /* 简体中文衬线 */
  Georgia,             /* 西文衬线后备 */
  serif;
```

### 标题字体

标题字体可以比正文更有个性。推荐与正文字体形成对比：

- 正文衬线 → 标题无衬线（或反过来）
- 正文常规字重 → 标题用更粗或更细的变体

### 代码字体

等宽字体的选择要注意：

- `0` 和 `O` 的区分
- `1`、`l`、`I` 的区分
- 连字（ligatures）的支持程度

```css
font-family: "JetBrains Mono", "Fira Code", monospace;
```

## 字号阶梯 (Type Scale)

用数学比率建立字号阶梯，常用比率：

| 名称 | 比率 | 适用场景 |
|------|------|---------|
| Minor Second | 1.067 | 紧凑界面 |
| Major Second | 1.125 | 正文为主 |
| Minor Third | 1.2 | 通用 |
| Major Third | 1.25 | 标题突出 |
| Perfect Fourth | 1.333 | 杂志风格 |

以 Major Second (1.125) 为例，基础字号 16px：

```
xs:   12.64px  →  0.79rem
sm:   14.22px  →  0.889rem
base: 16px     →  1rem
lg:   18px     →  1.125rem
xl:   20.25px  →  1.266rem
2xl:  22.78px  →  1.424rem
3xl:  25.63px  →  1.602rem
4xl:  28.83px  →  1.802rem
```

## 行高与段间距

### 行高 (Line Height)

行高影响阅读节奏：

- **正文**：1.5 ~ 1.8（中文偏大，1.7 ~ 1.8）
- **标题**：1.1 ~ 1.3
- **代码**：1.4 ~ 1.6

```css
body { line-height: 1.8; }      /* 中文友好 */
h1, h2, h3 { line-height: 1.2; }
pre, code { line-height: 1.5; }
```

### 段间距

段间距通常等于一个行高，或者正文字号的 1.5 倍：

```css
p + p { margin-top: 1.5em; }
```

## 垂直韵律 (Vertical Rhythm)

所有元素的间距都是基础行高的整数倍，形成视觉韵律：

```css
:root {
  --baseline: 1.5rem;  /* 基础行高 = 24px */
}

p       { margin-bottom: var(--baseline); }
h1      { margin-top: calc(var(--baseline) * 3);
          margin-bottom: var(--baseline); }
h2      { margin-top: calc(var(--baseline) * 2);
          margin-bottom: var(--baseline); }
img     { margin: var(--baseline) 0; }
```

## 最大行宽

**45 ~ 75 个字符**是公认的最佳阅读行宽。中文大约 **25 ~ 40 个字**。

```css
.prose {
  max-width: 65ch;  /* 约 720px @16px */
}
```

## 响应式排版

### clamp() 实现流式字号

```css
h1 {
  /* 最小 24px，最大 48px，中间按视窗宽度缩放 */
  font-size: clamp(1.5rem, 4vw, 3rem);
}
```

### 移动端调整

```css
/* 移动端稍小的基础字号 */
html { font-size: 16px; }

@media (min-width: 768px) {
  html { font-size: 18px; }
}
```

## 实际案例：本主题的排版

hexo-theme-pretext 的排版设计遵循以上原则：

- 正文：Noto Serif JP + SC，18px/1.8
- 标题：Shippori Mincho，紧凑行高 1.2
- 代码：JetBrains Mono，15px/1.5
- 最大内容宽度：720px
- 大量留白，段间距 1.5em

> 排版不是装饰，而是信息架构的基础设施。好的排版让读者忘记排版的存在。
