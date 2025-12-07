# [API Name] API Reference

> **Version**: v1
> **Base URL**: `https://api.example.com/v1`
> **Last Updated**: [Date]

## Overview

[Brief description of the API and its purpose]

## Authentication

### Bearer Token

All API requests require authentication using a Bearer token:

```http
Authorization: Bearer <your-token>
```

### Obtaining a Token

```http
POST /auth/token
Content-Type: application/json

{
  "client_id": "your-client-id",
  "client_secret": "your-client-secret"
}
```

**Response**:
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "Bearer",
  "expires_in": 3600
}
```

---

## Rate Limiting

| Limit | Window | Scope |
|-------|--------|-------|
| 100 requests | 1 minute | Per IP |
| 1000 requests | 1 hour | Per User |

Rate limit headers:
- `X-RateLimit-Limit`: Request limit
- `X-RateLimit-Remaining`: Remaining requests
- `X-RateLimit-Reset`: Reset timestamp (Unix)

---

## Common Response Formats

### Success Response

```json
{
  "data": { ... },
  "meta": {
    "timestamp": "2024-01-01T00:00:00Z",
    "requestId": "uuid"
  }
}
```

### Error Response

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": { ... }
  }
}
```

### Pagination

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

## Endpoints

### [Resource Name]

---

#### List [Resources]

```http
GET /resources
```

**Query Parameters**:

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| page | integer | No | 1 | Page number |
| limit | integer | No | 20 | Items per page (max: 100) |
| sort | string | No | created_at | Sort field |
| order | string | No | desc | Sort order (asc/desc) |
| search | string | No | - | Search query |

**Example Request**:
```bash
curl -X GET "https://api.example.com/v1/resources?page=1&limit=10" \
  -H "Authorization: Bearer <token>"
```

**Response**: `200 OK`
```json
{
  "data": [
    {
      "id": "uuid-1",
      "name": "Resource 1",
      "createdAt": "2024-01-01T00:00:00Z"
    },
    {
      "id": "uuid-2",
      "name": "Resource 2",
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

#### Get [Resource]

```http
GET /resources/{id}
```

**Path Parameters**:

| Parameter | Type | Description |
|-----------|------|-------------|
| id | uuid | Resource ID |

**Example Request**:
```bash
curl -X GET "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>"
```

**Response**: `200 OK`
```json
{
  "data": {
    "id": "uuid-1",
    "name": "Resource 1",
    "description": "Resource description",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z",
    "updatedAt": "2024-01-01T00:00:00Z"
  }
}
```

**Error Responses**:

| Status | Code | Description |
|--------|------|-------------|
| 404 | NOT_FOUND | Resource not found |

---

#### Create [Resource]

```http
POST /resources
```

**Request Body**:

| Field | Type | Required | Validation | Description |
|-------|------|----------|------------|-------------|
| name | string | Yes | 1-255 chars | Resource name |
| description | string | No | Max 1000 chars | Description |
| status | string | No | active/inactive | Status |

**Example Request**:
```bash
curl -X POST "https://api.example.com/v1/resources" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "New Resource",
    "description": "Resource description"
  }'
```

**Response**: `201 Created`
```json
{
  "data": {
    "id": "uuid-new",
    "name": "New Resource",
    "description": "Resource description",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

**Error Responses**:

| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Invalid request body |
| 409 | CONFLICT | Resource already exists |

---

#### Update [Resource]

```http
PUT /resources/{id}
```

**Path Parameters**:

| Parameter | Type | Description |
|-----------|------|-------------|
| id | uuid | Resource ID |

**Request Body**:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name | string | No | Resource name |
| description | string | No | Description |
| status | string | No | Status |

**Example Request**:
```bash
curl -X PUT "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Updated Name"
  }'
```

**Response**: `200 OK`
```json
{
  "data": {
    "id": "uuid-1",
    "name": "Updated Name",
    "description": "Resource description",
    "status": "active",
    "updatedAt": "2024-01-01T12:00:00Z"
  }
}
```

---

#### Delete [Resource]

```http
DELETE /resources/{id}
```

**Path Parameters**:

| Parameter | Type | Description |
|-----------|------|-------------|
| id | uuid | Resource ID |

**Example Request**:
```bash
curl -X DELETE "https://api.example.com/v1/resources/uuid-1" \
  -H "Authorization: Bearer <token>"
```

**Response**: `204 No Content`

---

## Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| UNAUTHORIZED | 401 | Invalid or missing authentication |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| VALIDATION_ERROR | 400 | Invalid request data |
| CONFLICT | 409 | Resource conflict |
| RATE_LIMITED | 429 | Too many requests |
| INTERNAL_ERROR | 500 | Server error |

---

## Webhooks

### Event Types

| Event | Description |
|-------|-------------|
| resource.created | New resource created |
| resource.updated | Resource updated |
| resource.deleted | Resource deleted |

### Payload Format

```json
{
  "event": "resource.created",
  "timestamp": "2024-01-01T00:00:00Z",
  "data": {
    "id": "uuid",
    "name": "Resource"
  }
}
```

---

## SDKs

- [JavaScript/TypeScript SDK](link)
- [Python SDK](link)
- [Java SDK](link)

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.0.0 | [Date] | Initial release |
