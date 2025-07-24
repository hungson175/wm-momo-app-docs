# MoMo Home Screen - API Specification

## Response Format

### Success Response

```json
{
  "success": true,
  "data": { /* API-specific data */ }
}

```

### Error Response

```json
{
  "success": false,
  "error": {
    "code": number_type_error_code,
    "message": "Human readable message in Vietnamese",
    "details": "Technical details for debugging"
  },
}

```

Bỏ meta, error code phải là number , ko phải string

### Error Codes

- `UNAUTHORIZED` (401): Token hết hạn hoặc không hợp lệ
- `FORBIDDEN` (403): Không có quyền truy cập
- `NOT_FOUND` (404): Không tìm thấy dữ liệu
- `RATE_LIMITED` (429): Quá nhiều request
- `VALIDATION_ERROR` (400): Dữ liệu request không hợp lệ
- `SERVER_ERROR` (500): Lỗi server

## Authentication

Protected APIs require Bearer token in header:

```json
{
  "Authorization": "Bearer {access_token}",
  "User-Agent": "MoMo-App/1.0",
  "Content-Type": "application/json"
}

```

---

## API Endpoints

### 1. AI Suggestions

```
GET /api/v1/ai-suggestions?screen=home&limit=3

```

Default: limit 

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "suggestions": [
      {
        "id": "suggestion_001",
        "question": "Tại sao nên mua MBB ?",
      }
    ]
  }
}

```

**Valid Screen Values:** `home`, `market`, `portfolio`, `trade`, `opportunities`

Bỏ hết, chỉ để question → query

### 2. Portfolio Summary

```
GET /api/v1/portfolio/summary

```

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "total_assets": {
      "value": 527000000,
	    "unrealized_pnl_percentage": 4.98
    }
  }
}

```

### 3. Personalized Products

```
GET /api/v1/products/personalized

```

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "products": [
      {
        "product_id": "stock_trading",
        "type": "trading",
        "title": "Chứng khoán",
        "icon_name": "trending_up",
        "extra_tag": null,
        "priority": 1
      },
      {
        "product_id": "haybond",
        "type": "savings",
        "title": "Haybond",
        "icon_name": "savings",
        "extra_tag": "6.5%",
        "priority": 3
      }
    ]
  }
}

```

**Valid Product Types:** `trading`, `savings`, `investment`, `ipo`, `service`

Notes: sửa - bỏ type trong extra tag, momo dùng màu hồng hết

### 4. Recommendations

```
GET /api/v1/recommendations/home-recommended-fin-entities?limit=10

```

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "recommendations": [
      {
        "fin_entity_id": 123,
        "type": "fund",
        "entity_name": "Quỹ trái phiếu VCBF-FIF",
        "description": "Phù hợp người mới, rủi ro thấp",
        "price": 12450
        "reason": "Uy tín, ổn định 8%",
        "priority": 1
      }
    ]
  }
}

```

### 5. Portfolio Chart Data

```
GET /api/v1/portfolio/chart-data?timeframe=1M&granularity=daily

```

**Authentication:** Required

**Parameters:**

- `timeframe`: `1W|1M|3M|6M|1Y|3Y|5Y|All`
- `granularity`: `daily|weekly|monthly`

**Response:**

```json
{
  "success": true,
  "data": {
    "timeframe": "1M",
    "granularity": "daily",
    "data_points": [
      {
        "timestamp": "2025-01-01T00:00:00Z",
        "value": 500000000,
        "date": "2025-01-01"
      }
    ],
    "summary": {
      "start_value": 500000000,
      "end_value": 527000000,
    }
  }
}

```

### 6. User Profile

```
GET /api/v1/user/profile

```

**Authentication:** Required

**Response:**