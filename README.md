# Reecopedia MCP Server

**Free regulatory search engine for EU textile sustainability law, exposed as a remote [MCP](https://modelcontextprotocol.io) server.** No API key, no account, no installation — connect any MCP client to:

```
https://ia.reeco.eco/mcp
```

Published in the official MCP Registry as [`eco.reeco/reecopedia`](https://registry.modelcontextprotocol.io/v0.1/servers?search=reecopedia) (domain-verified). Interactive web version: [ia.reeco.eco/reecopedia](https://ia.reeco.eco/reecopedia).

## What it covers

Reecopedia answers questions from a curated corpus of EU textile sustainability law and official preparatory studies:

- **ESPR** — Ecodesign for Sustainable Products Regulation (EU) 2024/1781
- **Digital Product Passport (DPP)** for textiles
- **CSRD** — Corporate Sustainability Reporting Directive
- **CBAM** — Carbon Border Adjustment Mechanism
- **EU ETS** — Emissions Trading System
- **CWA 18291** — CEN Workshop Agreement (CIRPASS-2)
- **JRC preparatory studies** for textile ecodesign

Every answer is grounded in retrieved passages with source citations (document, page). Retrieval only — your AI client writes the answer; no LLM runs on Reecopedia's side.

## Tools

| Tool | Purpose |
|---|---|
| `search_eu_textile_regulations` | Main search over the regulatory corpus, returns cited passages |
| `search` / `fetch` | Same corpus in the deep-research format (search by query, fetch full document page by id) |
| `about_reecopedia` | What Reecopedia is, who runs it, privacy policy |

## Connect

**Claude (claude.ai / Desktop)** — Settings → Connectors → *Add custom connector* → URL `https://ia.reeco.eco/mcp`

**Claude Code**

```bash
claude mcp add --transport http reecopedia https://ia.reeco.eco/mcp
```

**ChatGPT (developer mode)** — Settings → Connectors → *Add custom connector* → URL `https://ia.reeco.eco/mcp`, no authentication.

**Cursor** — add to `.cursor/mcp.json` in the project, or `~/.cursor/mcp.json` for every workspace:

```json
{
  "mcpServers": {
    "reecopedia": {
      "url": "https://ia.reeco.eco/mcp"
    }
  }
}
```

**VS Code (GitHub Copilot)** — add to `.vscode/mcp.json` in the workspace, or run *MCP: Open User Configuration*:

```json
{
  "servers": {
    "reecopedia": {
      "type": "http",
      "url": "https://ia.reeco.eco/mcp"
    }
  }
}
```

**Gemini CLI** — install as an extension, one command:

```bash
gemini extensions install https://github.com/halleluiaman-ux/reecopedia-mcp
```

Or add it by hand to `~/.gemini/settings.json` (`httpUrl` selects the streamable HTTP transport):

```json
{
  "mcpServers": {
    "reecopedia": {
      "httpUrl": "https://ia.reeco.eco/mcp"
    }
  }
}
```

**Any other MCP client** — add a remote MCP server with transport `streamable-http` and URL `https://ia.reeco.eco/mcp`. Generic JSON config:

```json
{
  "mcpServers": {
    "reecopedia": {
      "type": "streamable-http",
      "url": "https://ia.reeco.eco/mcp"
    }
  }
}
```

## Privacy

The server receives only your query text — no account, no login, no personal data. Queries are stored without any personal identifier (no IP, no user id, no session) to improve retrieval quality, retained at most 90 days, then deleted. Full policy: [ia.reeco.eco/reecopedia/privacy](https://ia.reeco.eco/reecopedia/privacy).

## Who runs it

Built by [Stefano Cipriani](https://reeco.eco), founder of **Reeco®** — algorithmic verification layer for textile supply-chain compliance (Digital Product Passport, mass-balance reconciliation). Expert Member of CIRPASS-2 (EWG1, EWG3), JRC Registered Stakeholder.


## Cursor plugin

This repository is also a Cursor marketplace repository. The plugin under
[`plugins/reecopedia`](plugins/reecopedia) adds the same remote server to Cursor;
the marketplace manifest is [`.cursor-plugin/marketplace.json`](.cursor-plugin/marketplace.json).

## About this repository

This repository documents the public Reecopedia MCP endpoint (`server.json` mirrors the official MCP Registry entry). The retrieval engine and corpus are not open source.
