# Nordic Data MCP Server

> Live Nordic company and public-sector data, exposed as 28 MCP tools for AI agents.

**Hosted at:** `https://api.nordicdata.cloud/mcp`
**Get a free API key:** [nordicdata.cloud](https://nordicdata.cloud)
**Docs:** [nordicdata.cloud/docs#mcp](https://nordicdata.cloud/docs#mcp)
**Smithery one-click install:** [smithery.ai/server/sofia-jameson-20/Nordic-Data](https://smithery.ai/server/sofia-jameson-20/Nordic-Data)

This repository contains setup instructions and configuration snippets. The server itself is hosted — no local install required.

---

## What's covered

- **Public procurement** — Nordic + EU-wide contract filings, including below-EU-threshold Norwegian municipal/county tenders that no other API exposes cleanly
- **Norwegian company registry** — live registry data + full shareholder cap tables
- **Officer & ownership network** — board memberships, shortest-path queries, full role history
- **News** — Norwegian-language news mentioning a company
- **EU R&D** — grant participations, joined to Norwegian recipients
- **Tech intelligence** — find companies using a specific technology
- **Compliance** — sanctions screening for any name or company + officers
- **AI summaries** — executive narratives and peer benchmarks per company

## Setup

### Claude Desktop

Edit `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "nordic-data": {
      "url": "https://api.nordicdata.cloud/mcp",
      "headers": {
        "X-API-Key": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

Restart Claude Desktop. The 28 tools appear in the MCP picker.

### Cursor

Edit `~/.cursor/mcp.json` with the same JSON.

### Any MCP-aware client

```
URL:       https://api.nordicdata.cloud/mcp
Header:    X-API-Key: <your key>
Transport: Streamable HTTP
```

## Tools (28 total)

### Procurement
- `search_tenders` — Nordic procurement notices by country, keyword, CPV, date. Filter by `source` (EU-wide vs Norway-with-below-threshold) or `buyer_orgnr`.
- `get_tender` — Full tender details by ID
- `search_awards` — Search contract awards (who won what)
- `get_tender_leaderboard` — Top public-sector buyers in a Nordic country
- `get_company_contract_wins` — Public-sector contracts won by a Norwegian company

### Norwegian company registry
- `search_companies` — Search by name, industry, location
- `get_company` — Full registry record
- `get_company_contact` — Public email + phone (with MX-verified email candidates)
- `get_company_narrative` — AI-generated executive summary
- `get_company_peers` — Peer-cohort benchmarks
- `get_company_snapshot` — One-call snapshot across every data layer
- `get_company_changes` — Registry change history
- `get_company_subsidiaries` — Subsidiaries registered under this orgnr
- `bulk_get_companies` — Enrich a list of up to 100 companies in one call

### Financials & ownership
- `get_company_accounts` — Annual accounts (revenue, profit, equity)
- `get_company_shareholders` — Shareholder cap table — 3M+ positions across 396K companies
- `get_shareholder_portfolio` — All companies a person/entity owns shares in

### Officer & network graph
- `search_persons` — Search persons in the Norwegian officer network
- `get_person` — Full role history across Norwegian companies
- `find_company_path` — Shortest path between two companies through shared officers
- `get_person_network` — Find who is connected to a person via shared boards

### News
- `get_company_news` — Recent Norwegian-language news mentioning a company
- `search_news` — Search Norwegian news headlines

### EU R&D
- `search_eu_grants` — Search EU R&D grant participations
- `get_company_eu_grants` — Norwegian company's EU R&D grant participations

### Tech intelligence
- `find_companies_using_tech` — Norwegian companies using a specific technology

### Compliance
- `screen_for_sanctions` — Screen any name against international sanctions lists
- `check_company_sanctions` — Sanctions screening for a Norwegian company + its officers

## Example prompts

- *"Which Norwegian municipalities tendered snow-clearing contracts under 5M NOK with deadlines in the next 30 days?"* (uses below-threshold coverage)
- *"Pull the latest accounts and shareholders for orgnr 923609016."*
- *"Find Norwegian companies using Snowflake."*
- *"Who sits on the boards of all three of these companies?"*
- *"Screen this list of suppliers against sanctions lists."*
- *"Show me EU R&D grants won by Norwegian SMBs in clean energy."*

## Agent-native buying

Designed for autonomous agents — three endpoints let an agent (or its operator) discover plans, subscribe with a Stripe payment method, and change plans without a browser:

```bash
# Discover available plans
curl https://api.nordicdata.cloud/agent/plans

# Subscribe — agent supplies card token, gets working API key in response
curl -X POST https://api.nordicdata.cloud/agent/subscribe \
  -H "Content-Type: application/json" \
  -d '{"email":"agent@example.com","plan":"starter","payment_method":"pm_xxx","country":"NO"}'

# Upgrade later (using the API key)
curl -X POST https://api.nordicdata.cloud/agent/change-plan \
  -H "X-API-Key: nrd_live_..." \
  -H "Content-Type: application/json" \
  -d '{"plan":"pro"}'
```

See [docs#agent-quickstart](https://nordicdata.cloud/docs#agent-quickstart) for the full flow.

## Pricing

- **Free** — 5,000 requests/month, no card required
- **Paid plans** from €29/mo

See [nordicdata.cloud](https://nordicdata.cloud).

## Support

- Email: [hello@nordicdata.cloud](mailto:hello@nordicdata.cloud)
- Docs: [nordicdata.cloud/docs](https://nordicdata.cloud/docs)
- LLM-friendly site index: [nordicdata.cloud/llms.txt](https://nordicdata.cloud/llms.txt)
- OpenAPI spec: [api.nordicdata.cloud/openapi.json](https://api.nordicdata.cloud/openapi.json)
