# S1amesecat.github.io

Material for MkDocs 文档站点，发布地址：<https://s1amesecat.github.io/>。

## 本地运行

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
mkdocs serve
```

## 发布

推送到 `main` 分支后，GitHub Actions 会自动构建并部署 GitHub Pages。
