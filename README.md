# AI-auto-pages 发电站

这是 AI-auto-pages 组织的根地址页面，发布后地址是 `https://ai-auto-pages.github.io/`。

## 页面怎么拿数据（与原 Angular 逻辑对应）

页面不再用本仓库里的本地 JSON 做主数据源，而是运行时直接去 GitHub API 拉取维护仓库里的同一个 JSON：

- 主数据：`GET https://api.github.com/repos/blog-auto/json/contents/users/admin.json?ref=main&时间戳`
- 支持进度：`GET https://api.github.com/repos/blog-auto/json/contents/pub/endorsements.json?ref=main&时间戳`

流程和原 Angular 代码一致：

1. 先尝试相对代理路径 `/api.github.com/...`，失败再走直连 `https://api.github.com/...`，并加时间戳防缓存。
2. GitHub API 返回的 `content` 是 Base64，先 `atob` 转成字节数组，再用 `TextDecoder('utf-8')` 解码，最后 `JSON.parse`。
3. 拿到 `api_url`，对每个产品做同样的处理：解析产品 `url` 里的 `sku` 参数，把 `skuArray[0].count` 设为 `price || 1`，生成时间戳 + 4 位随机数，拼出 `custom_order_id`，重建产品 URL，并生成 `pay_url`（`api_url/pay-in1?...`）。
4. `endorsements.json` 里的 `progresses` 为空时不显示支持进度卡片，有数据时按条目显示。

之后维护 JSON 内容的方法不变：直接改 `blog-auto/json` 仓库里的那两个文件，刷新本页就能看到新数据，不用改本仓库。

## 本仓库里的文件

- `index.html`：页面本体，含上面这套拉取和转换逻辑。
- `data/projects.json`：仅作备用数据源。实时数据加载失败时页面会用它兜底，并明确提示是备用数据。
- `.nojekyll`：告诉 GitHub Pages 不要用 Jekyll 处理，直接按静态文件发布。
