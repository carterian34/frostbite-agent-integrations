# Frostbite for Claude Code

Claude Code connects directly to Frostbite's remote streamable-HTTP MCP server; it does not install the Codex plugin package.

For local development, add the server with Claude Code's MCP command using `http://localhost/mcp`. For distribution, replace that address with Frostbite's public HTTPS MCP endpoint and complete the OAuth sign-in requested by Claude Code.

This package intentionally contains client documentation rather than a Codex-style plugin manifest, because Claude Code manages MCP connections through its own configuration and `claude mcp` workflow.
