# [API 名称] API 参考

> **版本**：v1
> **基础 URL**：`https://api.example.com/v1`
> **最后更新**：[日期]

## 概述

[API 及其用途的简要描述]

## 认证

### Bearer 令牌

所有 API 请求都需要使用 Bearer 令牌进行认证：

```http
Authorization: Bearer <your-token>
```

### 获取令牌

```http
POST /auth/token
Content-Type: application/json

{
  "client_id": "your-client-id",
  "client_secret": "your-client-secret"
}
```

**响应**：
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

---

## 速率限制

| 限制 | 窗口 | 范围 |
|------|------|------|
| 100 请求 | 1 分钟 | 每 IP |
| 1000 请求 | 1 小时 | 每用户 |

速率限制响应头：
- `X-RateLimit-Limit`：请求限制
- `X-RateLimit-Remaining`：剩余请求数
- `X-RateLimit-Reset`：重置时间戳（Unix）

---

## 通用响应格式

### 成功响应

```json
{
  "data": { ... },
  "meta": {
    "timestamp": "2024-01-01T00:00:00Z",
    "requestId": "uuid"
  }
}
```

### 错误响应

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "人类可读的消息",
    "details": { ... }
  }
}
```

### 分页

```json
{
  "data": [ ... ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "totalPages": 5,
    "hasNext": true,
    "hasPrev": false
  }
}
```

---

## 端点

### [资源名称]

---

#### 列出 [资源]

```http
GET /resources
```

**查询参数**：

| 参数 | 类型 | 必填 | 默认值 | 描述 |
|------|------|------|--------|------|
| page | integer | 否 | 1 | 页码 |
| limit | integer | 否 | 20 | 每页数量（最大：100） |
| sort | string | 否 | created_at | 排序字段 |
| order | string | 否 | desc | 排序顺序（asc/desc） |
| search | string | 否 | - | 搜索查询 |

**示例请求**：
```bash
curl -X GET "https://api.example.com/v1/resources?page=1&limit=10" \
  -H "Authorization: Bearer <token>"
```

**响应**：`200 OK`
```json
{
  "data": [
    {
      "id": "uuid-1",
      "name": "资源 1",
      "createdAt": "2024-01-01T00:00:00Z"
    },
    {
      "id": "uuid-2",
      "name": "资源 2",
      "createdAt": "2024-01-02T00:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 50,
    "totalPages": 5
  }
}
```

---

#### 获取 [资源]

```http
GET /resources/{id}
```

**路径参数**：

| 参数 | 类型 | 描述 |
|------|------|------|
| id | uuid | 资源 ID |

**示例请求**：
```bash
curl -X GET "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>"
```

**响应**：`200 OK`
```json
{
  "data": {
    "id": "uuid-1",
    "name": "资源 1",
    "description": "资源描述",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z",
    "updatedAt": "2024-01-01T00:00:00Z"
  }
}
```

**错误响应**：

| 状态码 | 代码 | 描述 |
|--------|------|------|
| 404 | NOT_FOUND | 资源未找到 |

---

#### 创建 [资源]

```http
POST /resources
```

**请求体**：

| 字段 | 类型 | 必填 | 验证 | 描述 |
|------|------|------|------|------|
| name | string | 是 | 1-255 字符 | 资源名称 |
| description | string | 否 | 最大 1000 字符 | 描述 |
| status | string | 否 | active/inactive | 状态 |

**示例请求**：
```bash
curl -X POST "https://api.example.com/v1/resources" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "新资源",
    "description": "资源描述"
  }'
```

**响应**：`201 Created`
```json
{
  "data": {
    "id": "uuid-new",
    "name": "新资源",
    "description": "资源描述",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

**错误响应**：

| 状态码 | 代码 | 描述 |
|--------|------|------|
| 400 | VALIDATION_ERROR | 请求体无效 |
| 409 | CONFLICT | 资源已存在 |

---

#### 更新 [资源]

```http
PUT /resources/{id}
```

**路径参数**：

| 参数 | 类型 | 描述 |
|------|------|------|
| id | uuid | 资源 ID |

**请求体**：

| 字段 | 类型 | 必填 | 描述 |
|------|------|------|------|
| name | string | 否 | 资源名称 |
| description | string | 否 | 描述 |
| status | string | 否 | 状态 |

**示例请求**：
```bash
curl -X PUT "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "更新后的名称"
  }'
```

**响应**：`200 OK`
```json
{
  "data": {
    "id": "uuid-1",
    "name": "更新后的名称",
    "description": "资源描述",
    "status": "active",
    "updatedAt": "2024-01-01T12:00:00Z"
  }
}
```

---

#### 删除 [资源]

```http
DELETE /resources/{id}
```

**路径参数**：

| 参数 | 类型 | 描述 |
|------|------|------|
| id | uuid | 资源 ID |

**示例请求**：
```bash
curl -X DELETE "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>"
```

**响应**：`204 No Content`

---

## 错误代码

| 代码 | HTTP 状态 | 描述 |
|------|-----------|------|
| UNAUTHORIZED | 401 | 认证无效或缺失 |
| FORBIDDEN | 403 | 权限不足 |
| NOT_FOUND | 404 | 资源未找到 |
| VALIDATION_ERROR | 400 | 请求数据无效 |
| CONFLICT | 409 | 资源冲突 |
| RATE_LIMITED | 429 | 请求过多 |
| INTERNAL_ERROR | 500 | 服务器错误 |

---

## Webhooks

### 事件类型

| 事件 | 描述 |
|------|------|
| resource.created | 新资源创建 |
| resource.updated | 资源更新 |
| resource.deleted | 资源删除 |

### 负载格式

```json
{
  "event": "resource.created",
  "timestamp": "2024-01-01T00:00:00Z",
  "data": {
    "id": "uuid",
    "name": "资源"
  }
}
```

---

## SDK

- [JavaScript/TypeScript SDK](链接)
- [Python SDK](链接)
- [Java SDK](链接)

---

## 变更日志

| 版本 | 日期 | 变更 |
|------|------|------|
| v1.0.0 | [日期] | 初始发布 |
