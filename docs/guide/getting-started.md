# 开始使用

## 目录结构

```text
.
├─ .github/workflows/deploy.yml
├─ docs/
│  ├─ guide/
│  │  ├─ getting-started.md
│  │  └─ deployment.md
│  ├─ stylesheets/extra.css
│  ├─ about.md
│  └─ index.md
├─ mkdocs.yml
└─ requirements.txt
```

## 本地预览

在项目根目录执行：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
mkdocs serve
```

浏览器访问 `http://127.0.0.1:8000/`。修改 Markdown 后页面会自动刷新。

## 添加页面

例如创建 `docs/network/index.md`：

```markdown
# 网络笔记

在这里编写正文。
```

然后在 `mkdocs.yml` 中加入导航：

```yaml
nav:
  - 首页: index.md
  - 网络笔记: network/index.md
```

## 添加图片

将图片放入 `docs/assets/images/`，在 Markdown 中使用相对路径：

```markdown
![图片说明](../assets/images/example.png)
```

不要使用以 `/` 开头的绝对路径，以免部署到子路径时出现资源失效。
