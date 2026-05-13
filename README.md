# Blocksize Cursor Plugins

This repository contains Cursor plugin packaging for Blocksize's hosted MCP
market-data services. It is the marketplace source repo for Cursor-specific
integrations that connect agents to `mcp.blocksize.info`.

The first plugin in this repo is `blocksize-market-data`, a Clerk-authenticated
remote MCP connection for read-only live crypto, equity, FX, and metals data in
Cursor.

## What This Repo Publishes

- Cursor marketplace metadata in `.cursor-plugin/marketplace.json`.
- The installable `blocksize-market-data` plugin package.
- The MCP configuration that points Cursor at
  `https://mcp.blocksize.info/cursor/mcp/`.
- User-facing documentation for supported tools, data offerings, auth, and
  testing.

## Plugin

`blocksize-market-data` gives Cursor agents access to Blocksize's hosted MCP
server at `mcp.blocksize.info`. The Cursor integration is intentionally separate
from the public x402 registry endpoint and from the pay.sh deployment:

- Cursor uses Clerk OAuth sign-in and server-side daily credits.
- Public registries use Blocksize's x402-oriented discovery and payment flows.
- The plugin is read-only and cannot execute trades, wallet transfers, or other
  account-changing actions.

See [blocksize-market-data/README.md](blocksize-market-data/README.md) for the
full plugin documentation.

## Marketplace Structure

```text
.cursor-plugin/marketplace.json
blocksize-market-data/
  .cursor-plugin/plugin.json
  mcp.json
  README.md
  CHANGELOG.md
  LICENSE
  assets/
```

The marketplace entry points at `blocksize-market-data`, which contains the
installable Cursor plugin manifest and MCP server configuration.

## Blocksize MCP Server

Main server:

```text
https://mcp.blocksize.info
```

Cursor MCP endpoint:

```text
https://mcp.blocksize.info/cursor/mcp/
```

Public x402 MCP endpoint:

```text
https://mcp.blocksize.info/mcp/server/
```

The hosted server exposes discovery and market-data tools for crypto, equities,
FX, and metals. Cursor users authenticate through Clerk, then consume daily
server-side credits for live read-only data calls.
