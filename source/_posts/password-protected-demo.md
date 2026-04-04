---
title: 密码保护测试 / Password Protection Demo
date: 2026-04-04 00:30:00
tags:
  - 测试
  - 密码保护
  - demo
categories:
  - 测试
password: test123
abstract: 这是一篇受密码保护的文章，请输入密码访问。This post is password protected.
message: 请输入密码test123
---

恭喜你成功解锁了这篇文章！🎉

Congratulations, you've unlocked this post!

## 测试内容 / Test Content

这篇文章用于验证 `hexo-blog-encrypt` 插件与 hexo-theme-pretext 主题的样式兼容性。

This post verifies the style compatibility between `hexo-blog-encrypt` and hexo-theme-pretext.

### 检查清单 / Checklist

- [ ] 密码输入框样式与主题一致
- [ ] 亮色/暗色模式下输入框正确显示
- [ ] 解锁按钮 hover 效果正常
- [ ] 解锁后文章内容正常渲染
- [ ] 摘要文本在文章列表中正确显示

### 代码块测试

```javascript
function secretFunction() {
  console.log("You found the secret!");
  return 42;
}
```

### 表格测试

| 项目 | 状态 |
|------|------|
| 密码输入 UI | 待验证 |
| 暗色模式适配 | 待验证 |
| 解锁后渲染 | 待验证 |

> 测试密码为 `test123`，仅供开发验证使用。
> Test password is `test123`, for development testing only.
