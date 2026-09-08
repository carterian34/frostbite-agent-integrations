# Frostbite agent integrations

This repository packages Frostbite's authenticated MCP server for supported AI clients.

Each client package connects to the same Frostbite streamable-HTTP endpoint and uses Frostbite OAuth. The checked-in endpoint is `http://localhost/mcp` for local development only. Before public distribution, replace it with Frostbite's public HTTPS MCP endpoint in every client configuration.

## Packages

- `plugins/frostbite-codex`: installable Codex plugin and marketplace entry.
- `plugins/frostbite-claude`: Claude Code marketplace plugin and MCP configuration.
- `plugins/frostbite-gemini`: Gemini CLI MCP configuration and installation notes.

The server, OAuth authorization rules, and tool behavior live in the Frostbite backend repository; this repository contains only client integration material.
