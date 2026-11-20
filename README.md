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

```bash
hugo new content posts/my-note.md
```

然后编辑 `content/posts/my-note.md`，把开头的 `draft` 改成 `false`。也可以直接在 `content/posts/` 下新建 Markdown 文件。提交并推送到 `main` 后，GitHub Actions 会自动构建发布。

## 部署

工作流在 `.github/workflows/gh-pages.yml`。推送到 `main` 后，Actions 用 Hugo Extended 执行 `hugo --minify`，并把 `public/` 发布到 `gh-pages` 分支。

GitHub Pages 的构建来源需要设为 **`gh-pages` 分支**：

**Settings → Pages → Build and deployment → Source** 选择 **Deploy from a branch**，Branch 选择 **`gh-pages`**，文件夹选择 **`/ (root)`**。

`gh-pages` 分支要等第一次工作流成功之后才会出现。如果第一次部署失败，先确认 Pages 来源是 `gh-pages`，再重新运行 Actions。
