# Japan Ramen Active Master API

**The world's cleanest ramen location API — every active ramen shop in Japan, English-first, built for AI agents.**

62,173 active shops · **100% geocoded** · names verified and corrected · REST API + MCP server.

We do one thing: *is this ramen shop still open — and exactly where?* Not a reviews site, not a Google or
Tabelog replacement — a clean, structured master your agent can treat as ground truth.

🔗 **Landing page, live demo & free trial:** https://ramen.gachi-tokusuru.com
📖 **The technical story** (romanization, benchmarks, coordinates): https://ramen.gachi-tokusuru.com/story

---

## What's in this repo

A **real 1,000-row sample** so you can see exactly what you get before signing up — no key, no signup.

```
open-data/sample_1000.json   # 1,000 REAL active shops, nationwide (47 prefectures)
```

> The full **62,173-shop master** is served only via the authenticated API. Sample IDs are public masks
> (internal keys withheld); `payment_qr_accepted` / `stationless_flag` are enriched in the live API only.

---

## Why it's different

| | Legacy scraping / review sites | Japan Ramen Active Master |
|---|---|---|
| Names | Romanize to nonsense | **Verified & corrected** — names a Japanese reader recognizes |
| Coordinates | Approximate / missing | **100% geocoded**, address-verified |
| Freshness | Closed shops still listed | Closed & relocated dropped, overseas branches excluded |
| Scope | Station-first bias | Deep-local `stationless` shops captured too |
| Legal | Unclear origin | Built from public & open data — original, independently derived |

We audited **53,502 records** against a **50.4% romanization-error baseline** and corrected every one.
[Read how →](https://ramen.gachi-tokusuru.com/story)

---

## Sample schema

```jsonc
{
  "rk_id": "rk_pub_00001",       // stable public-mask ID
  "name": "らーめん たべ亭",       // original Japanese
  "name_en": "Ramen Tabetei",    // verified romanization (inbound-ready)
  "pref": "三重県", "pref_en": "Mie",
  "city": "いなべ市", "city_en": "Inabe Shi",
  "lat": 35.150902, "lng": 136.510727,   // 100% geocoded
  "keito": ["tonkotsu"],         // coarse style enum: tonkotsu|miso|shoyu|shio|tsukemen|spicy|other
  "genre": "ramen",
  "cash_only_flag": null,        // three-valued: true | false | null (live API)
  "payment_qr_accepted": null,   // three-valued (live API)
  "stationless_flag": null,      // deep-local marker (live API)
  "status": "active"
}
```

Facts are three-valued: `true` / `false` / `null` — unknown is never coerced to `false`.
The live API returns a richer record (station distance, `sources[]`, `freshness{}`).

---

## Quickstart

### REST
```bash
curl "https://ramen.gachi-tokusuru.com/v1/shops?pref=Tokyo&limit=3" \
  -H "Authorization: Bearer YOUR_KEY"
```

### MCP (Claude Desktop / Claude Code)
```jsonc
{
  "mcpServers": {
    "japan-ramen": {
      "url": "https://ramen.gachi-tokusuru.com/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```
Tools: `search_ramen` · `get_ramen_shop` · `get_ramen_changes`

Grab a key on the landing page. Without a valid key the API returns **`401`**.

---

## Pricing (USD)

| Plan | Price | What you get |
|---|---|---|
| **Free trial** | $0 | 7-day trial · 1,000 requests/day · Tokyo, Osaka & Fukuoka · REST + MCP · no credit card |
| **Pro** ⭐ | **$500 / mo** | Unlimited requests · all 47 prefectures · REST + MCP · quarterly refresh · commercial-use license |

[Start the free trial →](https://ramen.gachi-tokusuru.com/#start) ·
Need multi-seat, redistribution, bulk, or a dataset you don't see? [Contact us](mailto:contact@gachi-tokusuru.com).

---

## Attribution & license

Store facts are derived from official Japanese government open data (**© municipality open data, CC BY**)
and **© OpenStreetMap contributors (ODbL)**; attribution is carried in the API `meta`. `stationless` and
transaction tags are original derived values by gachi-tokusuru.com. The `sample_1000.json` in this repo is
provided for evaluation under the same attribution terms.

© 2026 gachi-tokusuru.com
