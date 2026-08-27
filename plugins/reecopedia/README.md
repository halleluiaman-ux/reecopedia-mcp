# Reecopedia

Cited search over EU product and sustainability law, inside Cursor.

The plugin connects Cursor to the public Reecopedia MCP server at
`https://ia.reeco.eco/mcp` (streamable HTTP, MCP protocol 2025-06-18).
No authentication, no API key, no account: the server is public and read-only.

## Corpus

- ESPR — Ecodesign for Sustainable Products Regulation (EU) 2024/1781
- Digital Product Passport (DPP)
- CSRD, CBAM, EU ETS
- CEN CWA 18291 (CIRPASS-2)
- JRC preparatory studies
- National transposition register cards

## Tools

Seven tools: `search_eu_textile_regulations`, `search`, `fetch`, `document_outline`,
`find_exact_text` and `about_reecopedia` are read-only over the corpus;
`report_answer_issue` sends a correction to the human curation queue. Every answer
cites the source file and page, so a claim can always be traced back to the
official text.

## Notes

The corpus is in English and retrieval matches the wording of the law, not the
phrasing of a question. Queries are therefore sent to the server in English and in
the legal register of the act, whatever language you are working in; the answer
comes back in your language. Article and annex numbers and act identifiers
(`Article 9`, `ESPR`, `2024/1781`) are matched as metadata and are kept verbatim.

- Website and how to connect: https://ia.reeco.eco/reecopedia
- Privacy policy: https://ia.reeco.eco/reecopedia/privacy
- Terms: https://ia.reeco.eco/reecopedia/terms
- MCP registry entry: `eco.reeco/reecopedia`

MIT licensed. Maintained by Stefano Cipriani Studio (Reeco).
