# mobile.de Scraper

Extract structured data from [mobile.de](https://mobile.de) — structured car listings from mobile.de — Germany's largest car marketplace.

**[Run on Apify →](https://apify.com/blackfalcondata/mobile-de-scraper)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, and multiple filters. Smart input resolution ensures you always get results.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control output size.

📊 **Structured data**

Clean JSON output with consistent field naming. All fields always present — null when unavailable, never omitted.

---

## Use cases

<!-- WRITE: 4-6 use case paragraphs. Bold the title. 2-3 sentences each. -->

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured data on a schedule. Export to CSV, JSON, or directly to your database.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

---

## Quick start

```json
{
  "query": "volkswagen golf",
  "maxResults": 50
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Free-text search keywords (e.g. 'VW Golf GTI'). Use JSON array for multi-query. |
| `make` | string | — | Car make / brand (e.g. 'Volkswagen', 'BMW', 'Mercedes-Benz'). |
| `model` | string | — | Car model (e.g. 'Golf', '3er', 'C-Klasse'). Requires make. |
| `startUrls` | array | — | Direct mobile.de search URLs. Use this for full filter control. |
| `maxResults` | integer | `50` | Maximum total listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum search result pages to scrape per source. |
| `condition` | enum | — | Filter by vehicle condition. |
| `fuelType` | enum | — | Filter by fuel type. |
| `transmission` | enum | — | Filter by transmission type. |
| `bodyType` | enum | — | Filter by body type / vehicle category. |
| `sellerType` | enum | — | Filter by seller type. |
| `priceMin` | integer | — | Minimum price in EUR. |
| `priceMax` | integer | — | Maximum price in EUR. |
| `mileageMin` | integer | — | Minimum mileage in km. |
| `mileageMax` | integer | — | Maximum mileage in km. |
| `yearMin` | integer | — | Minimum first registration year. |
| `yearMax` | integer | — | Maximum first registration year. |
| `powerMin` | integer | — | Minimum engine power in PS. |
| `powerMax` | integer | — | Maximum engine power in PS. |
| `zipCode` | string | — | German postal code for location-based search. |
| `radiusKm` | integer | — | Search radius around ZIP code. |
| `sort` | enum | `"relevance"` | Sort Order. |
| `compact` | boolean | `false` | Output only core fields (for AI-agent/MCP workflows). |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape mobile.de?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |

---

*Last updated: 2026 03*
