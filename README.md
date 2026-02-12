# Plex MCP Server (Hardened Vendor Build)

This repository is a hardened vendor fork of `vladimir-tutin/plex-mcp-server` for use with Docker MCP Toolkit and LM Studio.

## What changed

- Patched vulnerable dependencies:
  - `aiohttp` -> `3.13.3`
  - `cryptography` -> `46.0.5`
- Removed explicit TLS verification bypass in server admin requests.
- Removed verbose OAuth token-proxy response logging.
- Redirected all stdout `print()` output to stderr so MCP `stdio` framing is not corrupted.
- Disabled `server_empty_trash` by removing tool registration.
- Added a containerized runtime entrypoint suitable for MCP Toolkit.

## Build

```bash
docker build -t local/plex-mcp-server:toolkit .
```

## Docker MCP Toolkit usage

1. Add this image as a local server in your Docker MCP catalog.
2. Provide:
- `PLEX_URL` (for example `http://<plex-host>:32400`)
- `PLEX_TOKEN` (server token)
3. Enable the server and connect your MCP client (LM Studio).

## Notes

- This build still includes destructive tools such as media/playlist/collection deletion and Butler task execution.
- `server_empty_trash` is intentionally disabled in this hardened build.

## Upstream

- Source project: [vladimir-tutin/plex-mcp-server](https://github.com/vladimir-tutin/plex-mcp-server)
