# ScanForAI MCP server

ScanForAI checks a text for signs of AI writing and explains what it found, in plain words. This is its MCP server:
any MCP-capable assistant (Claude Code, Claude Desktop, Cursor, and others) can call it directly.

A score is a signal, never a verdict. Scores estimate how strongly a text shows measurable machine-writing patterns
and can be wrong in both directions. Never use a score alone to accuse a person.

## Add it

1. Create a free account at https://app.scanforai.com/register?src=mcp and make an API key on the API keys page
   (it starts with `at_sk_`).
2. Add the server:

   ```
   claude mcp add --transport http scanforai https://api.scanforai.com/api/mcp \
       --header "Authorization: Bearer at_sk_..."
   ```

   Other clients: add the same URL as a remote (streamable HTTP) MCP server and set the `Authorization` header to
   `Bearer at_sk_...` wherever the client configures headers.

Texts you scan through your key are saved to your ScanForAI history, like any API scan, and you can delete your account
at any time.

## Tools

| tool | what it does |
|---|---|
| `scan_text` | Scores a text 0-100 for signs of AI/machine writing, with the band (low, moderate, elevated, high) and plain-English reasons. `deep: true` asks for the most thorough read (slower, quota-limited). `lang` chooses the language the reasons are written in (for example `es`). Texts in a language the scanner cannot read yet get no score, and the answer says so. |
| `cleanup_text` | Strips machine typography from a text without rewriting a word: smart quotes, em dashes and the rare glyphs AI models overuse become plain keyboard characters. |

Every call counts against your plan like a call to the REST API. A new account has a smaller deep-read quota until its email is verified and its first month has passed.

## Where things are

- Documentation: https://scanforai.com/mcp
- Web app and API keys: https://app.scanforai.com
- Endpoint: `https://api.scanforai.com/api/mcp` (MCP streamable HTTP, protocol revision 2025-03-26)

This repository holds the registry listing (`server.json`) and this page. The server itself is part of the ScanForAI
service and is not open source.
