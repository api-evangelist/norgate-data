# Norgate Data (norgate-data)

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

### Norgate Data Corporate Actions and Time Series

Point-in-time series for building survivorship-bias-free databases - index constituent history, major-exchange-listed status, capital events, dividend yield, unadjusted close, blank-check-company flags and padding status. Modeled: `index_constituent_timeseries`, `major_exchange_listed_timeseries`, `capital_event_timeseries`, `dividend_yield_timeseries`, `unadjusted_close_timeseries`, `blank_check_company_timeseries`, `padding_status_timeseries`.

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
