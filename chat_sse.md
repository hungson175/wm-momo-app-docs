request body 

{
   "content": "Xin chào!",
   "request_id": "req_bgdb4lzhw"
}


response - sse stream

: Chat completion stream started

event: message
id: req_xyz789-1
data: {
  "request_id": "req_xyz789",
  "type": "chunk",
  "content": "Đây"
}

event: message
id: req_xyz789-2
data: {
  "request_id": "req_xyz789",
  "type": "chunk",
  "content": "là"
}

event: message
id: req_xyz789-3
data: {
  "request_id": "req_xyz789",
  "type": "chunk",
  "content": "một"
}

event: message
id: req_xyz789-4
data: {
  "request_id": "req_xyz789",
  "type": "chunk",
  "content": "đoạn"
}

event: message
id: req_xyz789-5
data: {
  "request_id": "req_xyz789",
  "type": "chunk",
  "content": "stream"
}

event: message
id: req_xyz789-10
data: {
  "request_id": "req_xyz789",
  "type": "chart",
  "chart_type": "column",
  "content": {
    "title": "Biểu đồ",
    "data": [1, 2, 3]
  }
}

event: message
id: req_xyz789-11
data: {
  "request_id": "req_xyz789",
  "type": "follow_up",
  "content": [
    "Bạn muốn hỏi tiếp điều gì?",
    "Bạn có cần thêm thông tin không?"
  ]
}

: Chat completion finished
