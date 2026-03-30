# mobile.de Scraper

Extract structured car listing data from [mobile.de](https://www.mobile.de) — Germany's largest used car marketplace with 1.4 million+ vehicles from dealers and private sellers.

**[mobile.de Scraper on Apify →](https://apify.com/blackfalcondata/mobile-de-scraper)**

---

## Key features



**Search with filters** — Search by keyword and location. Filter by condition, fuel type, transmission, and more.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Structured data** — 30 fields per listing. Clean JSON output with consistent field naming. All fields always present — null when unavailable, never omitted.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from mobile.de on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from mobile.de.

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



- [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) — Denmark's largest car marketplace
- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data

---

*Last updated: 2026-03*
