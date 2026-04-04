---
title: JavaScript 异步编程模式详解
date: 2026-03-15 10:00:00
tags:
  - JavaScript
  - Async
  - 前端
categories:
  - 技术笔记
---

从回调地狱到 async/await，JavaScript 异步编程走过了漫长的演化之路。本文系统梳理各种异步模式的优劣与适用场景。

<!-- more -->

## 回调函数 (Callbacks)

最原始的异步模式。Node.js 早期 API 几乎全部基于回调：

```javascript
fs.readFile('/path/to/file', 'utf8', (err, data) => {
  if (err) {
    console.error('读取失败:', err);
    return;
  }
  console.log(data);
});
```

### 回调地狱

当多个异步操作需要串行执行时，嵌套层级迅速膨胀：

```javascript
getUser(userId, (err, user) => {
  getOrders(user.id, (err, orders) => {
    getOrderDetails(orders[0].id, (err, details) => {
      // 三层嵌套，代码已经很难维护
      renderPage(details);
    });
  });
});
```

## Promise

ES6 引入 Promise，用链式调用替代嵌套：

```javascript
getUser(userId)
  .then(user => getOrders(user.id))
  .then(orders => getOrderDetails(orders[0].id))
  .then(details => renderPage(details))
  .catch(err => console.error(err));
```

### Promise 组合

`Promise.all` 并行执行多个异步任务：

```javascript
const [users, posts, comments] = await Promise.all([
  fetchUsers(),
  fetchPosts(),
  fetchComments()
]);
```

`Promise.race` 取最快完成的结果：

```javascript
const result = await Promise.race([
  fetch('/api/data'),
  timeout(5000)
]);
```

## Async/Await

ES2017 的语法糖，让异步代码看起来像同步：

```javascript
async function loadPage(userId) {
  try {
    const user = await getUser(userId);
    const orders = await getOrders(user.id);
    const details = await getOrderDetails(orders[0].id);
    return renderPage(details);
  } catch (err) {
    console.error('加载失败:', err);
  }
}
```

### 常见陷阱

**串行 vs 并行：** 不要在循环中无脑 await：

```javascript
// ❌ 串行执行，很慢
for (const url of urls) {
  const data = await fetch(url);
  results.push(data);
}

// ✅ 并行执行
const results = await Promise.all(urls.map(url => fetch(url)));
```

## Generator + Co

在 async/await 之前，社区用 Generator 模拟异步控制流：

```javascript
const co = require('co');

co(function* () {
  const user = yield getUser(userId);
  const orders = yield getOrders(user.id);
  return orders;
});
```

这种模式现在已经被 async/await 完全取代，但理解它有助于理解 async/await 的本质。

## 响应式编程 (RxJS)

处理复杂的事件流和数据流：

```javascript
import { fromEvent, debounceTime, switchMap } from 'rxjs';

fromEvent(searchInput, 'input').pipe(
  debounceTime(300),
  switchMap(e => fetch(`/api/search?q=${e.target.value}`))
).subscribe(results => renderResults(results));
```

## 总结

| 模式 | 适用场景 | 复杂度 |
|------|---------|--------|
| Callback | 简单的单次异步 | 低 |
| Promise | 链式异步操作 | 中 |
| Async/Await | 大多数场景 | 低 |
| RxJS | 复杂事件流 | 高 |

现代 JavaScript 开发中，**async/await 是默认选择**，仅在需要处理复杂数据流时考虑 RxJS。
