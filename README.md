# MCP Server Project Documentation

## Project Structure

```
mcpserver/
├── client/examples/client.py    # MCP client with Claude integration
├── server/examples/weather.py   # Weather API server with NWS tools
└── pyproject.toml              # Dependencies and project config
```

**Key Files:**
- `client.py` - Interactive client for querying weather via natural language
- `weather.py` - Server providing weather alerts and forecasts tools
- `pyproject.toml` - Project dependencies (mcp, anthropic, httpx)

## Server Flow (weather.py)

1. **Initialize FastMCP server** → Create MCP server instance named "weather"
2. **Define tools** → Register `get_alerts()` and `get_forecast()` as available tools
3. **HTTP requests** → Make async requests to National Weather Service API with proper headers
4. **Data processing** → Parse JSON responses and format into readable strings
5. **Tool execution** → Handle tool calls from clients and return formatted weather data
6. **Transport layer** → Run server using stdio transport for client communication

## Client Flow (client.py)

1. **Initialize client** → Create MCPClient instance with Anthropic API connection
2. **Connect to server** → Launch server process via stdio and establish MCP session
3. **List tools** → Discover available tools from connected server
4. **Interactive loop** → Accept user queries in continuous chat interface
5. **Claude integration** → Send queries to Claude with available tool definitions
6. **Tool execution** → Execute server tools when Claude requests them
7. **Response handling** → Process tool results and return formatted responses to user

## Project Setup

**1. Install UV Package Manager:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**2. Clone and Setup:**
```bash
git clone <your-repo>
cd mcpserver
uv sync  # Install dependencies
```

**3. Configure API Key:**
```bash
# Option 1: Environment variable
export ANTHROPIC_API_KEY="your-api-key-here"

# Option 2: Create .env file
echo "ANTHROPIC_API_KEY=your-api-key-here" > .env
```

## How to Run Client with Server

```bash
uv run client/examples/client.py server/examples/weather.py
```

**Usage:**
1. Command starts weather server and connects client to it
2. Interactive prompt appears for entering weather queries
3. Type natural language questions about weather (e.g., "Get alerts for CA")
4. Claude will automatically call appropriate weather tools
5. Type 'quit' to exit the application
