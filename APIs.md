# MoMo API Specification

## Response Format

### ✅ Success Response

```json
{
  "success": true,
  "data": {
    /* API-specific data */
  }
}
```

### ❌ Error Response

```json
{
  "success": false,
  "error": {
    "code": 401,
    "message": "Token hết hạn hoặc không hợp lệ",
    "details": "Chi tiết kỹ thuật nếu cần debug"
  }
}
```

---

## 🤖 AI Suggestions (Unified)

### AI Suggestions for All Screens

`POST /api/v1/ai-suggestions`

**Request Body:**

```json
{
  "screen": "home", // home, market, news, ...
  "limit": 3, // Số lượng gợi ý tối đa (default: 3, max: 10)
  "context": {
    "stock_code": "VCB" // for stock detail, fund detail
  }
}
```

- `screen`: home | market | news | history | order | account
- `limit`: Number of suggestions (default: 3, max: 10)

**Response Format:**

```json
{
  "success": true,
  "data": {
    "screen": "home",
    "suggestions": [
      {
        "id": "home_001",
        "query": "Tại sao nên mua MBB ?",
        "category": "stock_analysis",
        "priority": 1
      },
      {
        "id": "home_002",
        "query": "Danh mục đầu tư của tôi có cân bằng không?",
        "category": "portfolio_analysis",
        "priority": 2
      },
      {
        "id": "home_003",
        "query": "Xu hướng thị trường tuần này như thế nào?",
        "category": "market_trend",
        "priority": 3
      }
    ]
  }
}
```

**Suggestion Categories:**

- `stock_analysis`: Phân tích cổ phiếu cụ thể
- `portfolio_analysis`: Phân tích danh mục đầu tư
- `market_trend`: Xu hướng thị trường
- `investment_advice`: Lời khuyên đầu tư
- `technical_analysis`: Phân tích kỹ thuật
- `fundamental_analysis`: Phân tích cơ bản
- `news_impact`: Tác động tin tức
- `risk_management`: Quản lý rủi ro

---

## 🏠 Home Screen

### 1. Portfolio Summary

`GET /api/v1/portfolio/summary`

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

### 2. Personalized Products

`GET /api/v1/products/personalized`

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

### 3. Recommendations

`GET /api/v1/recommendations/home-recommended-fin-entities?limit=10`

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
      }
    ]
  }
}
```

### 4. Portfolio Chart Data

`GET /api/v1/portfolio/chart-data?timeframe=1M&granularity=daily`

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
      "end_value": 527000000
    }
  }
}
```

---

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
        "change": 1200,
        "change_percent": 1.32
      },
      {
        "code": "VCBF-FIF",
        "type": "fund",
        "price": 102500,
        "change": -1500,
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
        "change": 8.0,
        "change_percent": 0.6
      },
      {
        "code": "VN30",
        "value": 780.0,
        "change": 3.9,
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
        "change": 0.59,
        "change_percent": 6.94
      },
      {
        "code": "VCBF-FIF",
        "type": "fund",
        "price": 102000,
        "change": 1000,
        "change_percent": 0.99
      }
    ],
    "top_losers": [
      {
        "code": "VIC",
        "type": "stock",
        "price": 45200,
        "change": -800,
        "change_percent": -1.74
      },
      {
        "code": "TCBF",
        "type": "fund",
        "price": 101000,
        "change": -1000,
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
  "code": "VCB",
  "type": "stock" // "stock" | "fund"
}
```

**Response**

```json
{
  "success": true,
  "data": {
    "code": "VCB",
    "type": "stock",
    "price": 92200,
    "change": 1200,
    "change_percent": 1.32
  }
}
```

### 5. Remove from Favorites

`DELETE /api/v1/market/favorites/{type}/{code}`

| Path Parameter | Type   | Description              |
| -------------- | ------ | ------------------------ |
| `type`         | string | "stock" or "fund"        |
| `code`         | string | Mã sản phẩm (e.g. "VCB") |

**Response**

```json
{
  "success": true,
  "data": {
    "code": "VCB",
    "type": "stock",
    "removed": true
  }
}
```
