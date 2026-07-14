# S1amesecat.github.io

使用 Material for MkDocs 构建的个人知识库：

- 网站：<https://s1amesecat.github.io/>
- 仓库：<https://github.com/S1amesecat/S1amesecat.github.io>
- 文章源文件：`docs/`
- 站点配置与导航：`mkdocs.yml`
- 自动部署：`.github/workflows/deploy.yml`

## 项目目录

```text
mkdocs/
├─ .github/workflows/deploy.yml   # GitHub Pages 自动部署
├─ docs/
│  ├─ articles/                   # 自己新增的文章
│  ├─ assets/                     # 图片、附件等资源
│  ├─ guide/                      # 使用指南
│  ├─ stylesheets/extra.css       # 自定义样式
│  ├─ index.md                    # 首页
│  └─ about.md                    # 关于页面
├─ mkdocs.yml                     # 站点设置和导航
├─ requirements.txt              # Python 依赖
└─ README.md
```

`articles/` 和 `assets/` 可以在发布第一篇文章时创建。

## 日常发布文章

```powershell
cd F:\code\publicbook\mkdocs
git pull --ff-only origin main
.\.venv\Scripts\Activate.ps1
mkdocs build --strict
git add mkdocs.yml docs
git diff --cached
git commit -m "docs: add 文章标题"
git push origin main
```

推送后 GitHub Actions 会自动构建并发布网站。

## 第一次配置环境

```powershell
cd F:\code\publicbook\mkdocs
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
mkdocs serve
```

浏览器打开 <http://127.0.0.1:8000/> 预览。

## 完整说明

- [文章发布完整指南](docs/guide/publishing-articles.md)
- [环境与目录](docs/guide/getting-started.md)
- [部署与维护](docs/guide/deployment.md)
