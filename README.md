# Blocksize Cursor Plugins

This repository publishes Blocksize Cursor plugins.

## Plugins

- `blocksize-market-data`: Clerk-authenticated remote MCP for read-only live crypto, equity, FX, and metals market data in Cursor.

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

## Source

The marketplace entry points at `blocksize-market-data`, which contains the installable Cursor plugin manifest and MCP configuration.
