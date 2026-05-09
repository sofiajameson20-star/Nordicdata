# Nordic Data MCP Server

> Live Nordic public-sector and Norwegian corporate data, exposed as 28 MCP tools for AI agents.

**Hosted at:** `https://api.nordicdata.cloud/mcp`
**Get a free API key:** [nordicdata.cloud](https://nordicdata.cloud)
**Docs:** [nordicdata.cloud/docs#mcp](https://nordicdata.cloud/docs#mcp)

This repository contains setup instructions and configuration snippets. The server itself is hosted — no local install required.

---

## What's covered

- **Public procurement** (TED) for Norway, Sweden, Denmark, Finland, Iceland — notices and contract awards
- **Norwegian company registry** (Brønnøysund) — full registry with contact info, accounts, shareholders, change history
- **Officer & ownership network** — board memberships, shortest-path queries, full role history
- **News** — Norwegian-language news mentioning a company
- **EU R&D** — Horizon Europe grants (Cordis)
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

Restart Claude Desktop. The tools appear in the MCP picker.

### Cursor

Edit `~/.cursor/mcp.json` with the same JSON.

### Any MCP-aware client

```
URL:       https://api.nordicdata.cloud/mcp
Header:    X-API-Key: <your key>
Transport: Streamable HTTP
```

## Tools

### Procurement (TED)
- `search_tenders` — Search procurement notices by country, keyword, CPV code, date
- `get_tender` — Full details for a single tender
- `search_awards` — Search contract awards (who won what)
- `get_tender_leaderboard` — Top public-sector buyers in a Nordic country
- `get_company_contract_wins` — Public-sector contracts won by a Norwegian company

### Norwegian company registry
- `search_companies` — Search by name, industry, location
- `get_company` — Full registry record
- `get_company_contact` — Public email + phone
- `get_company_narrative` — AI-generated executive summary
- `get_company_peers` — Peer-cohort benchmarks
- `get_company_snapshot` — One-call snapshot across every data source
- `get_company_changes` — Registry change history
- `get_company_subsidiaries` — Subsidiaries registered under this orgnr
- `bulk_get_companies` — Enrich a list of companies in one call

### Financials & ownership
- `get_company_accounts` — Annual accounts (revenue, profit, equity)
- `get_company_shareholders` — Shareholders (Aksjonærregisteret)
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
- `search_eu_grants` — Search Horizon Europe grants (Cordis)
- `get_company_eu_grants` — Norwegian company's Horizon Europe participations

### Tech intelligence
- `find_companies_using_tech` — Norwegian companies using a specific technology

### Compliance
- `screen_for_sanctions` — Screen any name against international sanctions lists
- `check_company_sanctions` — Sanctions screening for a Norwegian company + its officers

## Example prompts

- *"Which Norwegian municipalities tendered snow-clearing contracts over 5M NOK in 2026?"*
- *"Pull the latest accounts and shareholders for orgnr 923609016."*
- *"Find Norwegian companies using Snowflake."*
- *"Who sits on the boards of all three of these companies?"*
- *"Screen this list of suppliers against sanctions lists."*
- *"Show me Horizon Europe grants won by Norwegian SMBs in clean energy."*

## Pricing

- **Free** — 5,000 requests/month, no card required
- **Paid plans** from €29/mo

See [nordicdata.cloud](https://nordicdata.cloud).

## Support

- Email: [hello@nordicdata.cloud](mailto:hello@nordicdata.cloud)
- Docs: [nordicdata.cloud/docs](https://nordicdata.cloud/docs)
