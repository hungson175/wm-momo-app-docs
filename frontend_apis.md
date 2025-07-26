# Frontend APIs

## Chat SSE

### Endpoint
`POST /api/v1/ai-stream-response`

### Description
Server-Sent Events (SSE) endpoint for streaming chat responses with support for multiple content types including text chunks, charts, markdown, and follow-up suggestions.

### Request

#### Headers
```
Content-Type: application/json
```

#### Body
```json
{
  "content": "string",      // User's message
  "request_id": "string"    // Unique request identifier
}
```

### Response

#### Headers
```
Content-Type: text/event-stream
Cache-Control: no-cache
Connection: keep-alive
```

#### SSE Stream Format

The response is a stream of Server-Sent Events with the following structure:

```
event: message
id: <request_id>-<sequence_number>
data: <JSON payload>
```

#### Event Types

1. **Text Chunk**
   ```json
   {
     "request_id": "string",
     "type": "chunk",
     "content": "string"    // Partial text content
   }
   ```

2. **Markdown Content**
   ```json
   {
     "request_id": "string",
     "type": "markdown",
     "content": "string"        // Markdown formatted text
   }
   ```

3. **Image Data** (including charts)
   ```json
   {
     "request_id": "string",
     "type": "image",
     "content": {
       "format": "string",      // "svg", "png", etc.
       "alt": "string",         // Alt text for accessibility
       "data": "string"         // Base64 data URI (e.g., "data:image/svg+xml;base64,...")
     }
   }
   ```

4. **Follow-up Suggestions**
   ```json
   {
     "request_id": "string",
     "type": "follow_up",
     "content": ["string", ...]  // Array of suggested follow-up questions
   }
   ```

### Example

#### Request
```json
{
  "content": "Xin chào!",
  "request_id": "req_bgdb4lzhw"
}
```

#### Response Stream
```
: Chat completion stream started

event: message
id: req_xyz789-1
data: {"request_id": "req_xyz789", "type": "chunk", "content": "Đây"}

event: message
id: req_xyz789-2
data: {"request_id": "req_xyz789", "type": "chunk", "content": "là"}

event: message
id: req_xyz789-10
data: {"request_id": "req_xyz789", "type": "image", "content": {"format": "svg", "alt": "Biểu đồ phân tích", "data": "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjMwMCI+..."}}

event: message
id: req_xyz789-11
data: {"request_id": "req_xyz789", "type": "markdown", "content": "####hello"}

event: message
id: req_xyz789-12
data: {"request_id": "req_xyz789", "type": "follow_up", "content": ["Bạn muốn hỏi tiếp điều gì?", "Bạn có cần thêm thông tin không?"]}

: Chat completion finished
```

### Notes
- The stream starts with a comment line indicating the start of the chat completion
- Each event has a unique ID composed of the request_id and a sequence number
- The stream ends with a comment line indicating completion
- Clients should handle reconnection and error scenarios appropriately

### Image Streaming Implementation

#### SVG Charts as Base64 Data URIs
Images (particularly SVG charts) are streamed as base64-encoded data URIs. This approach:
- Eliminates the need for separate API calls to fetch images
- Works offline once data is received
- Scales perfectly on all devices (SVG)
- Keeps the stream self-contained

#### Frontend Implementation Example

**React Native:**
```javascript
// Handle image event
if (event.type === 'image') {
  return <Image source={{ uri: event.content.data }} alt={event.content.alt} />;
}
```

**Web:**
```javascript
// Handle image event
if (event.type === 'image') {
  return <img src={event.content.data} alt={event.content.alt} />;
}
```

#### Backend Implementation
The backend generates SVG charts dynamically and converts them to base64 data URIs:
```python
# Example SVG generation and encoding
svg_content = generate_svg_chart(data)
svg_base64 = base64.b64encode(svg_content.encode()).decode()
data_uri = f"data:image/svg+xml;base64,{svg_base64}"
```