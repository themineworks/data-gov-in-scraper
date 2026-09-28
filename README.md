# data.gov.in API Scraper: India Trade, Mandi Prices, Census

Pull any Indian government open dataset from data.gov.in via the official OGD API: foreign trade, mandi prices, census data, and thousands more. Filter, paginate, and receive clean structured JSON. No API key required.

**Run it on Apify:** [apify.com/themineworks/india-data-gov-scraper](https://apify.com/themineworks/india-data-gov-scraper)
**Docs, FAQ and pricing:** [themineworks.com/actors/india-data-gov-scraper](https://themineworks.com/actors/india-data-gov-scraper/)

**Price:** From $1.00 per 1,000 records on Apify's higher plans ($2.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged.

## What it returns

* Access thousands of Indian government datasets
* Foreign trade, mandi prices, census, and more
* Official OGD API. Authoritative source
* Filter, sort, and paginate any dataset
* Empty results are never charged

## Quick start

You need a free [Apify account](https://console.apify.com/sign-up) and its API token (Settings, API & Integrations).

### Python

```bash
pip install apify-client
```

```python
from apify_client import ApifyClient

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("themineworks/india-data-gov-scraper").call(run_input={
    "resourceId": "9ef84268-d588-465a-a308-a864a43d0070",
    "filters": [
        "state=Maharashtra",
        "commodity=Onion"
    ],
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

### Node.js

```bash
npm install apify-client
```

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_APIFY_TOKEN' });
const run = await client.actor('themineworks/india-data-gov-scraper').call({
    "resourceId": "9ef84268-d588-465a-a308-a864a43d0070",
    "filters": [
        "state=Maharashtra",
        "commodity=Onion"
    ],
    "maxResults": 50
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

### cURL

One request that runs the actor and returns the results in the response (for runs under 5 minutes):

```bash
curl -X POST "https://api.apify.com/v2/acts/themineworks~india-data-gov-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"resourceId": "9ef84268-d588-465a-a308-a864a43d0070", "filters": ["state=Maharashtra", "commodity=Onion"], "maxResults": 50}'
```

### Command line

This repo includes ready-made clients that save results to JSON and CSV:

```bash
python3 data_gov_in_scraper.py --token YOUR_APIFY_TOKEN --resource-id "9ef84268-d588-465a-a308-a864a43d0070" --filters "state=Maharashtra,commodity=Onion" --max-results "50"
node data_gov_in_scraper.mjs --token YOUR_APIFY_TOKEN --resource-id "9ef84268-d588-465a-a308-a864a43d0070" --filters "state=Maharashtra,commodity=Onion" --max-results "50"
```

## Input

| Field | Type | Default | Description |
|---|---|---|---|
| `resourceId` (required) | string |  | The data.gov.in dataset resource ID |
| `filters` | array |  | Optional filters as field=value strings, matching the dataset's fields (for example state=Maharashtra… |
| `maxResults` | integer | `1000` | Maximum number of records to return |

## Output

One row per result, as JSON, CSV, Excel or through the API.

| Field | Type | Description |
|---|---|---|
| `_resource_id` | string | data.gov.in resource ID of the dataset being scraped |
| `_scraped_at` | string | ISO timestamp when this record was scraped |

## Use it from an AI agent

The actor works as a tool in Claude, Cursor or any MCP client through Apify's MCP server:

```
https://mcp.apify.com/?tools=themineworks/india-data-gov-scraper
```

## FAQ

### What is data.gov.in?

data.gov.in is India's official government open data portal. It hosts 10,000+ datasets from central and state ministries covering agriculture, economy, environment, health, transport, and demographics.

### Do I need authentication to access data.gov.in?

The OGD Platform API requires a free API key. Registration is open and free at data.gov.in. The scraper handles the key-based authentication automatically.

### What are the most valuable datasets?

APMC mandi prices (daily commodity prices across mandis), foreign trade data (DGFT), PM Kisan beneficiary data, MSME registration data, and state-level COVID statistics are among the most-pulled datasets.

### Why is the data.gov.in API difficult to use directly?

Each dataset uses inconsistent field names, some older datasets ignore the format parameter and return CSV regardless, pagination has off-by-one errors on the last page, and filter key names are case-sensitive.

### What format does the scraper return data in?

Normalized JSON with consistent field names, UTF-8 encoding, and pagination already handled. Each record includes the source dataset ID and resource ID for traceability.

### How much does the data.gov.in API Scraper cost?

From $1.00 per 1,000 records on Apify's higher plans ($2.00 on the free plan), plus a $0.005 start fee per run. Failed and empty results are never charged. You can cap what a single run may spend with the maximum cost setting on Apify.

### Can I export the results to CSV or Excel?

Yes. Every run saves to an Apify dataset you can download as JSON, CSV, Excel or XML, or read through the API. The Python and Node clients in this repo also write the results to local files.

### Can I run it on a schedule?

Yes. Save your input as a task on Apify and attach a schedule, or call the API from your own cron job. Scheduled runs are billed the same way as manual ones.

## Related scrapers

* [CourtListener Scraper](https://themineworks.com/actors/courtlistener-court-records/): US court opinions, dockets, and case law as structured JSON
* [Socrata Open Data](https://themineworks.com/actors/socrata-open-data/): Any government data portal: CDC, HHS, NYC, Texas, and hundreds more
* [FDA 510(k) Scraper](https://themineworks.com/actors/fda-510k-device-clearances/): Medical device clearances by company, device, or code

Part of [The Mine Works](https://themineworks.com/): 151 pay-per-result scrapers with no login and no browser setup on your side.

## License

MIT © The Mine Works
