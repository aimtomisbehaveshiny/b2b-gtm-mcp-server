# B2B Lead, Shopify, Ads & Keyword Intelligence MCP Server

Connect **Claude Desktop**, **Cursor**, **Windsurf**, **n8n AI Agents**, or any **Model Context Protocol (MCP)** client directly to 5 live, fair-billed B2B GTM & competitive intelligence tools over Streamable HTTP (`/mcp`).

---

## Live MCP Standby Endpoint

```text
https://aimtomisbehave--b2b-gtm-mcp-server.apify.actor/mcp
```

**Authentication:** Pass your Apify API token either as an `Authorization: Bearer YOUR_APIFY_TOKEN` header or `?token=YOUR_APIFY_TOKEN` query parameter.

---

## Included Tools (`tools/list`)

1. **`enrich_shopify_store`** — Detect Shopify & Shopify Plus stores, resolve `myshopify.com` subdomain, HQ country/city/currency, theme, SKU count & 30-day product velocity, **30+ installed Shopify apps** (Klaviyo, Gorgias, ReCharge, Yotpo, Judge.me, Triple Whale, etc.), **9 ad pixels**, and MX-verified merchant emails/phones/socials. *(1 unit if Shopify or contacts found; `$0` otherwise.)*
2. **`extract_website_contacts`** — Crawl any company website homepage + `/contact` + `/about` pages with Chrome TLS impersonation, **Cloudflare `data-cfemail` XOR decoding**, Schema.org JSON-LD parsing, E.164 phone validation, WhatsApp, 12 social links, tech stack/ad pixels, and DNS MX provider detection. *(1 unit if >=1 contact or social found; `$0` on dead/empty sites.)*
3. **`verify_b2b_emails`** — Verify up to 25 emails per call with syntax validation, domain typo detection (`gmial.com`), 4,000+ disposable/burner blocklist, role-account flagging, live DNS `MX` + `SPF` + `DMARC` policy checks, and Microsoft 365 `GetCredentialType` verification. *(1 unit per verified email.)*
4. **`discover_buyer_keywords`** — Query up to 6 live autocomplete engines concurrently (**Google, YouTube, Google Shopping, Amazon, Bing, DuckDuckGo**) with Google internal relevance scores, BOFU/MOFU/TOFU funnel classification, and `opportunityScore` (`1–100`). *(1 unit per 5 returned keywords; `$0` if empty.)*
5. **`check_google_ads_advertiser`** — Check whether a domain, brand name, or Google Advertiser ID (`AR...`) actively runs Google Ads (`isRunningGoogleAds`, verified legal entity name, country, Transparency account URL, and recent decoded ad creatives). *(1 unit if advertiser/ads found; `$0` on empty/rate-limited responses.)*

---

## 1-Click Client Setup

### Claude Desktop (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "b2b-gtm-intelligence": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://aimtomisbehave--b2b-gtm-mcp-server.apify.actor/mcp",
        "--header",
        "Authorization: Bearer YOUR_APIFY_TOKEN"
      ]
    }
  }
}
```

### Cursor / Windsurf (`.cursor/mcp.json`)

```json
{
  "mcpServers": {
    "b2b-gtm-intelligence": {
      "url": "https://aimtomisbehave--b2b-gtm-mcp-server.apify.actor/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_APIFY_TOKEN"
      }
    }
  }
}
```

### n8n AI Agent (`MCP Client Tool` Node)

- **Endpoint URL:** `https://aimtomisbehave--b2b-gtm-mcp-server.apify.actor/mcp?token={{ $env.APIFY_API_TOKEN }}`
- **Transport:** HTTP Streamable

---

## Fair Pay-Per-Event Pricing (`mcp-intel-unit`)

| Plan Tier | Price per 1,000 Units | Cost per Typical Tool Call |
| :--- | :---: | :---: |
| **Free / Bronze** | **$1.50 / 1k** | `$0.0015` |
| **Silver** | **$1.25 / 1k** | `$0.00125` |
| **Gold+** | **$1.00 / 1k** | `$0.0010` |

- **$0.00** start fee, **$0.00** on failed/unreachable sites or empty searches.
- For massive 1,000+ row batch jobs with Google Maps Dataset chaining, invoke our dedicated batch Actors directly:
  - [`aimtomisbehave/shopify-store-leads-scraper`](https://apify.com/aimtomisbehave/shopify-store-leads-scraper)
  - [`aimtomisbehave/website-contact-scraper`](https://apify.com/aimtomisbehave/website-contact-scraper)
  - [`aimtomisbehave/bulk-email-verifier-pro`](https://apify.com/aimtomisbehave/bulk-email-verifier-pro)
  - [`aimtomisbehave/google-ads-transparency-scraper`](https://apify.com/aimtomisbehave/google-ads-transparency-scraper)
  - [`aimtomisbehave/google-autocomplete-keyword-scraper`](https://apify.com/aimtomisbehave/google-autocomplete-keyword-scraper)
