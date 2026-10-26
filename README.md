# AI-auto-pages 发电站

这是 AI-auto-pages 组织的根地址页面，发布后地址是 `https://ai-auto-pages.github.io/`。

## 文件结构

- `index.html`：页面本体，负责展示和交互。
- `data/projects.json`：下拉表单和常见问题的数据文件，改这里就能更新页面，不用改 HTML。
- `.nojekyll`：告诉 GitHub Pages 不要用 Jekyll 处理，直接按静态文件发布。

## 如何改项目数据

打开 `data/projects.json`，在 `projects` 数组里改每一项的 `name`、`price`、`description`、`supportUrl`，也可以增删项目。`download.lanzou` 和 `download.mega` 留空即可，填了也不会在页面上直接展示下载地址，需要你自己决定展示方式。

## 发布

仓库 Settings > Pages，发布源选 Deploy from a branch，分支 main，文件夹 /(root)，保存后等几分钟即可访问。
