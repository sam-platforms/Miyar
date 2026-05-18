# Privacy Policy — Miyar

*Last updated: May 18, 2026*

Miyar ("we", "the app") is a calculation aid for Shariah-compliant stock screening. This document describes exactly what data Miyar handles, what stays on your device, what leaves it, and what we don't do.

## TL;DR

- **No account required.** You don't sign up; we don't authenticate you.
- **No analytics, no tracking SDKs, no advertising identifiers.** The app does not include Google Analytics, Firebase, Sentry, Mixpanel, AppsFlyer, Adjust, or any equivalent third-party telemetry.
- **No data leaves your device except the network calls listed below.** Those calls fetch public financial data; they do not transmit your screening history, preferences, watchlist, or overrides.
- **Your data is stored only in your iOS sandbox** (Apple-managed app container). It is not synced to iCloud, not backed up to our servers (we have no servers), and not shared with any third party.

## What data the app handles

### Data stored on your device only

The following items are persisted in your local iOS sandbox (`UserDefaults`) and never leave it:

- **Screening history (recent tickers)** — up to 10 ticker symbols you've recently screened, with the company name and a timestamp. Stored under `Miyar.RecentTickers.v1`.
- **App preferences** — appearance (Light / Dark / System), brand accent choice, result-screen layout choice, mandatory-disclaimer acceptance flag.
- **Inclusion-policy toggles** — treasury yield, dividend income, fair-value adjustments, vendor aggregate, "Other income" proxy.
- **Threshold overrides** — any custom per-standard cap deltas you've configured.
- **Manual financial overrides** — any values you've edited via Data Sources to replace a fetched figure with one from a 10-K footnote or scholar review (e.g., non-interest haram revenue).
- **Optional API keys** — if you've supplied a Stooq API key in Settings, it is stored in `UserDefaults` (not the iOS Keychain — keys here are non-secret rate-limit tokens, not credentials).

You can delete all of this at any time by removing the app from your device. iOS will purge the sandbox.

### Data Miyar requests over the network

Miyar fetches public financial data from third-party services. Each request is initiated *by your action* (entering a ticker, switching providers, switching periods). No background fetches.

The third-party services Miyar reaches are listed below, with what is sent and what they return:

1. **SEC EDGAR** (`data.sec.gov`, `www.sec.gov`)
   - Sent: the ticker you screened, in the URL path of a public-domain XBRL request. A User-Agent string with the app name and a contact email (SEC requires this).
   - Returned: XBRL company facts, submissions metadata (industry classification), and the SEC company ticker → CIK map.
   - SEC's data is public-domain U.S. government data. SEC publishes their own privacy policy at <https://www.sec.gov/privacy.htm>.

2. **Yahoo Finance** (`query1.finance.yahoo.com`, `query2.finance.yahoo.com`, `fc.yahoo.com`, `feeds.finance.yahoo.com`)
   - Sent: the ticker you screened. A standard browser User-Agent string. Yahoo session cookies (acquired during the handshake) are stored ephemerally in-memory only and discarded when the app closes.
   - Returned: quote summaries, fundamentals timeseries, key statistics, analyst coverage, and RSS news headlines for the requested ticker.
   - Yahoo's privacy policy: <https://policies.yahoo.com/us/en/yahoo/privacy/index.htm>.

3. **Google Finance** (`www.google.com/finance/`)
   - Sent: the ticker you screened in a URL path. A standard browser User-Agent string.
   - Returned: scraped financial statement data embedded in the Google Finance quote page (`AF_initDataCallback` blocks).
   - Google's privacy policy: <https://policies.google.com/privacy>.

4. **Stooq** (`stooq.com`, `stooq.org`)
   - Sent: the ticker you screened (or `xagusd` for live silver nisab pricing), and your optional Stooq API key if supplied.
   - Returned: historical and current price data, used to compute trailing-average market caps and the live silver-nisab benchmark for zakat.
   - Stooq's terms: <https://stooq.com/api/>.

5. **Stock Alarm Pro** (optional, if enabled)
   - Sent: the ticker you screened.
   - Returned: financial statement data.

### Data Miyar **does not** request

- Your name, email, phone number, or any contact information.
- Your location.
- Your contacts, calendar, photos, or any other Apple-protected resource.
- Your iOS advertising identifier (IDFA).
- Any device fingerprint or hardware identifier.
- Any payment information (Miyar has no in-app purchases or subscriptions).

## What Miyar uses your data for

- **Stored on-device preferences and history** are used solely to render the app's UI (recent tickers list, picker selections, override badges). They are never transmitted off-device.
- **Network responses from the third-party services above** are used solely to compute Shariah-screening ratios, purification amounts, and zakat figures, and to display them to you. They are not retransmitted, aggregated, or shared.

## Third-party SDKs

Miyar does **not** integrate any third-party SDKs. The only outbound traffic is the HTTPS requests to the public APIs listed above, made via Apple's standard `URLSession` (with a hidden `WKWebView` proxy for the Yahoo handshake, which Yahoo's anti-bot system requires).

## Data sharing

We do not share, sell, rent, license, or otherwise transmit your data to any third party. The third-party services Miyar reaches are *your* request to *their* service via the app's UI — the app is a client, not a broker.

## Children's privacy

Miyar is not directed at children under 13 and does not knowingly collect data from them. The app has no accounts, no profile, and no mechanism to identify a child user.

## Your choices

- **Delete all stored data**: remove Miyar from your iOS device. iOS will purge the app's sandbox.
- **Stop network requests**: enable Airplane Mode or revoke Miyar's "Local Network" permission. The app falls back to Manual mode where every field is user-entered.
- **Switch providers**: in Settings → Data providers, you can disable any provider you don't want the app to reach. SEC EDGAR is the default and the most privacy-respectful (US government, no tracking).

## Changes to this policy

If we change how Miyar handles data, this document will be updated and the "Last updated" date at the top will change. Material changes will be flagged in the app's release notes.

## Contact

Miyar is published by Cybelli. For privacy questions or to request more detail about a specific behavior, reach out via the developer contact on the App Store listing for Miyar.

— *The Miyar team*
