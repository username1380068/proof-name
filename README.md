# 证明札记：零基础上手

这是一个 Quarto 数学笔记网站模板。每篇包含“定理陈述 → 证明路线 → 各步详证”，支持中文、LaTeX 公式、页内跳转、跨页引用、全文搜索和自动条目目录。

初次搭建可以全部在 GitHub 网页上操作，无需先安装 Git、Python、R 或 Quarto。模板只含文字和数学公式，GitHub Actions 会安装 Quarto 并生成网页。

## 1. 创建仓库

1. 登录 GitHub，打开 <https://github.com/new>。
2. 在 **Repository name** 填 `proof-notes`。
3. 可选描述：`定理、证明路线与分步详证`。
4. 选择 **Public**。GitHub Free 支持用公开仓库提供 GitHub Pages。
5. 打开 **Add README**，其他选项暂时保持默认。
6. 点击 **Create repository**。

“仓库”可以理解为 GitHub 上存放这个项目的文件夹。这里采用公开仓库，所上传的笔记和源文件都会公开。

## 2. 先启用网页发布

1. 在刚创建的仓库顶部点击 **Settings**。
2. 左侧点击 **Pages**。
3. 找到 **Build and deployment** 下的 **Source**。
4. 选择 **GitHub Actions**。暂时不用选择下方的其他模板。

先做这一步，再上传网站文件，可以避免首次工作流因 Pages 未启用而失败。

## 3. 上传模板文件

1. 将下载的 `proof-notes-starter.zip` 解压。
2. 打开解压后的 `proof-notes` 文件夹，确认能看到 `_quarto.yml`、`index.qmd`、`theorems`、`.github` 等项目。
3. 回到 GitHub 仓库的 **Code** 标签页，点击 **Add file → Upload files**。
4. 把 `proof-notes` 文件夹**里面的全部文件和子文件夹**拖到上传区域。不要上传压缩包，也不要把外层 `proof-notes` 文件夹整体套进去。
5. 在提交说明中填写 `Add proof notes website`，点击 **Commit changes**。如果出现分支选择，选择直接提交到 `main`。
6. 提交后，仓库首页应该直接看见 `_quarto.yml`、`index.qmd`、`theorems` 和 `.github`。

GitHub 网页可以拖入文件夹并保留其结构。上传会替换创建仓库时自动生成的 README，这是正常的。

**如果 `.github` 没有上传成功：** 在仓库首页点击 **Add file → Create new file**，把文件名写为 `.github/workflows/publish.yml`，然后用记事本打开本地同名文件，将全部内容复制过去并提交。GitHub 会根据文件名中的斜杠建立文件夹。

## 4. 打开你的网站

1. 点击仓库顶部的 **Actions**。
2. 找到 **Publish proof notes**，打开最近一次运行。
3. 等待 `build` 和 `deploy` 完成并出现绿色勾号；首次发布可能需要几分钟。
4. 回到 **Settings → Pages**，点击 **Visit site**。

如果用户名为 `alice`，仓库名为 `proof-notes`，默认网站地址就是 `https://alice.github.io/proof-notes/`。

注意区分：`github.com/alice/proof-notes` 是存放文件的仓库；`alice.github.io/proof-notes/` 才是供读者阅读的网站。

## 5. 修改第一篇笔记

1. 在仓库 **Code** 页面打开 `theorems/finite-domain.qmd`。
2. 点击铅笔按钮 **Edit this file**。
3. 先试着把开头的中文标题或一段说明改成自己的文字。
4. 点击 **Commit changes** 保存。
5. 等待新的一次 Actions 运行成功，再刷新网站。

`.qmd` 是“正文 + 少量排版标记”的文本文件。GitHub 文件页可能显示原始文本；读者阅读时应打开发布后的网站。

新增笔记时，进入 `theorems` 文件夹，点击 **Add file → Create new file**，文件名用 `英文短名.qmd`，再复制网站“阅读与写作”页中的模板。添加完成后，主页目录和左侧导航会自动收录。

## 最常用的语法

```markdown
## 证明路线 {#proof-roadmap}

1. [第一步：证明单射](#step-injective)。这里写一句解释。

## 详细证明

### 第一步：证明单射 {#step-injective}

这里写详细论证。例如，$a(x-y)=0$。

[返回证明路线](#proof-roadmap)
```

方括号中的内容是链接文字；圆括号中的 `#step-injective` 指向带有同名 `{#step-injective}` 标记的标题。可更改中文标题，但尽量保留已被引用的标记和文件名。

## 文件分别做什么

| 文件 | 作用 | 日常是否需要改 |
| --- | --- | --- |
| `theorems/*.qmd` | 每篇定理或引理的内容 | 经常 |
| `index.qmd` | 首页介绍与自动目录 | 偶尔 |
| `guide.qmd` | 阅读说明与可复制写作模板 | 偶尔 |
| `_quarto.yml` | 网站名称、导航、显示设置 | 很少 |
| `styles.css` | 页面样式 | 通常不用 |
| `.github/workflows/publish.yml` | 自动生成并发布网站 | 通常不用 |
| `.gitignore` | 本地使用 Git 时忽略生成文件 | 通常不用 |

## 遇到问题时

- **网站显示 404：** 先查看 Actions 是否成功；确认 Pages 的 Source 为 GitHub Actions；检查文件是否误放进了多余的外层文件夹。
- **Actions 没有任务：** 检查 `.github/workflows/publish.yml` 是否存在，以及默认分支是否为 `main`。
- **首轮发布失败：** 先检查 Pages 设置，再到 Actions 的失败运行中点击 **Re-run all jobs**。
- **跳转无效：** 检查 `(#标记)` 与标题上的 `{#标记}` 是否完全相同；同一页面不要使用重复标记。
- **公式没有排版：** 本模板使用 MathJax；网页需要能加载其脚本。也检查美元符号是否成对出现。
- **修改后看不到变化：** 等待 Actions 完成，再刷新的是网站页面，而不是仓库文件预览。

这是一份阅读和写作模板，尚不包含 Stacks Project 的自动依赖图、标签数据库或自动证明检查。跨页“应用”链接由作者手工维护。

## 官方文档

- Quarto Markdown 与公式：<https://quarto.org/docs/authoring/markdown-basics.html>
- Quarto 自动条目目录：<https://quarto.org/docs/websites/website-listings.html>
- GitHub Pages 创建网站：<https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site>
- GitHub Pages 自定义发布工作流：<https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages>

## 本次模板的验证范围

已检查 4 个内容文件中的 20 个内部链接及其目标，检查了发布工作流的基本结构。
另附的单页阅读示例已在浏览器中验证分步跳转、返回路线、引用引理、公式显示和手机宽度。
示例展示的是内容与跳转结构，正式 Quarto 网站还会增加首页、导航与搜索。
由于官方工具包下载过慢，本地未完成整个 Quarto 网站的构建；首次完整构建和部署仍需上传后由 GitHub Actions 验证。
