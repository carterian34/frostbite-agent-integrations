# Frostbite for Gemini CLI

Merge `gemini.settings.json` into either `~/.gemini/settings.json` or a project's `.gemini/settings.json`.

For local development, Gemini CLI can add the server with:

```bash
gemini mcp add --transport http frostbite http://localhost/mcp
```

For public distribution, replace the local URL with Frostbite's public HTTPS MCP endpoint. Gemini CLI supports OAuth discovery for remote MCP servers, but Frostbite's OAuth authorization response must include the issuer (`iss`) parameter expected by Gemini before this package can complete OAuth sign-in.
