---
name: yandex-market-api
description: Use whenever the user wants to interact with Yandex Market (Яндекс Маркет) as a seller — managing the product catalog (карточки, offer-mappings), prices, stocks (остатки), orders (заказы FBS/FBY/DBS/Express), shipments (отгрузки), returns (возвраты), supply requests, promos (акции), bids (ставки продвижения), reports (отчёты), outlets (точки продаж), chats with buyers, goods feedback (отзывы), Q&A, hidden offers, tariffs, or any other Yandex Market Partner API endpoint. Trigger on phrases like "Yandex Market API", "API Яндекс Маркета", "партнёрский API маркета", "заказы на маркете", "остатки на маркете", "businessId", "campaignId", or any URL under api.partner.market.yandex.ru. The skill bundles the full official OpenAPI 3.0 spec (159 operations, ~40 sections) and a lookup tool — use it instead of guessing paths or schemas, even for endpoints that look obvious.
---

# Yandex Market Partner API

This skill helps you call the Yandex Market Partner API (`https://api.partner.market.yandex.ru`). It bundles the full OpenAPI 3.0 spec from the **official repository** (`github.com/yandex-market/yandex-market-partner-api`) — 149 paths / 159 operations.

The spec is ~1.4 MB. Don't read it whole — use the helpers described below to pull only what you need.

## Authentication — Api-Key header

The primary (and recommended) auth is a single header:

```http
Api-Key: <ключ>
```

The user creates keys in the seller cabinet: **иконка аккаунта → Настройки → API и модули → Авторизация через Api-Key**. Each key gets an access scope at creation (read-only / full / по разделам) — a read-only key gets `403` on mutating methods.

The spec also lists an **OAuth** scheme (scope `market:partner-api`) for apps acting on behalf of sellers — Yandex has been phasing it out in favor of Api-Key; only go there if the user explicitly builds a multi-seller app, and check the current official docs (`yandex.ru/dev/market/partner-api/doc/`) for the flow.

There is no sandbox host — this is the live cabinet. Test orders exist as a feature (`fake` order flags), but mutating calls hit the real store.

## businessId vs campaignId — the #1 source of confusion

Two different identifiers route every request:

- **`businessId`** — the cabinet («бизнес»). Paths like `/v2/businesses/{businessId}/...` operate on the shared catalog: offer-mappings (карточки), prices for all stores, promos, feedback, Q&A.
- **`campaignId`** — one store = one placement model inside the cabinet. Paths like `/v2/campaigns/{campaignId}/...` operate per-store: orders, stocks, store prices, shipments, outlets.

Get both from `GET /v2/campaigns` (each campaign carries its `business.id`). **`campaignId` is NOT the «номер магазина» shown in the cabinet UI** — the cabinet shows it under Настройки → API и модули → «Идентификатор кампании». Passing a shop number where a campaignId is expected yields 404/403.

## How to find the right endpoint — DO THIS FIRST

```bash
# 1) See all sections with endpoint counts
python3 scripts/lookup_endpoint.py tags

# 2) Find endpoints by keyword (matches path, summary, tag — case-insensitive,
#    auto-falls-back to a shorter stem so Russian inflections work)
python3 scripts/lookup_endpoint.py search остатки
python3 scripts/lookup_endpoint.py search /offer-mappings
python3 scripts/lookup_endpoint.py search --tag orders

# 3) Get full operation details (parameters, request/response schemas, deprecation)
python3 scripts/lookup_endpoint.py show /v2/campaigns/{campaignId}/orders
python3 scripts/lookup_endpoint.py show /v2/businesses/{businessId}/offer-mappings --method post
```

`show` resolves top-level `$ref` for readability but leaves nested refs alone — for a deeper schema, read `references/yandex-market-openapi.json` directly with `jq`:

```bash
jq '.components.schemas.UpdateOfferMappingDTO' references/yandex-market-openapi.json
```

For a category overview, browse [references/index.md](references/index.md) — a flat per-section list of all paths with the placement models each method applies to.

**Why this matters:** many methods exist in `/v1` and `/v2` variants, several are deprecated with successors named only in the description (e.g. `GET /v2/campaigns/{campaignId}/orders` is deprecated → `POST /v1/businesses/{businessId}/orders`), and method applicability depends on the placement model. Guessing leads to 404s or calling endpoints that don't apply to the user's store model.

## Placement models

Every order/stock/shipment method is tagged with the models it applies to — shown in `search` output, `show` tags, and `index.md` brackets:

- **FBY** — fulfillment by Yandex (склад Маркета);
- **FBS** — fulfillment by seller (свой склад, доставка Маркетом);
- **DBS** — delivery by seller (свой склад и своя доставка);
- **Express** — FBS с экспресс-доставкой;
- **laas** — logistics-as-a-service (отдельная логистика Маркета).

Before suggesting an endpoint for orders/stocks/shipments, confirm which model the user's store runs — a DBS-only method 404s/403s on an FBY campaign.

## Calling pattern

```bash
# example: list campaigns (the first call to make — gives campaignId + businessId)
curl -s "https://api.partner.market.yandex.ru/v2/campaigns" \
  -H "Api-Key: $YM_API_KEY" | jq .

# example: catalog cards (business-level, POST with filters + cursor pagination)
curl -s -X POST "https://api.partner.market.yandex.ru/v2/businesses/$BUSINESS_ID/offer-mappings?limit=50" \
  -H "Api-Key: $YM_API_KEY" -H "Content-Type: application/json" \
  -d '{}' | jq .

# example: update stocks for a store
curl -s -X PUT "https://api.partner.market.yandex.ru/v2/campaigns/$CAMPAIGN_ID/offers/stocks" \
  -H "Api-Key: $YM_API_KEY" -H "Content-Type: application/json" \
  -d '{"skus":[{"sku":"АРТИКУЛ-1","items":[{"count":10}]}]}' | jq .
```

For Python, use `requests`/`httpx` with the same header. No SDK needed — every endpoint is a plain JSON HTTP call.

## Conventions and gotchas

- **Base URL** is `https://api.partner.market.yandex.ru` (no trailing slash). Paths from the spec are appended directly.
- **Mixed HTTP verbs**: 107 POST / 35 GET / 15 PUT / 2 DELETE. Many reads are POST because filters go in the body. Check the method with `show`, don't assume.
- **Pagination is cursor-based**: query params `pageToken` + `limit`, response carries `paging.nextPageToken`. The older `page`/`pageSize` params are deprecated — don't use them in new code. `limit` often has **no default**: omitting it can change response shape or return everything.
- **`sku` here means the seller's own offer ID** (ваш SKU/артикул), not a marketplace-generated ID. Market's own card ID is `marketSku` where it appears.
- **Deprecated methods** are flagged in `search`/`show`/`index.md`; the successor is named in the `description`. Several high-traffic paths are deprecated (orders listing per campaign → business-level `POST /v1/businesses/{businessId}/orders`), so check before reusing old integration patterns.
- **Descriptions contain Yandex docs-platform markup** (`{% include ... %}`, `{% note %}`, `{#T}`, `{{ limit-param-description }}`) — these are unresolved includes from the source repo. In particular, **per-method rate limits live in those includes and are NOT visible in the spec**; the real limits are on the docs site. Treat `420 LIMIT` responses as authoritative.
- **Dates** are mostly `DD-MM-YYYY` in query params (старый стиль) and ISO 8601 in newer JSON bodies — check the field's `format`/`example` in the schema, this API mixes both.
- **Orders older than 30 days** (delivered/cancelled) disappear from the campaign orders method — use business-level orders or stats methods for history.

## Errors

Error wrapper is consistent across the API:

```json
{"status": "ERROR", "errors": [{"code": "...", "message": "..."}]}
```

- `400` — validation: re-read the request schema with `show`.
- `401` — missing/bad Api-Key.
- `403` — key scope doesn't allow this method, or the campaign belongs to another business.
- `404` — wrong path, wrong campaignId/businessId, or method not applicable to this placement model.
- `420` — **rate limit** (Yandex uses 420, not 429): back off, halve the request rate, retry with exponential backoff.
- `423` — method locked for this campaign (e.g. model mismatch or feature disabled).
- `500` — Yandex's side: retry with backoff.

When you report an error to the user, include the HTTP status and the full body.

## Sections at a glance

Functional tags sorted by endpoint count (model tags fbs/fby/dbs/express/laas excluded). Full per-endpoint list is in [references/index.md](references/index.md).

| Section | # | Notes |
|---|---:|---|
| reports | 26 | Генерация отчётов (цены, остатки, продажи, юнит-экономика): `POST .../generate` → poll `GET /v2/reports/info/{reportId}` → download |
| orders | 16 | Заказы: campaign-level CRUD статусов + business-level список |
| shipments | 12 | Отгрузки FBS: ярлыки, акты, паллеты |
| returns | 9 | Возвраты и невыкупы |
| chats | 7 | Чаты с покупателями: сообщения, файлы |
| business-offer-mappings | 6 | Карточки каталога (business-level): список, добавление/правка, удаление |
| goods-feedback | 5 | Отзывы на товары + комментарии |
| order-delivery | 5 | Трекинг, коробки, сроки доставки |
| outlets | 5 | Точки продаж (DBS/самовывоз) |
| prices | 5 | Цены: business- и campaign-level, карантин цен рядом (`price-quarantine`, 4) |
| bids | 4 | Ставки продвижения товаров |
| offers | 4 | Campaign-level список товаров, скрытие (`hidden-offers`, 3) |
| promos | 4 | Акции Маркета: список, вход/выход |
| regions | 4 | Справочник регионов |
| warehouses | 4 | Склады FBY и свои |
| stocks | 2 | Остатки: PUT по складу кампании |
| supply-requests | 3 | Заявки на поставку FBY |
| goods-questions | 3 | Вопросы и ответы о товарах |
| content | 3 | Контент карточек: категории, характеристики (`categories`, 2 рядом) |
| campaigns / businesses | 4 | `GET /v2/campaigns` — стартовая точка: campaignId + businessId |
| прочее | ~15 | tariffs, ratings, orders-stats, goods-stats, delivery-services, outlet-licenses, order-labels, auth (`POST /v2/auth/token` — инфо о текущем токене), operations |

## Working with the user

- If the user's request maps to one obvious endpoint, look it up, show them the call you're about to make (URL, method, body), and execute when they confirm.
- If the request is ambiguous (e.g. "обнови цены" — business-level for all stores or campaign-level for one?), `search` first and ask which they mean.
- Start sessions with `GET /v2/campaigns` when IDs are unknown — it resolves both campaignId and businessId and shows the placement model of each store.
- When credentials are missing, ask for `YM_API_KEY` and explain where to get it (кабинет → Настройки → API и модули). Don't fabricate test calls without credentials — prepare the curl/python command and let the user run it.
- Watch out for endpoints that mutate state (цены, остатки, статусы заказов, отгрузки). Confirm with the user before sending — there is no sandbox.
