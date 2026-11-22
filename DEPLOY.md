# 部署指南（GitHub Pages）

`site/` 是纯静态站点（HTML + CSS + KaTeX CDN），无需任何构建工具，推到 GitHub 即可上线。

## 方案 A：挂在你已有的个人主页仓库（username.github.io）

如果你的 GitHub Pages 主页仓库是 `<用户名>/<用户名>.github.io`：

```bash
# 把 site/ 里的所有文件拷入该仓库根目录（或你想要的子目录，如 quant/）
cp -R site/* /path/to/username.github.io/
cd /path/to/username.github.io
git add -A && git commit -m "add quant handbook" && git push
```

访问：`https://<用户名>.github.io/`（或子目录路径）
> 注意：如果主页仓库已有其他内容，建议放子目录（如 `quant/`），站点全部使用相对路径，子目录部署无需任何修改。

## 方案 B：新建独立仓库（推荐，干净）

```bash
cd site
git init -b main
git add -A
git commit -m "Quant 面试复习手册 v1"
git remote add origin https://github.com/<你的用户名>/quant-handbook.git
git push -u origin main
```

然后在 GitHub 网页上：**仓库 Settings → Pages → Branch 选 main / 目录选 / (root) → Save**。
访问：`https://<你的用户名>.github.io/quant-handbook/`

## 自定义域名（可选，如 hwcoder.top 这种）

1. 仓库根目录加一个 `CNAME` 文件，内容写你的域名（如 `quant.yourdomain.top`）
2. 域名 DNS 加一条 CNAME 记录指向 `<用户名>.github.io`
3. Settings → Pages → Custom domain 填入并勾选 Enforce HTTPS

## 日常更新流程

```bash
# 1. 编辑 wechat/*.md（内容源文件）
# 2. 重新生成站点
python3 build.py
# 3. 提交推送
cd site && git add -A && git commit -m "update" && git push
```

## 公式与资源说明

- 数学公式：KaTeX（jsdelivr CDN，浏览器端渲染）——国内访问慢可把 `*.html` 里的
  `cdn.jsdelivr.net` 换成 `cdn.staticfile.net` 或自托管 katex dist
- 代码高亮：highlight.js（同 CDN）
- 无需 Node/Hexo 构建，克隆即用
