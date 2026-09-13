---
name: green-screens-ai-quote-a-lane
description: Price a single truckload lane with Triumph Intelligence (Green Screens AI) — authenticate, get a predicted buy/sell rate, and pull the negotiation context around it.
generated: '2026-09-12'
method: generated
source: >-
  Grounded in operationIds from the provider's own OpenAPI at https://connect.greenscreens.ai/openapi.yaml
  (harvested 2026-09-12). Every operationId, path, parameter and field named below appears verbatim in
  that contract.
api: green-screens-ai:green-screens-ai-prediction-api
base_url: https://api.greenscreens.ai
operations:
  - authToken
  - predictionRates
  - negotiation
  - analyticsLaneTopCarriers
  - predictionHistory
---

# Quote a lane

Use this to answer "what should this truckload move cost, and what do I say in the negotiation".

## 1. Get a token

`POST /v1/auth/token` (`authToken`) on `https://api.greenscreens.ai`.

- `Content-Type: application/x-www-form-urlencoded`
- body: `grant_type=client_credentials&client_id=<id>&client_secret=<secret>`
- Read `access_token` and `expires_in` from the response. Cache it and refresh on `expires_in`, not
  per request.

Credentials come from an Admin in the Triumph Intelligence app (Preferences > Credentials). They are
not self-serve.

Every call below sends `Authorization: Bearer <access_token>`.

## 2. Predict the rate

`POST /v3/prediction/rates` (`predictionRates`).

- Optional header `X-GS-User` identifies the acting user.
- Body (`Prediction_PredictionRatesRequest`): `stops` (origin, destination and any extra stops),
  `transportType` (`VAN` | `REEFER` | `FLATBED`), `pickupDateTime`, and optionally `commodity`,
  `tag`, `currency` (`USD` | `CAD`, defaults USD).

Stops accept a ZIP, a city+state, or both. Do not send an empty body: the API answers
`400 missing_property` with `"Missing property: body"`.

## 3. Get negotiation context

`GET /v1/marketintelligence/negotiation-advice` (`negotiation`) with the same lane expressed as query
parameters: `transportType`, `originCountry`/`originState`/`originCity`/`originZip`, the matching
`destination*` set, `pickUpDateTime`, `hasExtraStops`, `currency`, `region`.

Four fields on the response are marked deprecated in the contract and should not be relied on:
`holidayIsComing`, `inspectionWeeks`, `originLtrLow`, `destinationLtrHigh`.

## 4. Optional — who runs this lane

`GET /v1/analytics/lane-top-carriers` (`analyticsLaneTopCarriers`), same lane parameters plus
`dateFrom` and `sort`. Carriers come back keyed by industry identifiers — SCAC, FMCSA `mc`, and
USDOT `dot` — so they map straight into your own vetting process.

## 5. Optional — what you predicted before

`GET /v3/prediction/history` (`predictionHistory`) takes a single `date` parameter.

## Error handling

The envelope is `{code, message}` on `application/json` — this API does **not** use RFC 9457.

| status | code | what to do |
|---|---|---|
| 400 | `missing_required_parameter`, `missing_property`, `invalid_request` | Fix the request; `invalid_request` means the client id is wrong. |
| 401 | *(empty body, `WWW-Authenticate: Bearer`)* | Token missing or expired — re-run step 1. |
| 403 | `access_forbidden` | Authenticated but not entitled. Feature access is a Keycloak role granted per account; contact Customer Success. |
| 422 | `request_validation` | Read `errors[]` — each entry is `{field, message, value}` with dotted paths like `loadSource.loadId`. |
| 424 | `distance_calculation_error` | Upstream mileage lookup failed for this lane. Retry once, then verify the pair is a routable US/CA lane. |
| 429 | `too_many_requests` | Throttled. There is **no** `Retry-After` and no `RateLimit-*` header — back off exponentially with jitter. |
| 500 | `internal_error` | Retry with backoff, then support@greenscreens.ai. |

## Rules

- This flow is read-only. Nothing here writes.
- There is no idempotency key and no request-id header on this API, so a retry cannot be
  de-duplicated server-side and a failure cannot be quoted back to support by id. Log your own
  correlation id locally.
- `connect.greenscreens.ai` is the docs host. Call `api.greenscreens.ai`.
