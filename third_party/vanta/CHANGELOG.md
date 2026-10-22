# Changelog

All notable changes to this plugin will be documented here.

## 1.0.0 — initial release

- Added the `vanta` MCP server pointing at Vanta's hosted Streamable HTTP endpoint for US instances (`https://mcp.vanta.com/mcp`), with `"placement": "server"` so Grok Bot connects through Cursor's hosted path.
- Auth uses MCP OAuth with Vanta account login, Dynamic Client Registration, and PKCE — no API token, client secret, or custom header to configure.
- Logo: the "V" glyph from Vanta's official wordmark, from `https://cdn.prod.website-files.com/64009032676f24f376f002fc/6400ac82429afb0f7b31fa6c_vanta-logo.svg` (Vanta Inc.).
