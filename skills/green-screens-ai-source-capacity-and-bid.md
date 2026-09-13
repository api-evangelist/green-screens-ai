---
name: green-screens-ai-source-capacity-and-bid
description: Find carriers for a lane and run the bid cycle in Triumph Intelligence (Green Screens AI) — search, save, send, accept. Contains the one irreversible write in this API.
generated: '2026-09-12'
method: generated
source: >-
  Grounded in operationIds from https://connect.greenscreens.ai/bids/v1/openapi.yaml and
  https://connect.greenscreens.ai/openapi.yaml (harvested 2026-09-12).
api: green-screens-ai:green-screens-ai-bids-api
base_url: https://api.greenscreens.ai
operations:
  - authToken
  - carrierInfo
  - analyticsLaneTopCarriers
  - saveBid
  - getBids
  - getBidByKey
  - recentBids
  - updateBid
  - deleteBid
  - requestBid
  - acceptBid
---

# Source capacity and run a bid

## Read before you act

`POST /v1/bids/send` (`requestBid`) **sends a bid request to an external carrier**. There is no
recall, cancel, void, or undo operation published for it anywhere in this contract. Treat it as
irreversible, and confirm with a human before calling it. `saveBid` is the reversible sibling —
it records a bid without contacting anyone.

## 1. Token

`POST /v1/auth/token` (`authToken`). Cache on `expires_in`.

## 2. Find carriers

- `GET /v1/bids/carriers` (`carrierInfo`) — carrier search.
- `GET /v1/analytics/lane-top-carriers` (`analyticsLaneTopCarriers`) — who actually runs this lane.

Both return carriers identified by SCAC, FMCSA `mc` and USDOT `dot`. Carry those identifiers through;
do not re-key carriers by name.

## 3. See what already exists

- `GET /v1/bids` (`getBids`) — bids for the current user.
- `GET /v1/bids/recent` (`recentBids`) — the ten most recent bids for a lane.
- `GET /v1/bids/by-key/{key}` (`getBidByKey`) — one bid by key.

## 4. Record a bid (reversible)

`POST /v1/bids` (`saveBid`), body `Bids_BidsRequest`: `userEmail`, `carrierName`, `carrierMC`,
`carrierDOT`, `carrierEmail`, `carrierPhone`, `origin`, `destination`, `extraStops`, `transportType`,
`pickupDateTime`, `deliveredDateTime`, `bidDateTime`, `bidCost`, `loadProNumber`, `weight`,
`commodity`, `brokerComment`, `carrierComment`, `currency`.

Corrections: `PATCH /v1/bids/{bidId}` (`updateBid`).
Removal: `DELETE /v1/bids/{bidId}` (`deleteBid`). **No window is published** for how long a bid stays
deletable — do not promise the user one.

## 5. Send the request (IRREVERSIBLE — gate on human approval)

`POST /v1/bids/send` (`requestBid`), body `Bids_BidsSendRequest`: `userEmail`, `carriers`, `origin`,
`destination`, `extraStops`, `pickupDateTime`, `deliveredDateTime`, `loadProNumber`, `weight`,
`commodity`, `brokerComment`, `transportType`.

Use the structured `carriers` array. `carrierEmailList` and `carrierPhoneList` are marked
**deprecated** in the contract.

Because this API has **no idempotency key**, a timeout on this call is genuinely ambiguous: the
request may have gone out. Do not blind-retry. Read back with `getBids` / `recentBids` first.

The provider's July 2026 release notes add a bid status and notification for email send failure —
check the bid's status rather than assuming delivery.

## 6. Accept

`POST /v1/bids/accept` (`acceptBid`), body `Bids_BidActionRequest`: `key`, `bidCost`, `carrierName`,
`carrierMC`, `carrierComment`, `currency`. No published reversal.

## Errors

Same `{code, message}` envelope as everywhere else. Watch for `item_not_found` (404) when a `bidId`
or `key` does not belong to the authenticated account, and `403 access_forbidden` when the account
lacks the entitlement.

## Rules

- Never call `requestBid` without explicit human confirmation of carrier list, lane and cost.
- Never retry a write on timeout; read back instead.
- No time window may be stated to the user for deleting a bid — the provider does not publish one.
