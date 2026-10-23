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
| `document_outline` | Table of contents of one document, to navigate a long act or standard |
| `list_corpus_documents` | List available corpus documents, optionally filtered by title |
| `find_exact_text` | Locate a literal string (e.g. an article number or defined term) inside one document |
| `report_answer_issue` | Flag a wrong or unsupported answer for correction |
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

Restart Gemini CLI after installation, then run `/extensions list` and `/mcp`
to check that `reecopedia` is loaded and connected. Try:

> Use Reecopedia to find Article 9 of Regulation (EU) 2024/1781. Fetch the
> relevant passage and cite its document title, reference and original URL.

The extension exposes seven source-reading tools. `report_answer_issue` is excluded
because it submits a report. Gemini CLI authentication is separate from the
Reecopedia server, which requires no account or key.

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

## Gemini API example

[examples/gemini_api.py](examples/gemini_api.py) connects Google’s Interactions
API to the same remote MCP endpoint using the official Python SDK. It requires
your own Gemini API key and a model available to your Google account. Google’s
API usage terms and charges apply separately from public Reecopedia access.

```bash
python3 -m venv .venv
.venv/bin/pip install -r examples/requirements.txt
# Set GEMINI_API_KEY securely in your environment.
.venv/bin/python examples/gemini_api.py --model YOUR_AVAILABLE_GEMINI_MODEL
```

The example uses a 300-second Google request timeout (configurable with
`--timeout-seconds`), low thinking, bounded output, no automatic retries, and restricts tools to source
reading, and exits unsuccessfully unless the response contains a matched MCP call
and result plus an answer. A plausible answer alone does not prove MCP use.
`--check` validates the request locally without a key or network call; it does
not verify Google access or a live integration.

API failures print a diagnostic JSON to stderr: HTTP status, structured API error
status/message when provided, and an explicit allowlist of response trace headers.
Request headers, URLs, cookies and arbitrary response bodies are excluded; the
active API key is redacted from the selected values. A client timeout can have
no HTTP status or response headers. Missing tracing headers remain absent.


Gemini CLI gallery discovery uses the GitHub topic `gemini-cli-extension` and
the root manifest. A valid repository does not guarantee gallery inclusion or
availability in Gemini web/mobile. See Google’s
[extension release guide](https://geminicli.com/docs/extensions/releasing/) and
[remote MCP API documentation](https://ai.google.dev/gemini-api/docs/function-calling).

### Verification on 23 October 2026

Gemini CLI 0.65.0 validated and loaded extension 1.0.1 and reported the public
MCP endpoint as Connected. A separate MCP client completed a public search and
fetched the returned Article 9(2) identifier successfully. The API example passed
thirteen local contract tests using google-genai 2.33.0 and a mocked HTTP transport.
A live plain streaming Google request returned `OK` after 161.4 seconds.
The remote MCP stream began a `reecopedia:find_exact_text` call and result, but
ended without a completed answer; non-streaming MCP requests timed out even at
300 seconds. **A completed Gemini API + MCP answer remains unverified.**
These checks do not certify answer quality or gallery inclusion.

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
