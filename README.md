# Auto Task MCP Server

一个支持 HTTP 的 MCP (Model Context Protocol) 服务器，提供 `sayhello` 工具。

## 功能

- ✅ HTTP MCP 服务器
- ✅ `sayhello` 工具 - 支持自定义问候语
- ✅ CORS 支持
- ✅ 健康检查端点

## 安装和运行

1. 安装依赖：
```bash
npm install
```

2. 启动服务器：
```bash
npm start
# 或开发模式
npm run dev
```

服务器将在 `http://localhost:3002` 启动。

## 端点

- `GET /health` - 健康检查
- `POST /mcp` - MCP 协议端点

## 工具

### sayhello

向指定的人说你好，支持自定义消息。

**参数：**
- `name` (可选): 要问候的名字，默认为 "World"
- `message` (可选): 自定义消息

**示例：**
```json
{
  "method": "tools/call",
  "params": {
    "name": "sayhello",
    "arguments": {
      "name": "Alice",
      "message": "Have a great day!"
    }
  }
}
```

**响应：**
```json
{
  "content": [
    {
      "type": "text",
      "text": "Hello, Alice! Have a great day!"
    }
  ]
}
```

## 测试

使用 curl 测试服务器：

```bash
# 健康检查
curl http://localhost:3002/health

# 列出工具
curl -X POST http://localhost:3002/mcp \
  -H "Content-Type: application/json" \
  -d '{"method": "tools/list"}'

# 调用 sayhello 工具
curl -X POST http://localhost:3002/mcp \
  -H "Content-Type: application/json" \
  -d '{
    "method": "tools/call",
    "params": {
      "name": "sayhello",
      "arguments": {
        "name": "World",
        "message": "Nice to meet you!"
      }
    }
  }'
```