---
name: green-screens-ai-sync-tms-and-quotes
description: Feed loads, carriers, shippers and quotes from a TMS into Triumph Intelligence (Green Screens AI). One-way ingestion with no published rollback.
generated: '2026-09-12'
method: generated
source: >-
  Grounded in operationIds from https://connect.greenscreens.ai/tmsconnector/v2/openapi.yaml,
  https://connect.greenscreens.ai/quotes/v2/openapi.yaml and
  https://connect.greenscreens.ai/quotes/v1/openapi.yaml (harvested 2026-09-12).
api: green-screens-ai:green-screens-ai-tms-api
base_url: https://api.greenscreens.ai
operations:
  - authToken
  - tmsImportLoad
  - tmsBatchImportLoad
  - tmsImportCarrier
  - tmsBatchImportCarrier
  - tmsShipper
  - tmsBatchImportShipper
  - quotesImport
  - quotesBatchImport
  - quotesGetAll
---

# Sync a TMS into Triumph Intelligence

The quality of every prediction this platform returns depends on what you feed it here. This is the
write path.

## 1. Token

`POST /v1/auth/token` (`authToken`).

## 2. Reference data first

Import the entities a load points at, before the loads:

- `POST /v2/tms/import-carrier` (`tmsImportCarrier`) / `POST /v2/tms/batch/import-carrier`
  (`tmsBatchImportCarrier`) — carrier profiles carry `mc`, `dot` and `scac`; populate all three you
  have.
- `POST /v2/tms/import-shipper` (`tmsShipper`) / `POST /v2/tms/batch/import-shipper`
  (`tmsBatchImportShipper`).

## 3. Loads

`POST /v2/tms/import-load` (`tmsImportLoad`) or `POST /v2/tms/batch/import-load`
(`tmsBatchImportLoad`).

Body (`TmsConnector_ImportLoadRequest`): `loadId`, `origin`, `destination`, `extraStops`, `rate`,
`pickupDate`, `deliveredDate`, `transportType`, `transportTypeGroup`, `transportMode`, `status`,
`details`, `shipper`, `carrier`.

`TmsConnector_Details.miles` is marked **deprecated** in the contract — stop sending it.
`status` includes `CANCELED`, which is how a cancelled load is represented; there is no delete
operation for an imported load.

## 4. Quotes

- `POST /v2/quotes/import` (`quotesImport`) — body `Quotes_QuotesImportRequest`: `quoteId`, `loadId`,
  `userEmail`, `transportType`, `transportTypeGroup`, `stops`, `distance`, `pickupDateTime`,
  `deliveredDateTime`, `expirationDateTime`, `quoteDateTime`, `status`, `rejectionReason`, `weight`,
  `shipper`, `pricingType`, `pricingTypeGroup`, `contractDuration`, `numberOfLoads`, `costs`.
- `POST /v2/quotes/batch/import` (`quotesBatchImport`) for volume.
- `GET /v2/quotes` (`quotesGetAll`) to read back — paginated with `page` / `perPage` (note: analytics
  uses `pageNumber` / `pageSize` instead; the API is not consistent here).

Quotes **v1** carries a wider surface if you need it — `saveQuote`, `acceptQuote`, `rejectQuote`,
`updateQuote`, `deleteQuote`, `shipperInfo`, `laneTopQuotes` — and is still published. v2 is **not**
a superset of v1.

## Rules that matter on this path

- **One-way.** No delete, void, or rollback operation exists for an imported load, carrier or
  shipper. Once ingested, correction means re-importing with the same `loadId`, not undoing.
- **No idempotency key.** Use your own stable `loadId` / `quoteId` / `quoteId` values as the
  de-duplication anchor, and read back before re-sending after a timeout.
- **No dry-run.** Validate locally; `422 request_validation` returns `errors[]` with `{field,
  message, value}` and dotted paths.
- Throttling: 429 `too_many_requests`, no `Retry-After`, no published limit. Cap concurrency yourself.
- Batch product uploads are limited to 100 MB (February 2026 release notes); no per-request record
  count is published for the API.
