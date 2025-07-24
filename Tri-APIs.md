# API Reference: Chat Completions

Tài liệu này cung cấp đặc tả chi tiết cho API Chat Completions, cho phép tạo phản hồi từ mô hình chat ở cả chế độ streaming và non-streaming.

---

## Endpoint

Tạo phản hồi từ mô hình cho một cuộc hội thoại.

```
POST /v1/chat/completions
```

---

## Request Body

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| `messages` | Array | Yes | - | Một mảng các đối tượng message tạo thành lịch sử cuộc trò chuyện. |
| `stream` | Boolean | No | `false` | Nếu `true`, phản hồi sẽ được stream bằng Server-Sent Events. |
| `model` | String | No | `momo-finhay-v1` | ID của model được sử dụng. |

### Request Example

```json
{
  "messages": [
    {
      "role": "user",
      "content": "Xin chào, bạn khỏe không?"
    }
  ],
  "stream": true,
  "model": "momo-finhay-v1"
}
```

---

## Responses

Phản hồi từ API có thể chứa nhiều phần nội dung với các loại (`type`) khác nhau, chẳng hạn như `text`, `chart`, và `follow_up_question`. Các phần này có thể được trả về theo thứ tự bất kỳ.

### 1. Non-Streaming Response (`stream: false`)

Nếu `stream` là `false` hoặc không được chỉ định, API sẽ trả về một đối tượng JSON duy nhất. Trường `message.content` sẽ là một mảng chứa tất cả các phần của phản hồi.

#### Cấu trúc Response

```json
{
  "id": "req_xyz789",
  "object": "chat.completion",
  "created": 1677610700,
  "model": "momo-finhay-v1",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": [
          {
            "type": "text",
            "content": "Đây là biểu đồ về doanh thu hàng tháng."
          },
          {
            "type": "chart",
            "content": {
              "chart_type": "bar",
              "title": "Doanh thu hàng tháng",
              "data": {
                "labels": ["Tháng 1", "Tháng 2", "Tháng 3"],
                "datasets": [{
                  "label": "Doanh thu",
                  "data": [1200, 1900, 1500]
                }]
              }
            }
          },
          {
            "type": "follow_up_question",
            "content": {
              "questions": [
                "Bạn có muốn xem chi tiết theo từng sản phẩm không?",
                "So sánh với quý trước?"
              ]
            }
          }
        ]
      },
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 10,
    "completion_tokens": 85,
    "total_tokens": 95
  }
}
```

### 2. Streaming Response (`stream: true`)

Nếu `stream` là `true`, API sẽ sử dụng **Server-Sent Events (SSE)** để gửi dữ liệu.

* **Content-Type:** `text/event-stream; charset=utf-8`
* **Quy tắc streaming:**
    * Nội dung loại `text` sẽ được stream từng phần nhỏ (chunk).
    * Nội dung loại `chart` và `follow_up_question` sẽ được gửi dưới dạng một đối tượng JSON hoàn chỉnh trong một event duy nhất.

#### Các loại Event trong SSE

* `chunk`: Gửi các phần nhỏ của nội dung `text`.
* `message_part`: Gửi một phần nội dung hoàn chỉnh (dành cho `chart` và `follow_up_question`).
* `completion`: Event cuối cùng chứa thông tin hoàn thành và `usage`.

#### Ví dụ về SSE Stream

Luồng dữ liệu có thể chứa các loại event xen kẽ nhau.

```
retry: 3000

: Chat completion stream started

event: chunk
id: req_xyz789-1
data: {"id":"req_xyz789","object":"chat.completion.chunk","created":1677610700,"model":"momo-finhay-v1","choices":[{"index":0,"delta":{"content":"Đây là biểu đồ"},"finish_reason":null}]}

event: message_part
id: req_xyz789-2
data: {"id":"req_xyz789","object":"chat.completion.part","created":1677610700,"model":"momo-finhay-v1","choices":[{"index":0,"delta":{"type":"chart","content":{"chart_type":"bar","title":"Doanh thu hàng tháng","data":{"labels":["Tháng 1","Tháng 2","Tháng 3"],"datasets":[{"label":"Doanh thu","data":[1200,1900,1500]}]}}},"finish_reason":null}]}

event: chunk
id: req_xyz789-3
data: {"id":"req_xyz789","object":"chat.completion.chunk","created":1677610700,"model":"momo-finhay-v1","choices":[{"index":0,"delta":{"content":" về doanh thu hàng tháng."},"finish_reason":null}]}

event: message_part
id: req_xyz789-4
data: {"id":"req_xyz789","object":"chat.completion.part","created":1677610700,"model":"momo-finhay-v1","choices":[{"index":0,"delta":{"type":"follow_up_question","content":{"questions":["Bạn có muốn xem chi tiết theo từng sản phẩm không?","So sánh với quý trước?"]}},"finish_reason":null}]}

event: completion
id: req_xyz789-final
data: {"id":"req_xyz789","object":"chat.completion.chunk","created":1677610700,"model":"momo-finhay-v1","choices":[{"index":0,"delta":{},"finish_reason":"stop"}],"usage":{"prompt_tokens":10,"completion_tokens":85,"total_tokens":95}}

: Chat completion finished
data: [DONE]
```

#### Cấu trúc Đối tượng trong Stream

1.  **Event `chunk` (cho `type: 'text'`)**
    Trường `delta.content` chứa một phần nhỏ của chuỗi văn bản.

    ```json
    {
      "id": "req_xyz789",
      "object": "chat.completion.chunk",
      "choices": [{
        "index": 0,
        "delta": { "content": "một phần văn bản" },
        "finish_reason": null
      }]
    }
    ```

2.  **Event `message_part` (cho `type: 'chart'` hoặc `type: 'follow_up_question'`)**
    Trường `delta` chứa toàn bộ đối tượng JSON cho phần nội dung đó.

    ```json
    // Ví dụ cho type: 'chart'
    {
      "id": "req_xyz789",
      "object": "chat.completion.part",
      "choices": [{
        "index": 0,
        "delta": {
          "type": "chart",
          "content": { /* ... toàn bộ dữ liệu của chart ... */ }
        },
        "finish_reason": null
      }]
    }
    