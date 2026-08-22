# Norgate Data (norgate-data)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Norgate Data provides high-quality, survivorship-bias-free **end-of-day (EOD) historical market data** for US, Australian and Canadian stocks, around 100 worldwide **futures** markets, and **foreign exchange**. It is a long-standing vendor (founded 1995) focused on clean, backtest-ready daily data for systematic traders and quants.

> **Access model - read this first.** Norgate Data is **not a hosted REST API**. There is no public HTTP/REST base URL and no WebSocket. Subscribers install the **Norgate Data Updater (NDU)** - a Windows desktop application that downloads and maintains a complete **local database** and runs a **local data service**. Programmatic access is through the **`norgatedata` Python package** (on PyPI), which reads from that local NDU database and returns **Pandas DataFrames / NumPy arrays**. NDU must be running for the package to work. This catalog entry honestly models the library's logical operations as capability areas; it is a **client library over a local service**, not a public API.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/norgate-data/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/norgate-data/refs/heads/main/apis.yml)

## Tags

- Market Data
- Financial Data
- Historical Data
- Futures
- Stocks
- End of Day
- EOD
- Backtesting
- Survivorship Bias Free
- Python

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## How Access Works

- **Norgate Data Updater (NDU):** Windows-only desktop app (Windows 10/11 or Windows Server; Mac/Linux users run it in a Windows VM or WSL2 with mirrored networking). It maintains a local, survivorship-bias-free database and applies the daily EOD update.
- **`norgatedata` Python package:** `pip install norgatedata`. Requires an active subscription and a running NDU. Depends on pandas, numpy, requests and logbook. Returns price/volume history, corporate-action time series, metadata, fundamentals and watchlists.
- **Platform plugins & integrations:** Amibroker plugin, plus community integrations with Python backtesting frameworks such as **Zipline** (`zipline-norgatedata`) and **Backtrader**.

## Capability Areas (modeled from the `norgatedata` library)

These are the library's logical operations, grouped as capability areas. They are **local library calls**, not HTTP endpoints.

### Norgate Data Price and Volume Data

Daily OHLCV, volume, turnover, unadjusted close, dividends and open interest as Pandas/NumPy. Supports date ranges, limits, weekly/monthly/quarterly/yearly intervals, capital-and-dividend price adjustment, and date padding. Modeled: `price_timeseries`.

- **Reference:** [https://pypi.org/project/norgatedata/](https://pypi.org/project/norgatedata/)


### Norgate Data Security Metadata and Classifications

Single-value reference lookups - name, symbol, asset id, domicile, currency, exchange, classification at any level, corresponding industry index, base type, listing status, quoted-date range and tick size. Modeled: `security_name`, `symbol`, `assetid`, `domicile`, `currency`, `exchange_name`, `classification`, `classification_at_level`, `status`, `tick_size`, and related.

### Norgate Data Futures Metadata

Reference data for ~100 futures markets across 11 exchange groups - market/session names and symbols, session contracts, point value, margin and first notice date. Unadjusted and back-adjusted spot-month continuous contracts. Modeled: `futures_market_symbols`, `futures_market_session_contracts`, `point_value`, `margin`, `first_notice_date`, and related.

- **Reference:** [https://norgatedata.com/futurespackage.php](https://norgatedata.com/futurespackage.php)

### Norgate Data Fundamentals

Company fundamentals - named fundamental fields, financial and business summaries, shares outstanding and shares float. Availability depends on package. Modeled: `fundamental`, `financial_summary`, `business_summary`, `sharesoutstanding`, `sharesfloat`.

### Norgate Data Watchlists and Databases

Enumerate and resolve security lists - watchlists, built-in databases and their member symbols - plus database/price update timestamps for freshness checks. Modeled: `watchlist`, `watchlists`, `watchlist_symbols`, `database`, `databases`, `database_symbols`, `last_database_update_time`, `last_price_update_time`.

## Pricing (summary)

Norgate is sold as a flat **data subscription**, not metered API calls; the Python package and plugins are free with a subscription. Stock data is packaged per market by history depth; futures and forex are separate. Terms are 6 or 12 months (~10% annual discount). Grounded USD figures (verify on Norgate's price calculator):

- **Stocks - Silver:** ~USD 270/yr per market, 10 years of history
- **Stocks - Gold:** ~USD 360/yr per market, 20 years of history
- **Stocks - Platinum:** ~USD 630/yr per market, history back to the early 1990s (delisted securities + historical index constituents)
- **Stocks - Diamond (US only):** deepest tier, history back to 1950
- **Futures:** ~USD 270/yr (~USD 148.50 for 6 months), ~100 markets, history back to ~1980, continuous contracts
- **Forex:** separate package, history back to 1991

See [plans/norgate-data-plans-pricing.yml](plans/norgate-data-plans-pricing.yml).

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/norgatedata)
- [Website](https://norgatedata.com/)
- [Documentation](https://pypi.org/project/norgatedata/)
- [Plans](plans/norgate-data-plans-pricing.yml)
- [Rate Limits](rate-limits/norgate-data-rate-limits.yml)
- [Fin Ops](finops/norgate-data-finops.yml)

## Review

Does Norgate Data expose a documented public WebSocket API? **No** - and it exposes no hosted public API at all. Access is the `norgatedata` Python library over a local NDU database delivering EOD historical data. There is no REST, SSE or WebSocket transport. See [review.yml](review.yml).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
