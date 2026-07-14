# 环境与目录

## 项目目录

```text
mkdocs/
├─ .github/
│  └─ workflows/
│     └─ deploy.yml
├─ docs/
│  ├─ articles/
│  │  ├─ network/
│  │  ├─ security/
│  │  └─ development/
│  ├─ assets/
│  │  └─ images/
│  ├─ guide/
│  │  ├─ getting-started.md
│  │  ├─ publishing-articles.md
│  │  └─ deployment.md
│  ├─ stylesheets/
│  │  └─ extra.css
│  ├─ about.md
│  └─ index.md
├─ mkdocs.yml
├─ requirements.txt
└─ README.md
```

| 路径 | 用途 |
| --- | --- |
| `docs/` | 所有会发布到网站的 Markdown 页面和资源 |
| `docs/articles/` | 自己新增的文章，建议按主题分类 |
| `docs/assets/` | 多篇文章共用的图片和附件 |
| `docs/guide/` | 本站使用说明 |
| `mkdocs.yml` | 站点名称、主题、插件和导航目录 |
| `.github/workflows/deploy.yml` | 推送后自动部署 GitHub Pages |
| `site/` | 本地构建产物，已忽略，不需要提交 |
| `.venv/` | 本地 Python 环境，已忽略，不需要提交 |

`articles/` 和 `assets/` 不存在时可以自行创建。

## 第一次安装

在 PowerShell 中执行：

```powershell
cd F:\code\publicbook\mkdocs
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

以后再次使用只需要：

```powershell
cd F:\code\publicbook\mkdocs
.\.venv\Scripts\Activate.ps1
```

如果 PowerShell 阻止激活脚本，可以仅在当前窗口临时放行：

```powershell
Set-ExecutionPolicy -Scope Process Bypass
.\.venv\Scripts\Activate.ps1
```

## 本地预览

```powershell
mkdocs serve
```

浏览器访问 <http://127.0.0.1:8000/>。修改 Markdown 或 `mkdocs.yml` 后页面通常会自动刷新，结束时按 `Ctrl+C`。

## 发布前检查

```powershell
mkdocs build --strict
```

只有该命令成功后再推送。下一步请阅读[文章发布方法](publishing-articles.md)。
