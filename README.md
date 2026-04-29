# Blocksize Market Data Cursor Plugin

Blocksize Market Data connects Cursor agents to Blocksize's remote MCP discovery server for real-time crypto, FX, and metals market data.

Agents can search supported instruments, inspect pricing, and find integration docs before using Blocksize's x402-paid HTTP market data endpoints with USDC settlement on Solana and Base.

## MCP Server

This plugin registers the hosted Blocksize MCP server:

```json
{
  "mcpServers": {
    "blocksize-market-data": {
      "url": "https://mcp.blocksize.info/mcp/server/"
    }
  }
}
```

## What Agents Can Do

- Search supported crypto, FX, and metals instruments.
- Inspect pricing, networks, and credit options.
- Search and fetch Blocksize integration documentation.
- Discover x402-paid HTTP endpoints for live market data.

## Links

- Homepage: https://mcp.blocksize.info
- Remote MCP endpoint: https://mcp.blocksize.info/mcp/server/
- OpenAPI reference: https://mcp.blocksize.info/openapi.json
- x402scan listing: https://www.x402scan.com/server/3d0ad7cd-9e98-473a-8409-25813530df66

## License

MIT
