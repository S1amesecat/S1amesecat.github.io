# 发布与维护

## 自动部署

仓库中的 `.github/workflows/deploy.yml` 会在以下情况运行：

- 向 `main` 分支推送提交；
- 在 GitHub Actions 页面手动触发。

工作流依次完成依赖安装、MkDocs 严格构建、产物上传和 GitHub Pages 部署。

## 更新文档

```powershell
git add .
git commit -m "docs: update notes"
git push
```

推送后可以在仓库的 **Actions** 页面查看部署进度。

## 部署地址

```text
https://s1amesecat.github.io/
```

## 常见问题

### Actions 构建失败

先在本地运行：

```powershell
mkdocs build --strict
```

根据终端中的文件名和行号修复配置或链接错误。

### 页面样式丢失

确认 `mkdocs.yml` 中的地址为：

```yaml
site_url: https://s1amesecat.github.io/
```

### 新增插件后远端缺少模块

把插件包同时加入 `requirements.txt`，再提交并推送。
