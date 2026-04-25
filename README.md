# Brave Search MCP Server on Railway

这是一个部署在 Railway 上的 Brave Search MCP HTTP 服务。

## 部署方式

### 方式 1：通过 GitHub 部署（推荐）

1. Fork 或上传此目录到 GitHub 仓库
2. 登录 [Railway Dashboard](https://railway.app/dashboard)
3. 点击 **New Project** → **Deploy from GitHub repo**
4. 选择你上传的仓库
   - Railway 会自动识别 package.json 并运行 `npm start`
   - Railway 会自动设置 `PORT` 环境变量

### 方式 2：通过 Railway CLI

```bash
npm i -g @railway/cli
railway login
railway init
railway up
```

## 环境变量

在 Railway Dashboard 中 **必须设置**：

| 变量名 | 说明 | 示例 |
|--------|------|------|
| `BRAVE_API_KEY` | **必需** Brave Search API Key | `BSA-xxxxxxxxxx` |

不需要手动设置 `PORT`，Railway 会自动处理。

## 获取 Brave API Key

1. 前往 [Brave Search API](https://brave.com/search/api/) 注册
2. 选择 **Search** 计划（适合 AI Agents）
3. 在 [开发者面板](https://api-dashboard.search.brave.com/app/keys) 生成 API Key

## 部署完成后

Railway 会提供一个 `https://xxx.up.railway.app` 域名。

MCP 端点地址为：`https://xxx.up.railway.app/mcp`

本地测试：
```bash
curl -s -X POST https://xxx.up.railway.app/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

## 在 Hermes 中添加 MCP

部署后运行：
```bash
# 添加 MCP 服务器
hermes mcp add brave-search --url https://你的域名.up.railway.app

# 确认无认证需求（API Key 在服务端设置）
```

这样 Hermes 就能通过 Railway 上的 Brave Search MCP 服务进行搜索了。
