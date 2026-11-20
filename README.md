# 0xSY

个人站点，使用 [Hugo](https://gohugo.io/) 和 [Blowfish](https://blowfish.page/) 主题。线上地址是 <https://0xsy-sec.github.io/>。

## 本地预览

需要 **Hugo Extended**。Blowfish 当前要求 **0.166.0 到 0.169.0**（本仓库用 0.169.0 构建）。克隆时带上主题子模块：

```bash
git clone --recurse-submodules https://github.com/0xSY-SEC/0xSY-SEC.github.io.git
cd 0xSY-SEC.github.io
hugo server
```

浏览器打开 <http://localhost:1313/>。如果仓库已经克隆过，但 `themes/blowfish` 是空的，先执行：

```bash
git submodule update --init --recursive
```

## 写一篇文章

文章放进五个栏目之一，不要直接放在 `content/posts/` 根目录：

| 栏目 | 目录 |
| --- | --- |
| 漏洞研究 | `content/posts/vuln-research/` |
| 移动安全 | `content/posts/mobile-security/` |
| Web 安全 | `content/posts/web-security/` |
| 工具与开发 | `content/posts/tooling/` |
| 随笔 | `content/posts/notes/` |

例如写一篇 Web 安全笔记：

```bash
hugo new content posts/web-security/my-note.md
```

打开生成的文件，把 `draft` 改成 `false`，并补上摘要。开头可以写成：

```yaml
---
title: "文章标题"
date: 2026-11-20
draft: false
description: "一句话说明这篇文章讲什么"
summary: "列表和首页上显示的摘要"
tags:
  - Web
---
```

正文用 Markdown 写在 front matter 下面。本地预览：

```bash
hugo server
```

浏览器打开 <http://localhost:1313/>，确认栏目页和文章都正常。提交并推送到 `main` 后，GitHub Actions 会执行 `hugo --minify` 并发布。

## 部署

工作流在 `.github/workflows/gh-pages.yml`。推送到 `main` 后，Actions 用 Hugo Extended 执行 `hugo --minify`，并把 `public/` 发布到 `gh-pages` 分支。

GitHub Pages 的构建来源需要设为 **`gh-pages` 分支**。这个仓库目前的 Pages 来源是 **`main`**，那样会直接发布源码，而不是 Hugo 生成的站点。合并后请改成：

**Settings → Pages → Build and deployment → Source** 选择 **Deploy from a branch**，Branch 选择 **`gh-pages`**，文件夹选择 **`/ (root)`**。

`gh-pages` 分支要等第一次工作流成功之后才会出现。如果第一次部署失败，先确认 Pages 来源是 `gh-pages`，再重新运行 Actions。
