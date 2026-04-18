# mobile.de Scraper

Extract structured car listing data from [mobile.de](https://www.mobile.de) — Germany's largest used car marketplace with 1.4 million+ vehicles from dealers and private sellers.

**[mobile.de Car Scraper - Germany’s Largest Car Marketplace on Apify →](https://apify.com/blackfalcondata/mobile-de-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by condition, fuel type, transmission, and more.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from mobile.de on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from mobile.de.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "volkswagen golf",
  "maxResults": 50
}
```

```json
{
  "make": "BMW",
  "fuelType": "DIESEL",
  "priceMax": 25000,
  "yearMin": 2020,
  "maxResults": 100
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Free-text search (e.g. "VW Golf GTI"). |
| `make` | string | — | Car make (e.g. "Volkswagen", "BMW"). |
| `model` | string | — | Car model (e.g. "Golf", "3er"). Requires make. |
| `startUrls` | array | — | Direct mobile.de search URLs for full filter control. |
| `maxResults` | integer | `50` | Maximum listings to return (0 = unlimited). |
| `maxPages` | integer | `5` | Maximum search pages. Each page returns ~26 listings. |
| `condition` | enum | — | NEW, USED, EMPLOYEE_CAR, PRE_REGISTRATION, CLASSIC |
| `fuelType` | enum | — | DIESEL, PETROL, ELECTRIC, HYBRID, PLUG_IN_HYBRID, CNG, LPG, HYDROGEN |
| `transmission` | enum | — | MANUAL_GEAR, AUTOMATIC_GEAR, SEMI_AUTOMATIC_GEAR |
| `bodyType` | enum | — | LIMOUSINE, KOMBI, KLEINWAGEN, COUPE, CABRIO, SUV, GELAENDEWAGEN, VAN, PICKUP |
| `sellerType` | enum | — | DEALER, PRIVATE |
| `priceMin` / `priceMax` | integer | — | Price range in EUR |
| `mileageMin` / `mileageMax` | integer | — | Mileage range in km |
| `yearMin` / `yearMax` | integer | — | First registration year range |
| `powerMin` / `powerMax` | integer | — | Engine power range in PS |
| `zipCode` | string | — | German postal code for location search |
| `radiusKm` | integer | — | Radius around ZIP code (km) |
| `sort` | enum | `"relevance"` | relevance, price_asc, price_desc, mileage_asc, registration_desc, registration_asc |
| `compact` | boolean | `false` | Core fields only for AI/MCP workflows. |

---

## FAQ

**What data does it return?**
29 fields per listing: price, specs (make, model, fuel, power, mileage, registration), seller info (name, type, rating, review count, location), price rating, 1–5 thumbnail images, and metadata.

**Does it include full images and descriptions?**
Each listing includes 1–5 thumbnail images from search results. Full-resolution galleries and descriptions from detail pages are not included in this version.

**How fast does it run?**
A typical run with 50 results completes in 10–15 seconds. Each search page takes 3–5 seconds and returns ~26 listings.

**Is it legal to scrape mobile.de?**
This actor accesses publicly available listing data. Review mobile.de's terms of service and your local regulations before using the data commercially.

---

## Known limitations

- Data comes from search result pages only. Full descriptions, equipment lists, and full-resolution images are not included in v1.
- `transmission` and `bodyType` work as search filters but are not returned in the output — mobile.de does not display them on search result cards.
- `condition` is only populated when mobile.de explicitly marks the listing (e.g. "Unfallfrei", "Vorführfahrzeug").
- `sellerRating` requires enough review history — private sellers and small dealers may not have a rating.
- Images are search result thumbnails, not the full-resolution gallery from the detail page.


## Output fields

Every listing returns the same 29-field schema. Missing values are `null` — never omitted.

- `listingId`
- `listingKey`
- `canonicalUrl`
- `title`
- `make`
- `model`
- `price`
- `priceCurrency`
- `priceType`
- `vatDeductible`
- `mileageKm`
- `firstRegistration`
- `fuelType`
- `powerKw`
- `powerPs`
- `condition`
- `priceRating`
- `sellerName`
- `sellerType`
- `sellerRating`
- `sellerReviewCount`
- `location`
- `imageUrls`
- `numImages`
- `sourceUrl`
- `searchQuery`
- `searchUrl`
- `isSponsored`
- `scrapedAt`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "listingId": "7a358277a4357caa4233978183ddb9ae0a1ae164a14d260fcf531c3dc19b875f",
  "listingKey": "444927632",
  "canonicalUrl": "https://suchen.mobile.de/fahrzeuge/details.html?id=444927632",
  "title": "Volkswagen GolfVIII GTI Clubsport 2.0 TSI Performance IQ-L",
  "make": "Volkswagen",
  "model": "GolfVIII",
  "price": 43933,
  "priceCurrency": "EUR",
  "priceType": "FIXED",
  "vatDeductible": true,
  "mileageKm": 13614,
  "firstRegistration": "09/2024"
}
```

*Truncated — full records contain 29 fields. See Output fields for the complete schema.*


**[Try mobile.de Car Scraper - Germany’s Largest Car Marketplace now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/mobile-de-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.005 |
| Result | $0.001 |

See the [actor on Apify](https://apify.com/blackfalcondata/mobile-de-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [Bilbasen Scraper](https://apify.com/blackfalcondata/bilbasen-scraper?fpr=1h3gvi) — Denmark's largest car marketplace
- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026-03*
