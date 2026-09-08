# Frostbite for Claude Code

Install Frostbite from this repository's Claude Code marketplace:

```sh
claude plugin marketplace add carterian34/frostbite-agent-integrations
claude plugin install frostbite@frostbite-integrations
```

Restart Claude Code or run `/reload-plugins` if prompted, then use `/mcp` to complete the OAuth sign-in for Frostbite.

The installed plugin connects to Frostbite's public streamable-HTTP MCP endpoint at `https://thefrostbiteapp.com/mcp`.

## Local development

To connect to a local Frostbite server instead, bypass the marketplace and add a project-scoped MCP server:

```sh
claude mcp add --scope project --transport http frostbite http://localhost/mcp
```
