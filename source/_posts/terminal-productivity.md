---
title: 终端效率提升：我的工具链分享
date: 2026-04-01 11:00:00
tags:
  - 工具
  - 终端
  - 效率
categories:
  - 工具箱
---

作为一个每天在终端里花费大量时间的开发者，这些工具显著提升了我的工作效率。

<!-- more -->

## Shell: Zsh + Oh My Zsh

基础配置：

```bash
# .zshrc
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="robbyrussell"
plugins=(git z fzf docker kubectl)
source $ZSH/oh-my-zsh.sh
```

### 常用别名

```bash
alias gs="git status"
alias gc="git commit"
alias gp="git push"
alias gd="git diff"
alias ll="ls -la"
alias ..="cd .."
alias ...="cd ../.."
```

## 搜索: fzf + ripgrep

### fzf 模糊搜索

```bash
# 安装
brew install fzf

# 文件搜索
vim $(fzf)

# 历史命令搜索 (Ctrl+R)
# Git 分支切换
git checkout $(git branch | fzf)
```

### ripgrep 代码搜索

```bash
# 比 grep 快 10 倍以上
rg "function.*async" --type js
rg "TODO|FIXME" -g "!node_modules"
```

## 文件管理: eza + bat

```bash
# eza: ls 的现代替代
eza -la --git --icons

# bat: cat 的替代，带语法高亮
bat src/main.rs
```

## 终端复用: tmux

```bash
# 基础快捷键 (prefix = Ctrl+b)
# 新建窗口: prefix + c
# 切换窗口: prefix + 数字
# 水平分割: prefix + "
# 垂直分割: prefix + %
# 切换面板: prefix + 方向键
```

我的 tmux 配置片段：

```bash
# 改 prefix 为 Ctrl+a
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# 鼠标支持
set -g mouse on

# 256色
set -g default-terminal "screen-256color"

# 面板边框颜色
set -g pane-border-style fg=colour240
set -g pane-active-border-style fg=colour166
```

## JSON 处理: jq

```bash
# 格式化
cat data.json | jq '.'

# 提取字段
curl -s api.example.com/users | jq '.[].name'

# 过滤
jq '.[] | select(.age > 25)' users.json

# 转换
jq '{name: .first_name, email: .contact.email}' user.json
```

## HTTP 调试: httpie

```bash
# 比 curl 更友好的语法
http GET api.example.com/users
http POST api.example.com/users name=Alice age:=25
http PUT api.example.com/users/1 name=Bob
```

## 进程监控: btop

比 top/htop 更现代的系统监控工具，支持：
- CPU/内存/磁盘/网络实时图表
- 进程树视图
- 鼠标操作

## 我的效率原则

1. **能自动化的就自动化** — 重复三次以上就写脚本
2. **键盘优先** — 减少鼠标操作
3. **组合简单工具** — Unix 哲学：每个工具做好一件事
4. **定期清理** — 删除不再使用的别名和脚本

> 工具只是手段，解决问题才是目的。不要陷入无止境的配置优化中。
