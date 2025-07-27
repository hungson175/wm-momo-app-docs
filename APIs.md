
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
  }
}

```


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

Default: limit = 3

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "suggestions": [
      {
        "query": "Tại sao nên mua MBB ?"
      },
      {
        "query": "Phân tích kỹ thuật VN-Index hôm nay"
      },
      {
        "query": "So sánh quỹ mở và trái phiếu doanh nghiệp"
      }
    ]
  }
}

```

**Valid Screen Values:** `home`, `market`, `portfolio`, `trade`, `opportunities`
this will be provided by another backend api later on

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
	    "unrealized_pnl_amount": 27000000
    }
  }
}

```

### 3. Personalized Products

```
GET /api/v1/products/personalized?limit=4

```

Default: limit = 4

**Authentication:** Required

**Response:**

```json
{
  "success": true,
  "data": {
    "products": [
      {
        "product_id": 123,
        "type": "trading",
        "title": "Chứng khoán",
        "icon_name": "trending_up",
        "extra_tag": null,
        "priority": 1
      },
      {
        "product_id": 456,
        "type": "savings",
        "title": "Mobond",
        "icon_name": "savings",
        "extra_tag": "6.5%",
        "priority": 2
      },
      {
        "product_id": 789,
        "type": "investment",
        "title": "Quỹ mở VCBF-MGF",
        "icon_name": "account_balance",
        "extra_tag": "Top 1",
        "priority": 3
      },
      {
        "product_id": 321,
        "type": "ipo",
        "title": "IPO FPT Digital",
        "icon_name": "new_releases",
        "extra_tag": "Hot",
        "priority": 4
      }
    ]
  }
}

```

**Valid Product Types:** `trading`, `savings`, `investment`, `ipo`, `service` - will be provided by another API from backend

### 4. Recommendations

```
GET /api/v1/recommendations/home-recommended-fin-entities?limit=3

```

Default: limit = 3

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
        "price": 12450,
        "reason": "Uy tín, ổn định 8%",
        "priority": 1
      },
      {
        "fin_entity_id": 245,
        "type": "stock",
        "entity_name": "VCB - Vietcombank",
        "description": "Cổ phiếu blue-chip ngân hàng",
        "price": 89500,
        "reason": "Tăng trưởng ổn định, cổ tức cao",
        "priority": 2
      },
      {
        "fin_entity_id": 489,
        "type": "etf",
        "entity_name": "VFMVN30 ETF",
        "description": "Theo dõi VN30 Index",
        "price": 18700,
        "reason": "Đa dạng hóa, phí thấp",
        "priority": 4
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
    "granularity": "weekly",
    "data_points": [
      {
        "timestamp": "2025-01-01T00:00:00Z",
        "value": 500000000,
        "date": "2025-01-01"
      },
      {
        "timestamp": "2025-01-08T00:00:00Z",
        "value": 510000000,
        "date": "2025-01-08"
      },
      {
        "timestamp": "2025-01-15T00:00:00Z",
        "value": 515000000,
        "date": "2025-01-15"
      },
      {
        "timestamp": "2025-01-22T00:00:00Z",
        "value": 520000000,
        "date": "2025-01-22"
      },
      {
        "timestamp": "2025-01-26T00:00:00Z",
        "value": 527000000,
        "date": "2025-01-26"
      }
    ],
    "summary": {
      "start_value": 500000000,
      "end_value": 527000000
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

```json
{
  "success": true,
  "data": {
    "full_name": "Nguyễn Văn A",
    "avatar_url": "https://cdn.momo.vn/avatars/user_12345.jpg",
    "account_id": "ACC123456",
    "kyc_status": "verified",
  }
}

```