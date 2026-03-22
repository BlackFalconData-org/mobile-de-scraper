# mobile.de Scraper

Extract structured car listing data from [mobile.de](https://www.mobile.de) — Germany's largest used car marketplace with 1.4 million+ vehicles from dealers and private sellers.

**[Run on Apify →](https://apify.com/blackfalcondata/mobile-de-scraper)**

---

## Key features

🔍 **Structured search filters**

Search by make, model, fuel type, price range, mileage, year, power, body type, seller type, ZIP code with radius, and sort order. No manual URL construction needed.

💰 **Price intelligence**

Every listing includes mobile.de's own price assessment (Guter Preis, Fairer Preis, Sehr guter Preis) plus seller star ratings and review counts.

🖼️ **Multiple images**

1–5 thumbnail image URLs per listing from the search results.

⚡ **AI-agent ready**

Compact output mode returns 13 core fields for MCP tools, LLM pipelines, and agent workflows.

---

## Use cases

**Price monitoring and market intelligence**
Track asking prices across makes, models, regions, and fuel types. The built-in price rating tells you where each listing sits relative to the market without building your own pricing model.

**Dealer inventory aggregation**
Build a unified view of dealer stock across Germany. Filter by ZIP code and radius, sort by price or registration date, and feed structured records into dashboards on a recurring schedule.

**Lead generation for automotive services**
Identify active dealers by region with high listing volume and strong ratings. Use seller name, rating, review count, and location to build qualified prospect lists.

**Recurring data pipelines**
Schedule daily or weekly runs and export to CSV, JSON, or push to a warehouse. The 29-field schema is stable across runs — downstream consumers don't need per-run cleanup logic.

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

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |
| [DBA Marketplace Scraper](https://github.com/BlackFalconData-org/dba-listings-scraper) | Denmark's largest classifieds platform |
| [FINN.no Torget Scraper](https://github.com/BlackFalconData-org/finn-torget-scraper) | Norway's largest classifieds marketplace |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |

---

*Last updated: 2026-03*
