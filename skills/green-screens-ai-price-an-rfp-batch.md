---
name: green-screens-ai-price-an-rfp-batch
description: Price a whole RFP lane file against Triumph Intelligence (Green Screens AI) using the batch and long-term batch prediction operations.
generated: '2026-09-12'
method: generated
source: >-
  Grounded in operationIds from https://connect.greenscreens.ai/openapi.yaml (harvested 2026-09-12).
api: green-screens-ai:green-screens-ai-prediction-api
base_url: https://api.greenscreens.ai
operations:
  - authToken
  - predictionBatchRates
  - predictionLongTermBatchRates
  - predictionNetworkRates
  - predictionBatchNetworkRates
---

# Price an RFP batch

Spot pricing a bid file is `predictionBatchRates`; contract/award pricing over a longer horizon is
`predictionLongTermBatchRates`. They are different operations with different request shapes.

## 1. Token

`POST /v1/auth/token` (`authToken`) — see the quote-a-lane skill. Cache on `expires_in`.

## 2. Spot batch

`POST /v3/prediction/batch-rates` (`predictionBatchRates`), optional `X-GS-User` header.

Body (`Prediction_PredictionBatchRatesRequest`) is a single field, `requests`: an array of the same
per-lane objects `predictionRates` takes (`stops`, `transportType`, `pickupDateTime`, `commodity`,
`tag`, `currency`).

## 3. Long-term batch

`POST /v3/prediction/long-term/batch-rates` (`predictionLongTermBatchRates`).

Body (`Prediction_PredictionLongTermBatchRatesRequest`) takes `requests` plus the shape controls:
`rateType`, `historicalDataType`, `historyPeriod`, `geographyLevel`, `includeNetwork`,
`includeMargin`, `includeSellRate`, `includeVolume`, `includeBuyRate`, `includeMinBuyRate`,
`includeMaxBuyRate`.

Ask only for the `include*` fields you will use — each one widens the response for every lane in the
file.

## 4. Network rates

`POST /v3/prediction/network-rates` (`predictionNetworkRates`) for one lane, or
`POST /v3/prediction/batch-network-rates` (`predictionBatchNetworkRates`) for many, when you want the
network view rather than the market view.

## Sizing and limits

- The provider removed per-file lane caps in February 2026. The only published ceiling is a **100 MB
  file size** on product-side batch uploads. No per-request lane count is published for the API.
- 429 `too_many_requests` is declared on this operation. There is no `Retry-After` header and no
  published rate limit, so a batch driver must implement its own concurrency ceiling and exponential
  backoff with jitter.

## Rules

- **No idempotency.** If a batch call times out you cannot safely assume it did not run, and there is
  no key to replay it under. Prefer smaller batches you can reconcile, and record what you sent.
- **No dry-run.** There is no validate-only mode; a malformed file is discovered by `422
  request_validation`, whose `errors[]` array names each failing field and its dotted path.
- Read-only operation — batch prediction does not create bids or quotes.
