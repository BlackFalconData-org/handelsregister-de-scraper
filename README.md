# Handelsregister Germany Scraper [Just 💰$0.9]

Extract structured data from [handelsregister.de](https://handelsregister.de) — Search the German commercial register (handelsregister.de) by company name, city or register number. Each record has legal form, registered address, share capital and directors. Ready to import into a CRM or a spreadsheet for KYC checks.

**[Handelsregister Germany Scraper [Just 💰$0.9] on Apify →](https://apify.com/blackfalcondata/handelsregister-de-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 📝 description format, and more.

**Detail enrichment** — Fetch structured metadata for each record.

**Incremental mode** — Only get new or changed records since your last run. Content hash per record — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how records evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Result cap** — Stop after N records (up to 100). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every record returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured records from handelsregister.de on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor records, track trends, and analyze market dynamics with structured, deduplicated data from handelsregister.de.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per record is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "Bäckerei",
  "maxResults": 100,
  "includeDetails": true,
  "compact": false,
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "emitUnchanged": false,
  "emitExpired": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5,
  "descriptionFormat": "all"
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Company name or keyword to search the register for (e.g. "Bäckerei", "Siemens AG"). Use a JSON array for several searches, e.g. ["Bäckerei","Kaffeerösterei"]. |
| `location` | string | — | Optional. Restrict results to companies with this registered seat (city), e.g. "Hannover". Use a JSON array for several cities. |
| `maxResults` | integer | `100` | Maximum total records (0 = everything the register returns). The register itself shows at most 100 hits per search — narrow the keyword or add a seat for bigger universes. |
| `includeDetails` | boolean | `true` | Fetch the structured register content per company (legal form, address, business purpose, share capital, officers, register entries). Turn off for name/court/seat only. |
| `includeDeleted` | boolean | `false` | Also return companies whose register entry has been deleted (gelöscht) — useful for due diligence and history research. |
| `includeRawXml` | boolean | `false` | Attach the raw structured register document (XJustiz XML) to each record as `raw_xml` — large, increases dataset size. Needs Include Full Register Details. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, seats) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `skipReposts` | boolean | `false` | When incremental, skip records whose content matches an expired record from a prior run (cross-run duplicate detection). |
| `emitUnchanged` | boolean | `false` | When incremental mode is on, also emit records whose content has not changed since the last run. |
| `emitExpired` | boolean | `false` | When incremental mode is on, also emit records that were seen before but are no longer found. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED records. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of records included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |
| `descriptionFormat` | enum | `"all"` | Choose which representation of the listing description to include. `all` keeps every variant; the others keep only the selected one. |
| `startUrls` | array | — | One or more links that name a register entry, for example from a company-profile page. The link must contain the court, register type and number (such as Amtsgericht Hannover HRB 12345). When set, other search filters are ignored. |

---

## Output fields

Every record returns the same 46-field schema. Missing values are `null` — never omitted.

- `query`
- `found`
- `sourceUrl`
- `scrapedAt`
- `company_name`
- `registry_court`
- `registry_court_code`
- `register_type`
- `hr_number`
- `register_id`
- `state`
- `registered_seat`
- `status`
- `legal_form`
- `registered_address`
- `address_street`
- `address_house_number`
- `address_postal_code`
- `address_city`
- `business_purpose`
- `share_capital_eur`
- `share_capital_text`
- `representation_rule`
- `managing_directors`
- `board_members`
- `supervisory_board`
- `prokura_holders`
- `officers`
- `branches`
- `incorporation_date`
- `articles_date`
- `last_change_date`
- `entry_count`
- `register_entries`
- `previous_names`
- `available_documents`
- `search_result_url`
- `portalUrl`
- `scraped_at`
- `listingId`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per record. Here is a real example from a production run:

```json
{
  "query": "Bäckerei",
  "found": true,
  "sourceUrl": "https://www.handelsregister.de/rp_web/sucheErgebnisse/welcome.xhtml",
  "scrapedAt": "2026-10-14T13:37:04.736Z",
  "company_name": "\"... em Tetz Backes\" Bäckerei und Konditorei GmbH",
  "registry_court": "Amtsgericht Mönchengladbach",
  "registry_court_code": "R1504",
  "register_type": "HRB",
  "hr_number": "4934",
  "register_id": "Amtsgericht Mönchengladbach HRB 4934",
  "state": "Nordrhein-Westfalen",
  "registered_seat": "Mönchengladbach"
}
```

*Truncated — full records contain 46 fields. See Output fields for the complete schema.*

**[Try Handelsregister Germany Scraper [Just 💰$0.9] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/handelsregister-de-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.0009 |

See the [actor on Apify](https://apify.com/blackfalcondata/handelsregister-de-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape handelsregister.de?**
Use this actor on Apify to extract structured data from handelsregister.de. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get handelsregister.de data as JSON, CSV, or Excel?**
The actor writes each record to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape handelsregister.de?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check handelsregister.de's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each record gets a content hash. On subsequent runs, only new or changed records are emitted — saving time, compute, and storage. Expired records can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Handelsregister Germany Scraper [Just 💰$0.9]](https://apify.com/blackfalcondata/handelsregister-de-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
