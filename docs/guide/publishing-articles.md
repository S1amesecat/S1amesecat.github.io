# 文章发布完整指南

这份指南覆盖从创建文章到 GitHub Pages 上线的完整过程。

## 一、日常流程

每次发布按照下面的顺序操作：

1. 拉取远端最新内容；
2. 在 `docs/articles/` 中创建 Markdown 文章；
3. 添加图片或附件；
4. 在 `mkdocs.yml` 中登记导航；
5. 本地预览并严格构建；
6. 检查 Git 改动；
7. 提交并推送到 `main`；
8. 查看 GitHub Actions 和线上页面。

## 二、同步仓库

打开 PowerShell：

```powershell
cd F:\code\publicbook\mkdocs
git status
git pull --ff-only origin main
```

看到 `Already up to date.` 表示已经是最新版本。如果 `git status` 显示有未提交修改，先处理这些修改，不要强制覆盖。

## 三、建立文章目录

建议按主题分类：

```text
docs/
└─ articles/
   ├─ network/
   │  ├─ kali-network-setup.md
   │  └─ images/
   │     └─ kali-ip-address.png
   ├─ security/
   │  └─ log-analysis-basics.md
   └─ development/
      └─ python-environment.md
```

创建目录：

```powershell
New-Item -ItemType Directory -Force docs\articles\network
New-Item -ItemType Directory -Force docs\articles\network\images
```

文件名建议：

- 使用小写英文、数字和短横线；
- 使用 `.md` 扩展名；
- 不使用空格和特殊符号；
- 让文件名表达主题，例如 `kali-network-setup.md`。

中文文件名也能工作，但英文文件名更适合生成稳定链接。

## 四、编写文章

例如创建：

```text
docs/articles/network/kali-network-setup.md
```

文章模板：

```markdown
# Kali 网络配置与排错

这里用一两句话说明文章解决什么问题。

## 环境信息

- 系统：Kali Linux
- 网络模式：NAT
- 网卡：eth0

## 操作步骤

### 1. 查看网卡

运行相应命令，并说明输出和判断方法。

### 2. 修复连接

写出命令、预期结果和注意事项。

## 常见问题

记录错误现象、原因和解决方法。

## 总结

列出最终结论和关键命令。
```

写作时注意：

- 每篇文章只使用一个一级标题 `#`；
- 大章节使用 `##`，子步骤使用 `###`；
- 命令放进带语言标记的代码块；
- 截图要填写清晰的图片说明；
- 不要写入密码、Token、Cookie 或私钥。

## 五、添加图片

把文章专用图片放在文章旁边的 `images` 目录：

```text
docs/articles/network/
├─ kali-network-setup.md
└─ images/
   └─ kali-ip-address.png
```

文章中使用相对路径：

```markdown
![Kali 网卡地址](images/kali-ip-address.png)
```

图片名建议使用小写英文和短横线。不要引用电脑上的绝对路径，并注意 GitHub Pages 区分文件名大小写。

多篇文章共用的图片可以放入 `docs/assets/images/`。

## 六、加入网站目录

创建 Markdown 文件后，还需要编辑项目根目录的 `mkdocs.yml`，才能让文章显示在导航中。

示例：

```yaml
nav:
  - 首页: index.md
  - 文章:
      - 网络:
          - Kali 网络配置与排错: articles/network/kali-network-setup.md
      - 安全:
          - 日志分析基础: articles/security/log-analysis-basics.md
  - 使用指南:
      - 环境与目录: guide/getting-started.md
      - 文章发布方法: guide/publishing-articles.md
      - 部署与维护: guide/deployment.md
  - 关于: about.md
```

注意：

- 路径相对于 `docs/`，不要写开头的 `docs/`；
- YAML 只能用空格缩进，不要使用 Tab；
- 同一层级保持相同缩进；
- 导航名称可以用中文，文件路径建议用英文。

## 七、本地预览

```powershell
cd F:\code\publicbook\mkdocs
.\.venv\Scripts\Activate.ps1
mkdocs serve
```

打开 <http://127.0.0.1:8000/>，检查：

- 文章是否出现在正确目录；
- 标题层级是否正常；
- 图片和链接是否有效；
- 代码块是否完整；
- 手机宽度下是否方便阅读。

结束预览时按 `Ctrl+C`。

## 八、发布前检查

```powershell
mkdocs build --strict
git status
git diff --check
```

暂存文章、图片和导航：

```powershell
git add mkdocs.yml docs
git diff --cached
```

确认没有密码、临时文件或无关内容后再提交。

## 九、提交并推送

```powershell
git commit -m "docs: add Kali network setup article"
git push origin main
```

推送成功后，GitHub Actions 会自动安装依赖、严格构建并部署网站。

查看部署进度：

<https://github.com/S1amesecat/S1amesecat.github.io/actions>

部署地址：

<https://s1amesecat.github.io/>

通常等待几十秒到几分钟即可看到更新。仍显示旧内容时按 `Ctrl+F5`。

## 十、修改已有文章

直接修改原 Markdown 文件：

```powershell
mkdocs build --strict
git add docs\articles
git commit -m "docs: update 文章标题"
git push origin main
```

如果同时修改了导航，也要暂存 `mkdocs.yml`。

## 十一、重命名或移动

```powershell
git mv docs\articles\network\old-name.md docs\articles\network\new-name.md
```

随后修改 `mkdocs.yml` 中的路径，运行严格构建，再提交推送。旧网址会失效，因此公开过的文章不建议频繁改名。

## 十二、删除文章

```powershell
git rm docs\articles\network\old-article.md
```

再从 `mkdocs.yml` 删除对应导航，并执行：

```powershell
mkdocs build --strict
git add mkdocs.yml
git commit -m "docs: remove 文章标题"
git push origin main
```

不再使用的文章专用图片也应一并删除。

## 十三、常见错误

### 提示不是 Git 仓库

```powershell
cd F:\code\publicbook\mkdocs
```

### 严格构建失败

检查：

- `mkdocs.yml` 的缩进；
- `nav` 中的文件路径；
- Markdown 内部链接；
- 图片是否存在；
- 文件名大小写是否一致。

### 推送被拒绝：non-fast-forward

确保工作区内容已提交，然后：

```powershell
git pull --rebase origin main
git push origin main
```

发生冲突时查看 `git status`，修复后执行：

```powershell
git add 冲突文件
git rebase --continue
```

不要使用强制推送覆盖远端内容。

### 账号或权限错误

```powershell
git credential-manager github list
git credential-manager github login --username S1amesecat --browser --force
```

### GitHub Actions 失败

打开 Actions 最新的红色运行记录。通常先在本地执行 `mkdocs build --strict` 就能复现错误。

### 线上没有更新

依次确认：

1. `git push` 是否成功；
2. Actions 是否显示绿色；
3. 文章是否加入 `mkdocs.yml`；
4. 是否打开正确网址；
5. 是否已用 `Ctrl+F5` 刷新。

## 十四、网页端临时发布

进入仓库：

<https://github.com/S1amesecat/S1amesecat.github.io>

使用 **Add file → Create new file**，文件路径填写：

```text
docs/articles/主题/文章名.md
```

提交到 `main` 后，还要在线编辑 `mkdocs.yml`，把文章加入 `nav`。涉及多张图片、重命名或大量文章时，推荐使用本地 Git 流程。

## 十五、最短命令清单

```powershell
cd F:\code\publicbook\mkdocs
git pull --ff-only origin main
.\.venv\Scripts\Activate.ps1
mkdocs serve
mkdocs build --strict
git status
git add mkdocs.yml docs
git diff --cached
git commit -m "docs: add 文章标题"
git push origin main
```
