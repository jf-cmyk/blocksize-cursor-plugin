# Blocksize Market Data Cursor Plugin

Blocksize Market Data connects Cursor agents to Blocksize's Clerk-authenticated
remote MCP server for read-only live crypto, equity, FX, and metals market data.

Cursor users sign in with Blocksize through Clerk. After auth, the MCP server
exposes discovery tools plus daily-credit live data tools. This package points
at the dedicated Cursor endpoint, separate from Blocksize's public x402 registry
endpoint and the pay.sh flow.

## Install

Add the MCP server in Cursor with this config:

```json
{
  "mcpServers": {
    "blocksize-market-data": {
      "url": "https://mcp.blocksize.info/cursor/mcp/"
    }
  }
}
```

Cursor deeplink:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=blocksize-market-data&config=eyJ1cmwiOiJodHRwczovL21jcC5ibG9ja3NpemUuaW5mby9jdXJzb3IvbWNwLyJ9
```

## MCP Server

This plugin registers the Cursor-specific hosted Blocksize MCP server:

```json
{
  "mcpServers": {
    "blocksize-market-data": {
      "url": "https://mcp.blocksize.info/cursor/mcp/"
    }
  }
}
```

## What Agents Can Do

- Search supported crypto, equity ticker, FX, and metals instruments.
- List supported instrument namespaces.
- Show the signed-in user's remaining daily Blocksize data credits.
- Fetch read-only VWAP, bid/ask, FX, and metal snapshots.
- Use daily server-side credits through Clerk-authenticated Cursor sessions.

## What Agents Cannot Do Through This Plugin

- Execute wallet transactions.
- Submit x402 payment proofs.
- Spend USDC directly from Cursor.
- Write trades, orders, account changes, or other mutable actions.

## Smoke Test

```bash
rm -rf ~/.mcp-auth

npx -y -p mcp-remote@latest mcp-remote-client \
  https://mcp.blocksize.info/cursor/mcp/ \
  --transport http-only \
  --debug
```

Expected result: Clerk auth opens, the client stores OAuth tokens, connects over
Streamable HTTP, and lists the Blocksize market-data tools.

## Links

- Homepage: https://mcp.blocksize.info
- Cursor MCP endpoint: https://mcp.blocksize.info/cursor/mcp/
- OAuth callback: https://mcp.blocksize.info/cursor/mcp/auth/callback
- Public x402 MCP endpoint: https://mcp.blocksize.info/mcp/server/
- OpenAPI reference: https://mcp.blocksize.info/openapi.json
- x402scan listing: https://www.x402scan.com/server/3d0ad7cd-9e98-473a-8409-25813530df66

## License

MIT
