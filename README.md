# uapi-pro-mcp-vercel

基于 Vercel Serverless 的 UAPI Pro 搜索 MCP 服务器，支持 API Key 认证。

## 功能特性

- 🔐 **API Key 认证** - 基于 Bearer Token 的安全认证
- 🚀 **Vercel Serverless** - 无状态、自动扩缩容
- 🌐 **智能搜索** - 支持多种搜索参数和过滤条件
- 📱 **兼容性强** - 支持标准 MCP 客户端

## 快速开始

### 1. 安装依赖

```bash
npm install
```

### 2. 配置环境变量

创建 `.env.local` 文件：

```env
# UAPI Pro API Key (可选，但推荐)
UAPI_PRO_API_KEY=your-uapi-pro-api-key

# MCP API Keys (用于认证，逗号分隔)
MCP_API_KEYS=key1,key2,key3

# 应用URL (用于OAuth元数据)
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 3. 本地开发

```bash
npm run dev
```

服务器将在 http://localhost:3000 启动。

### 4. 测试认证

```bash
# 测试无认证请求（应该返回401）
curl -X POST http://localhost:3000/api/mcp   -H "Content-Type: application/json"   -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{}}'

# 测试带认证请求（应该成功）
curl -X POST http://localhost:3000/api/mcp   -H "Content-Type: application/json"   -H "Authorization: Bearer key1"   -d '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{}}'
```

### 5. 部署到 Vercel

```bash
npm i -g vercel
vercel login
vercel --prod
```

## 客户端配置

### Claude Desktop

```json
{
  "mcpServers": {
    "uapi-search": {
      "url": "https://your-domain.vercel.app/api/mcp",
      "headers": {
        "Authorization": "Bearer your-api-key"
      }
    }
  }
}
```

### Cursor

```json
{
  "mcpServers": {
    "uapi-search": {
      "url": "https://your-domain.vercel.app/api/mcp",
      "headers": {
        "Authorization": "Bearer your-api-key"
      }
    }
  }
}
```

## 可用工具

### `search_web`

使用 UAPI Pro 搜索 API 进行智能网页搜索。

**参数：**
- `query` (必填): 搜索查询关键词
- `site` (可选): 限制搜索特定网站
- `filetype` (可选): 限制文件类型 (pdf, doc, docx 等)
- `fetch_full` (可选): 是否获取完整正文
- `sort` (可选): 排序方式 (relevance/date)
- `time_range` (可选): 时间范围 (day/week/month/year)

## 许可证

MIT License
