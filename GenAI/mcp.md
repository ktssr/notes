# Model Context Protocol
    Standardizes how context should be passed to LLM.
# MCP Provides
- Pre-built Integrations
- Vendor flexibility
- Security best practices
- Univesal Standard
- Reduced duplicate work
- Future-proof development
- Clear separation of concerns

# Architecture
## Components
### Tools
    Functions called by model like DB queris, API Calls.
    Model Controlled
### Resources
    Files, Database rows, Media files, etc.
    Application Controlled
## Prompts
    Predefined templates for AI interaction
    User controlled
## MCP Servers
    Exposes Tools
    Exposes Resources
    Exposes Prompts
## MCP Hosts
    Contains MCP Client
### MCP Client
    Interacts with MCP Server via Transport Layer
    Maintain 1:1 Connection with servers to
        - Invoke tools
        - Queries resources
        - Interpolates prompts
# Transport in MCP
    uses JSON-RPC 2.0
### Request Schema
```json
{
    jsonrpc: "2.0",
    method: string,
    params?: object,
    id?: number | string | null
}
```
### Response Schema
```json
{
    jsonrpc: "2.0",
    result?: object,
    error?: {
        code: number,
        message: string,
        data?: object
    },
    id?: number | string | null
}
```
### Notification Schema
```json
{
    jsonrpc: "2.0",
    method: string,
    params?: object
}
```
## Transport Types
### stdio
Communication through standard input and output streams.

- Best for
    - Command-line applications
    - Local integrations
    - Simple process communication
    - Shell Scripts

- Key Features
    - Direct process communication
    - Lightweight and simple
    - No network overhead
    - Perfect for local tools

### Server-sent events (SSE)
Depricated and previously used fo real-time updates from server to client.

- Best for
    - Real-time updates
    - Server-to-client communication
    - Simple event-driven architectures

No longer recommended and use for backwards compatibility only.

### Streamable HTTP
New standard introduced in March 2025.
Optional HTTP Post requests with SSE streams.

- Best for
    - Web based integrations
    - Server-to-client communication over HTTP
    - Stateful sessions
    - Multiple concurrent clients
    - Resumable connections
- Key Features
    - Client to Server: HTTP Post request to MCP endpoint.
    -  Server to client: SSE stream from MCP endpoint (optional).
    -  Stateful sessions with session ID.
    -  Resumability: Event IDs and message replay.

## Connection Establishment
### Initialization
- Client sends a Initialize request to the server.
- Server responds with a Initialize response to the client.
- Client sends a  Intialize tification to the server.
- Connection is established

### Message Exchange
- Both client and server can send requests and notifications to each other.
  
### Termination
- Either client or server can send a `close` command to terminate the connection.

# Sampling
Allows MCP servers to request LLM completion through the client.

## Working
1. Server request clinet.
2. Client reviews the request.
3. LLM generates the content.
4. Client reviews the content.

> User control and privacy is maintained by Human-in-the-loop design (Human can accept/reject)

## Real world example: Calender server
- Server has meeting data but needs help creating a summary
- Server requests LLM assistance via clients
- Client handles LLM interaction, returns formatted summary
- User maintains visibility and control throughout.

### Request controls by server
- Model preferences
- System prompt suggestions
- Context inclusion options
- Sampling parameters (temperature, max tokens)

> Client/Server is a logical separation, not a physical one.Client component can act as server and vice-versa. Client and server change roles for fluent information flow between systems and avoid building the connection from scratch.

# MCP - Discovery
All MCP Capabilities follow the same discovery approach.

## Tools Discovery
Endpoint: `/tools/list`

## Resources Discovery
Endpoint: `/resources/list`

## Prompts Discovery
Endpoint: `/prompts/list`

## Key points
- Same /list pattern for all discoveries
- Client initiated (Client asks and server responds)
- Dynamic updates (Server notify client when data changes)
- All discoveries uses standard JSON-RPC 2.0 protocol.

# FastMCP
SDK for building MCP servers in python.

## create server
```python
from fastmcp import FastMCP

mcp = FastMCP("Calculator")

@mcp.tool()
def calculate_sum(a: float, b: float) -> float:
    """Add two numbers"""
    return a + b

if __name__ == "__main__":
    mcp.run()
```
> starts the server using "stdio" by default
 
 ## Run server in SSE mode

 ```python
 mcp.run(transport='sse',host='127.0.0.1',port=8000) 
 ```

 ## Run server in streamble-http mode
 
 ```python
 mcp.run(transport='streamable-http',host='127.0.0.1',port=8000,path='/mcp') 
 ```