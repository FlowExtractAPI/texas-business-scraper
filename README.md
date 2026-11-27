**[Texas Business Search](https://apify.com/dz_omar/texas-business-scraper?fpr=smcx63)** looks up businesses in the **Texas Comptroller's public business records** and returns each one as clean, structured data. Type a **business name, Texas taxpayer number, EIN or Secretary of State file number** and get back the **registered agent, the officers and directors, franchise tax status and, optionally, every business location**. Or skip the names and build a **list of Texas businesses** by type, status, registration date, city, ZIP code or county.

It is built for **lead generation and sales research**, **KYB and compliance teams**, **process servers and legal work**, and **data teams** who need Texas company records in bulk instead of one search at a time on the state website.

## What does Texas Business Search do?

- 🔎 **Look up by name or number** — any mix of names, taxpayer numbers, EINs and file numbers, one per line, in one run
- 📋 **Build lists of businesses** — new LLCs this month, active corporations in one city, nonprofits in one county; closed businesses included on request
- 🏛️ **Registered agent and officers** — agent name and office, plus every officer, director or manager the business reported, with titles and addresses
- 📍 **Business locations** — the places a business holds a sales-tax permit, with address, industry code and first-sales date
- 🧩 **Very common names, listed in full** — a name like "Smith" matches thousands of businesses; the Actor lists them all and tells you if any could not be listed
- ✅ **Complete rows** — every row says whether its details were included, so nothing is silently missing

Running it on Apify also gives you **API access**, **scheduling** (re-check a watchlist every week), **integrations** with Make, Zapier, n8n, Google Sheets and webhooks, and exports to **JSON, CSV and Excel**.

### What data can you extract from Texas business records?

| Group | Fields |
|---|---|
| 🆔 Identity | name, taxpayer number, EIN, trade name (DBA), Secretary of State file number |
| 📊 Status | franchise tax status, Secretary of State status, registration date, state of formation, entity type |
| 📮 Address | mailing street, city, state, ZIP, ZIP+4, county |
| 🏛️ Registered agent | agent name, registered office street, city, state, ZIP, report year |
| 👥 Officers and directors | count, one-line summary and a detailed list with name, title, address and year |
| 📍 Locations | location number, name, address, county, industry code (NAICS), permit date, first-sales date |
| 🧭 Context | the search that found the business, search type, details status, source page, time of extraction |

Sole proprietors and businesses that never registered with the Comptroller are not in these records.

### Why use Texas Business Search on Apify?

The state's own search shows one business at a time and stops at 200 matches. This Actor takes a whole list, goes past that limit, and delivers everything as a dataset you can schedule, export or call over the API. A single lookup with details costs under one cent.

## How to search Texas businesses

1. Click **Try** to open the Actor in Apify Console (or add it to your account).
2. To look up businesses you know, enter **one per line** in **Business names or numbers**: a name such as `Dell Inc` (finds every business that **starts with** it), an 11-digit **taxpayer number**, a 9-digit **EIN**, or a **Secretary of State file number**.
3. To build a list instead, leave that box empty and use **Find lists of businesses**: pick the type of business, the status, a registration date range, and a city, ZIP code or county.
4. Under **What to include**, choose whether to add **agent and officers** (on by default) and **business locations** (off by default).
5. Set **Maximum businesses** (start small, the default is 50) and click **Start**.
6. Download the results from the **Output** tab as JSON, CSV or Excel, or fetch them over the API.

> 💡 Dates accept a calendar day or plain words such as `30 days` (the last 30 days). Leave a filter empty to ignore it.

## How much does it cost to search Texas businesses?

This Actor uses **pay-per-event** pricing: you pay for businesses delivered, not for compute time.

| Event | FREE | BRONZE | SILVER | GOLD |
|---|---|---|---|---|
| Run start (per GB of memory; the default counts as one) | $0.003 | $0.0025 | $0.002 | $0.002 |
| Business found (identity, status, address) | $0.001 | $0.0009 | $0.0008 | $0.0007 |
| Agent and officers add-on (per business read) | $0.002 | $0.0018 | $0.0016 | $0.0014 |
| Business locations add-on (per business with locations) | $0.001 | $0.0009 | $0.0008 | $0.0007 |

**Example costs on the FREE plan:**

- One lookup with agent and officers: $0.003 + $0.001 + $0.002 = **$0.006**
- 100 businesses with agent and officers: $0.003 + 100 × $0.003 = **$0.303**
- 1,000 businesses with agent and officers: about **$3.00**
- 1,000 businesses, identity only: about **$1.00**

Add-ons are charged only when they delivered something: a business whose agent and officers could not be read, or that has no locations, is not charged for that add-on. Set **Max cost per run** in the run options and the Actor stops cleanly at that budget.

## Input and output examples

### Input

```json
{
    "searchTerms": ["Dell Inc", "17601402922"],
    "includeDetails": true,
    "includeLocations": true,
    "maxResults": 50
}
```

| Input value | What it does |
|---|---|
| `Dell Inc` | Finds every business whose name starts with it, closed ones included |
| `17601402922` | Returns the business with this Texas taxpayer number |
| `742487834` | A 9-digit number is tried as an EIN, then as a file number |
| *(empty)* + filters | Builds a list, for example `"businessTypes": ["llc"]`, `"city": "Austin"`, `"registeredFrom": "30 days"` |

### Output

One record per business (real output; empty fields left out, two of the seven officers shown):

```json
{
    "type": "business",
    "name": "DELL INC.",
    "taxpayer_number": "17424878340",
    "fei_number": "742487834",
    "dba_name": "DELL COMPUTER INC.",
    "sos_file_number": "0007444706",
    "right_to_transact": "ACTIVE",
    "sos_status": "ACTIVE",
    "texas_registration_date": "1987-10-27",
    "state_of_formation": "DE",
    "mailing_address_street": "1 DELL WAY # RR1-35 ATTN: TAX DEPT",
    "mailing_address_city": "ROUND ROCK",
    "mailing_address_state": "TX",
    "mailing_address_zip": "78682",
    "registered_agent_name": "CORPORATION SERVICE COMPANY D/B/A+",
    "registered_office_street": "211 E. 7TH STREET SUITE 620",
    "registered_office_city": "AUSTIN",
    "registered_office_state": "TX",
    "registered_office_zip": "78701",
    "report_year": "2026",
    "officer_count": 7,
    "officers": [
        { "name": "MICHAEL S. DELL", "title": "CEO", "active_year": "2026", "street": "ONE DELL WAY RR1-35", "city": "ROUND ROCK", "state": "TX", "zip": "78682", "source": "SOS" },
        { "name": "DAVID KENNEDY", "title": "CFO", "active_year": "2026", "street": "ONE DELL WAY RR1-35", "city": "ROUND ROCK", "state": "TX", "zip": "78682", "source": "SOS" }
    ],
    "detail_status": "ok",
    "search_term": "Dell Inc",
    "search_type": "name",
    "source_url": "https://comptroller.texas.gov/taxes/franchise/account-status/search/17424878340",
    "scraped_at": "2026-11-24T20:42:52.835Z"
}
```

With **business locations** on, a business also carries `location_count` and `locations`:

```json
{
    "name": "BUC-EE'S, LTD.",
    "taxpayer_number": "17601402922",
    "location_count": 34,
    "locations": [
        { "location_number": "1", "name": "BUC-EE'S #2", "street": "101 HWY 2004", "city": "LAKE JACKSON", "state": "TX", "zip": "77566", "county": "Brazoria", "naics_code": "445120", "permit_issue_date": "1985-03-16", "first_sales_date": "1985-04-01" }
    ]
}
```

Each business returns its first 25 locations; `location_count` is always the full number. A row's `detail_status` is `ok` (agent and officers included), `not_requested` (you turned them off), `no_franchise_record` (the Comptroller lists this taxpayer but holds no franchise tax record, typical for businesses that only hold sales-tax permits) or `unavailable` (could not be read in this run; the business is still delivered and the add-on is not charged).

### Call it as an API

Look up one business with a single HTTP request, no run to start and no dataset to read:

```bash
curl -H "Authorization: Bearer $APIFY_TOKEN" \
  "https://dz-omar--texas-business-scraper.apify.actor/lookup?q=Dell%20Inc&maxResults=1"
```

The response is JSON: `{ "items": [ ... ], "count": 1 }`, each item shaped like the record above. Parameters are `q` (a name or number), `maxResults` (1 to 25), `includeDetails` and `includeLocations`. A request is billed per business returned, with no start fee, and a request that returns nothing costs nothing. Bigger lists belong in a normal run.

## Other Actors you might need

<!-- RECOMMENDED:START (generated by apify-actor-forge/tools/recommend.py; edits inside are overwritten) -->

| Actor | What it adds |
|---|---|
| **[California Business & UCC Lien Search](https://apify.com/dz_omar/california-bizfile-scraper?fpr=smcx63)** | California business entities & UCC liens: status, registered agent and filings |
| **[Delaware Business Search](https://apify.com/dz_omar/delaware-corporations-scraper?fpr=smcx63)** | Registered Agents & Bulk Lookup |
| **[realestate.com.au Agents Scraper](https://apify.com/dz_omar/realestate-com-au-agents-scraper?fpr=smcx63)** | Agents & agencies by suburb or postcode: emails, phones, listing counts & median sold price |
| **[LinkedIn Jobs Scraper](https://apify.com/dz_omar/linkedin-jobs-scraper?fpr=smcx63)** | LinkedIn job postings with salary ranges, applicant counts & the recruiter who posted |
| **[AI Scraper](https://apify.com/dz_omar/ai-lead-extractor?fpr=smcx63)** | Emails, phones, job titles & social links from any website, plus custom AI data fields |

<!-- RECOMMENDED:END -->

## Frequently asked questions

### Is it legal to scrape Texas business records?

The Actor reads information that any visitor can see without logging in. You are responsible for how you use the data, including privacy and marketing rules such as GDPR, CCPA and anti-spam laws. This is not legal advice.

### Do I need a Texas account or a login?

No. You only need your Apify account. There are no cookies, API keys or accounts to set up.

### What can I search for?

Business names (a name matches every business that starts with it), 11-digit Texas taxpayer numbers, 9-digit EINs and Secretary of State file numbers. You can mix them in one list; a business found twice is delivered once.

### How does it handle very common names?

A name that matches thousands of businesses is listed in full automatically; there is no setting to change. If a few businesses cannot be listed individually, the run adds a notice row with the exact count, so you always know what is missing.

### How fresh is the data?

Single lookups and the agent and officer details are read live. Lists built from filters, and business locations, come from the Comptroller's open records, which are refreshed weekly; list rows carry the refresh date in `source_as_of`.

### Why are some officers or agents empty?

Only businesses that file a franchise tax report show officers, and some do not file one yet (new businesses). Those rows are marked in `detail_status` and are not charged for the add-on.

### Can I use it through the API or on a schedule?

Yes. Start runs from the Apify API, any Apify client, Make, Zapier or n8n, schedule them in Apify Console, or call the lookup API above from your own app or AI agent.

### What happens if a run stops part-way?

Every business is saved the moment it is read and the run status message says what happened. If the platform restarts a run, businesses already delivered are not delivered or charged again.

## Support

- 🌐 **Website:** [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email:** [support@flowextractapi.com](mailto:support@flowextractapi.com)
- 💬 **GitHub:** [FlowExtractAPI](https://github.com/FlowExtractAPI)
- 💼 **LinkedIn:** [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **X (Twitter):** [@FlowExtractAPI](https://x.com/FlowExtractAPI)
- 📱 **Facebook:** [flowextractapi](https://www.facebook.com/flowextractapi)
- 🎵 **TikTok:** [@flowextractapi](https://www.tiktok.com/@flowextractapi)

## Legal & compliance

- **Public data only** — data visible to any visitor, no login, no cookies.
- **Rate limiting** — modest request rates with back-off.
- **Data protection** — no storage of personal information or unauthorized data collection.
- **Commercial use** — suitable for business intelligence and research.
- No affiliation with or endorsement by the Texas Comptroller of Public Accounts is implied.

---

*Texas Business Search — by FlowExtract API. Turn any website into structured data.*
