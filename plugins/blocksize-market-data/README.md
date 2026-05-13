# Blocksize Market Data for Cursor

Blocksize Market Data connects Cursor agents to Blocksize's hosted MCP server at
`mcp.blocksize.info` for read-only market-data discovery and live data snapshots.

This Cursor plugin uses the dedicated Clerk-authenticated MCP endpoint:

```text
https://mcp.blocksize.info/cursor/mcp/
```

After sign-in, Cursor can call Blocksize tools directly from an agent workflow.
The integration is read-only and includes 50 Blocksize data credits per user per
day. It is separate from Blocksize's public paid API and registry flows.

## What Is Possible

Cursor agents can use this plugin to:

- Search supported crypto, equity, FX, and metals instruments.
- List supported instrument namespaces.
- Check the signed-in user's remaining daily Blocksize data credits.
- Fetch live crypto VWAP snapshots.
- Fetch live crypto and supported equity bid/ask snapshots.
- Fetch live FX bid, ask, and mid-rate snapshots.
- Fetch supported metal spot-price snapshots.

Each signed-in Cursor user receives 50 Blocksize data credits per day. Discovery
tools are available for finding instruments and metadata; live data tools spend
daily credits according to the server's active tool-cost configuration.

Typical prompts:

```text
Search Blocksize for BTC market data instruments.
```

```text
Get the latest BTC-USD VWAP from Blocksize.
```

```text
Show my remaining Blocksize data credits.
```

```text
Get the current EURUSD FX snapshot.
```

```text
Get the latest XAUUSD metal price.
```

## Data Offerings

Blocksize's hosted MCP server exposes these market-data surfaces to Cursor:

| Offering | Tooling | Notes |
| --- | --- | --- |
| Crypto discovery | `search_pairs`, `list_instruments` | Search supported pairs and metadata before making live calls. |
| Crypto VWAP | `get_vwap` | Institutional VWAP snapshots for supported crypto pairs such as `BTC-USD`. |
| Crypto bid/ask | `get_bid_ask` | Latest bid, ask, and spread for supported crypto pairs. |
| Equities bid/ask | `get_bid_ask` | Supported equity tickers through the shared bid/ask surface. |
| FX | `get_fx_rate` | Bid, ask, and mid-rate snapshots for supported FX pairs such as `EURUSD`. |
| Metals | `get_metal_price` | Spot snapshots for supported metal tickers such as `XAUUSD`. |
| Credits | `get_credit_balance` | Shows the authenticated user's remaining balance from the included 50 daily Blocksize credits. |

The public health endpoint at `https://mcp.blocksize.info/health` also exposes
current service metadata, supported links, pricing categories, and the active
Cursor connector configuration.

## MCP Tools

This plugin currently exposes these read-only MCP tools:

- `search_pairs`: Search supported crypto, equity, FX, and metal instruments by
  symbol or asset name.
- `list_instruments`: List supported instruments for a Blocksize service
  namespace.
- `get_credit_balance`: Show remaining daily data credits for the signed-in
  Cursor user.
- `get_vwap`: Fetch a crypto VWAP snapshot for one supported pair.
- `get_bid_ask`: Fetch bid/ask data for one supported crypto pair or equity
  ticker.
- `get_fx_rate`: Fetch a supported FX pair snapshot.
- `get_metal_price`: Fetch a supported metal spot-price snapshot.

All tools are read-only. The plugin cannot write orders, execute trades, move
funds, or mutate user accounts.

## Access Model

Cursor uses this endpoint:

```text
https://mcp.blocksize.info/cursor/mcp/
```

The endpoint supports OAuth discovery for MCP clients:

```text
https://mcp.blocksize.info/.well-known/oauth-protected-resource/cursor/mcp/
https://mcp.blocksize.info/.well-known/oauth-authorization-server
```

Users sign in with Blocksize through Clerk. The MCP client receives OAuth tokens
and then calls the hosted MCP server over Streamable HTTP. Live data calls spend
from the included 50 daily Blocksize data credits. Cursor does not submit payment
proofs, initiate wallet transactions, or spend funds directly.

## Install

Add this MCP server config in Cursor:

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

## What This Is Not

This Cursor plugin does not:

- Execute wallet transactions.
- Submit payment proofs.
- Spend funds directly from Cursor.
- Place trades or orders.
- Change accounts, balances, positions, or payment settings.

For Blocksize's public paid API and registry-oriented integrations, use:

```text
https://mcp.blocksize.info/mcp/server/
```

## Smoke Test

You can test the hosted Cursor MCP endpoint without Cursor using `mcp-remote`:

```bash
rm -rf ~/.mcp-auth

npx -y -p mcp-remote@latest mcp-remote-client \
  https://mcp.blocksize.info/cursor/mcp/ \
  --transport http-only \
  --debug
```

Expected result:

- Clerk auth opens in the browser.
- The client stores OAuth tokens.
- The MCP client connects over Streamable HTTP.
- The server lists Blocksize's read-only market-data tools.

## Links

- Blocksize MCP server: https://mcp.blocksize.info
- Cursor MCP endpoint: https://mcp.blocksize.info/cursor/mcp/
- OAuth callback: https://mcp.blocksize.info/cursor/mcp/auth/callback
- OAuth protected-resource metadata: https://mcp.blocksize.info/.well-known/oauth-protected-resource/cursor/mcp/
- OAuth authorization-server metadata: https://mcp.blocksize.info/.well-known/oauth-authorization-server
- Public MCP endpoint: https://mcp.blocksize.info/mcp/server/
- OpenAPI reference: https://mcp.blocksize.info/openapi.json

## License

MIT
