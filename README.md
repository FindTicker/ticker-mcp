# Ticker MCP

Ticket market data for ticket brokers, inside the AI you already use. Connect Claude, ChatGPT, Cursor, Perplexity or any MCP client, sign in with your Ticker account, and ask in plain words.

What your AI reads through it:

- Completed resale sales by section and row, on one event or ranked across the market.
- Primary seats taken by section and how that changed over time, with the seats each presale and the public on sale released.
- Seat history on the primary market: every change to each seat, one seat at a time or a whole section.
- Primary and resale on one event: each section's asking prices before and after fees, marketplace by marketplace, with face value beside them.
- Price and demand history for any event, and a screener across upcoming events.

## Server URL

```
https://api.findticker.com/mcp
```

Streamable HTTP. OAuth 2.1 with PKCE. No API key to create or store.

## Connect

**Claude** (any plan, Free included): Customize, Connectors, select +, find Ticker, Connect. In a chat, open + and Connectors and switch Ticker on. On Team and Enterprise an owner adds Ticker first.

**ChatGPT**: Plugins, select +, then Add custom MCP server. Name it Ticker, paste the server URL under Connection, choose OAuth, accept the warning, then Create as a plugin. Install it and sign in. In a new chat, type @ and pick Ticker. No Add custom MCP server in the menu? Turn on Developer mode in Settings first.

**Perplexity** (Pro, Max or Enterprise): Plugins or Customize, Connectors, Add custom, Add MCP connector, Remote. Name it Ticker and paste the server URL. Under Advanced, set Authentication to OAuth and Transport to Streamable HTTP, tick the box, then Add.

**Cursor** (`~/.cursor/mcp.json`, then restart Cursor):

```json
{ "mcpServers": { "ticker": { "url": "https://api.findticker.com/mcp" } } }
```

**Claude Code**:

```bash
claude mcp add --transport http ticker https://api.findticker.com/mcp
claude mcp login ticker
```

**Codex CLI**:

```bash
codex mcp add ticker --url https://api.findticker.com/mcp
codex mcp login ticker
```

**VS Code (Copilot)**:

```bash
code --add-mcp '{"name":"ticker","type":"http","url":"https://api.findticker.com/mcp"}'
```

**Gemini CLI**: `gemini mcp add --transport http ticker https://api.findticker.com/mcp`, restart it, then run `/mcp auth ticker`.

**Any other client**: point it at the server URL. It follows the OAuth flow on first use.

## Sign in

Your client registers itself (Dynamic Client Registration or a Client ID Metadata Document) and opens findticker.com, where you sign in and approve access. The token is Ticker's own, short-lived, and refreshes itself. Revoke it from your client or from your Ticker account settings.

A free account connects with a tool-call allowance. Paid plans raise it and open more markets: [findticker.com/plans](https://findticker.com/plans).

## Tools

| Tool | What it answers |
| --- | --- |
| `screen_events` | Upcoming events filtered and ranked by price, price change, listings, primary seats left, demand, sales, date and place |
| `list_screen_columns` | The columns and preset screens a screen can use |
| `search_events` | Events by name, performer, venue or date, with their ids |
| `get_event_analytics` | Every number Ticker holds for one event, now or on past dates |
| `get_event_bundle` | One event's headline numbers, price history and top sections in one call |
| `get_event_chart` | An event's price or demand history as a series, with a chart image |
| `get_event_sections` | Section prices and listings for one event, before and after fees, now and over the last 7 days |
| `get_event_sections_live` | Open seats per section on the primary market, now or at a past moment, with prices and capacity |
| `get_event_seats` | Single seats on the primary market's seat map: open now or at a past moment, each seat's history, and what each sale window released |
| `get_event_sellers` | Seller concentration on one event, shown anonymously |
| `get_sales` | Completed resale sales and primary seats taken, for one event, performer or venue, or ranked across the market |
| `get_performer_analytics` | A performer's numbers and history across their shows |
| `get_venue_schedule` | A venue's upcoming events with sale dates and the lowest price |
| `research_event` | Recent dated news coverage of an event and its performers |
| `search_docs` | The parts of Ticker's docs that answer a question, each with its page and heading |
| `watch_event`, `unwatch_event`, `list_watchlist` | Star an event and set its alerts, stop watching, list what you watch |
| `create_view`, `update_view`, `delete_view`, `list_views` | Views: saved screens that alert you when an event enters |
| `get_view_alert_preview`, `list_matches` | What a View would send, and the events that entered it |
| `list_destinations` | Your alert destinations, such as Slack and Discord |
| `get_account` | Your plan, quotas and what is used |

Parameters for every tool: [findticker.com/docs/tools](https://findticker.com/docs/tools).

## Five prompts brokers use

1. Which events had the most primary seats taken in the last 24 hours?
2. Show completed sales in section 104 of this event this week, with row and listed price.
3. What is the lowest asking price after fees in each section of this event, marketplace by marketplace?
4. How many seats are open in each section on the primary market, and which sections lost the most since Monday?
5. Show every change to seat 12 in row F of section 104 at this event.

## Docs and support

Setup guides and limits: [findticker.com/docs/mcp](https://findticker.com/docs/mcp). Questions or a security report: support@findticker.com.

## License

This repository holds documentation only. Its text is under the MIT License (see `LICENSE`). The Ticker service and its data are covered by the [Ticker terms](https://findticker.com/terms).
