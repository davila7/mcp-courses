# JSON-RPC

At its core, MCP uses JSON-RPC 2.0 as the message format for all communication between Clients and Servers. JSON-RPC is a lightweight remote procedure call protocol encoded in JSON, which makes it:

Human-readable and easy to debug
Language-agnostic, supporting implementation in any programming environment
Well-established, with clear specifications and widespread adoption

[image]

## 1. Requests
Sent from Client to Server to initiate an operation. A Request message includes:

- A unique identifier (id)
- The method name to invoke (e.g., tools/call)
- Parameters for the method (if any)

Example Request:

```json
{
  "jsonrpc": "2.0",
  "id": 1, // Unique identifier for this request
  "method": "tools/call",
  "params": {
    "name": "weather",
    "arguments": {
      "location": "San Francisco"
    }
  }
}
```

## 2. Responses
Sent from Server to Client in reply to a Request. A Response message includes:

- The same id as the corresponding Request
- Either a result (for success) or an error (for failure)

Example Success Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1, // Matches the id of the corresponding Request
  "result": {
    "temperature": "68°F",
    "condition": "Partly Cloudy"
  }
}
```

Example Error Response:

```json
{
  "jsonrpc": "2.0",
  "id": 1, // Matches the id of the corresponding Request
  "error": {
    "code": -32601,
    "message": "Method not found"
  }
}
```

## 3. Notifications
One-way messages that don’t require a response. Typically sent from Server to Client to provide updates or notifications about events.

Example Notification:

```json
{
  "jsonrpc": "2.0",
  "method": "progress",
  "params": {
    "message": "Processing data...",
    "percent": 50
  }
}
```