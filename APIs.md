
# MoMo Home Screen - API Specification

**Note:** This document serves as the contract between frontend and backend. It should contain ONLY API specifications without any backend implementation notes.

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
        "priority": 1,
        "query": "Tại sao nên mua MBB ?"
      },
      {
        "priority": 2,
        "query": "Phân tích kỹ thuật VN-Index hôm nay"
      },
      {
        "priority": 3,
        "query": "So sánh quỹ mở và trái phiếu doanh nghiệp"
      }
    ]
  }
}

```

**Valid Screen Values:**
- `stock_analysis`: Phân tích cổ phiếu cụ thể
- `portfolio_analysis`: Phân tích danh mục đầu tư
- `market_trend`: Xu hướng thị trường
- `investment_advice`: Lời khuyên đầu tư
- `technical_analysis`: Phân tích kỹ thuật
- `fundamental_analysis`: Phân tích cơ bản
- `news_impact`: Tác động tin tức
- `risk_management`: Quản lý rủi ro
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
        "type": "for_kids",
        "title": "Cho con",
        "icon_name": "child",
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

**Valid Product Types:** 
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



## 📈 Market Screen

### 1. Market Favorites Tab

`GET /api/v1/market/favorites`

```json
{
  "success": true,
  "data": {
    "favorites": [
      {
        "code": "VCB",
        "type": "stock",
        "price": 92200,
        "change_percent": 1.32
      },
      {
        "code": "VCBF-FIF",
        "type": "fund",
        "price": 102500,
        "change_percent": -1.44
      }
    ]
  }
}
```

### 2. Market Indices

`GET /api/v1/market/indices`

```json
{
  "success": true,
  "data": {
    "indices": [
      {
        "code": "VNINDEX",
        "value": 1323.0,
        "change_percent": 0.6
      },
      {
        "code": "VN30",
        "value": 780.0,
        "change_percent": 0.5
      }
    ]
  }
}
```

### 3. Market Movers

`GET /api/v1/market/top-movers?period=start_of_day`

```json
{
  "success": true,
  "data": {
    "top_gainers": [
      {
        "code": "DXS",
        "type": "stock",
        "price": 9.09,
        "change_percent": 6.94
      },
      {
        "code": "VCBF-FIF",
        "type": "fund",
        "price": 102000,
        "change_percent": 0.99
      }
    ],
    "top_losers": [
      {
        "code": "VIC",
        "type": "stock",
        "price": 45200,
        "change_percent": -1.74
      },
      {
        "code": "TCBF",
        "type": "fund",
        "price": 101000,
        "change_percent": -0.98
      }
    ]
  }
}
```

### 4. Add to Favorites

`POST /api/v1/market/favorites`

**Request Body**

```json
{
  "symbol": "VCB",
  "type": "stock" // "stock" | "fund"
}
```

**Response**

```json
{
  "success": false | true,
  "data": {
    "messsage": "Some message",
  }
}
```

### 5. Remove from Favorites

`DELETE /api/v1/market/favorites/{type}/{symbol}`

| Path Parameter | Type   | Description              |
| -------------- | ------ | ------------------------ |
| `type`         | string | "stock" or "fund"        |
| `symbol`         | string | Mã sản phẩm (e.g. "VCB") |

**Response**

```json
{
  "success": false | true,
  "data": {
    "message": "Some message",
  }
}
```


## 📰 News Screen

### 1. Tabs  
`GET /api/v1/news/tabs`

**Response:**
```json
{
  "success": true,
  "data": {
    "tabs": [
      { "key": "all", "title": "Tất cả" },
      { "key": "favorites", "title": "Yêu thích" },
      { "key": "banking", "title": "Ngân hàng" },
      { "key": "technology", "title": "Công nghệ" },
      { "key": "real_estate", "title": "Bất động sản" },
      { "key": "commodities", "title": "Hàng hóa" }
    ]
  }
}
```

### 2. Fetch News Articles  
`GET /api/v1/news?tab={tab}&page={page}&page_size={page_size}`

**Query Parameters:**
- `tab`: one of the `key` values from `GET /api/v1/news/tabs`
- `page`: page index (0-based, default 0)
- `page_size`: number of articles per page (default 10, max 100)

**Response:**
```json
{
  "success": true,
  "data": {
    "articles": [
      {
        "id": 131,
        "category": "banking",
        "title": "VCB công bố kết quả kinh doanh quý 3/2025 tăng trưởng mạnh",
        "summary": "Ngân hàng TMCP Ngoại thương Việt Nam (VCB) vừa công bố kết quả kinh doanh quý 3 với lợi nhuận tăng 15% so với cùng kỳ.",
        "source": "VCB",
        "created_at": "2025-07-27T12:00:00Z",
        "thumbnail_url": "https://api.momo.vn/v1/news/images/131.jpg",
        "link": "https://api.momo.vn/v1/news/131"
      },
      {
        "id": 112,
        "category": "technology",
        "title": "FPT ký hợp đồng lớn với đối tác Nhật Bản trị giá 50 triệu USD",
        "summary": "Tập đoàn FPT vừa ký kết hợp đồng cung cấp dịch vụ công nghệ thông tin với một tập đoàn lớn tại Nhật Bản.",
        "source": "FPT",
        "created_at": "2025-07-27T10:00:00Z",
        "thumbnail_url": "https://api.momo.vn/v1/news/images/112.jpg",
        "link": "https://api.momo.vn/v1/news/112"
      }
    ],
    "page": 0,
    "page_size": 10,
    "total_pages": 13
  }
}
```
