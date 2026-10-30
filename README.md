# Green Screens AI

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

Green Screens AI — now sold as Triumph Intelligence following its acquisition by Triumph Financial — publishes predictive freight rate, capacity and pricing intelligence APIs for truckload brokers and shippers across the United States and Canada. The estate spans eleven versioned services behind one OAuth2 client-credentials gateway: lane rate prediction (spot, network and long-term batch), market intelligence and negotiation advice, carrier and lane analytics keyed on SCAC, MC and USDOT identifiers, historical rates, pricing rules, quotes, a carrier bid cycle, and a TMS connector for importing loads, carriers and shippers. Twelve first-party OpenAPI 3.0.2 documents, 36 paths and 47 operations are published openly at connect.greenscreens.ai; the callable production host is api.greenscreens.ai. A CDN-distributed browser widget bundle and a Chrome extension are the only client libraries.

**Areas:** Artificial Intelligence · Freight · Logistics · Machine Learning · Pricing · Transportation

## Green Screens AI on APIs.io

Everything profiled for Green Screens AI is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/green-screens-ai/](https://apis.io/providers/green-screens-ai/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Green Screens AI Prediction API](https://apis.io/apis/green-screens-ai/green-screens-ai-prediction-api/) — Prediction service v3 — lane rate prediction, batch rates, network rates, long-term batch rates and prediction history. Spec version 3.8.0, 6 paths. The…
- [Green Screens AI Auth API](https://apis.io/apis/green-screens-ai/green-screens-ai-auth-api/) — Authentication service. OAuth 2.0 client_credentials grant (RFC 6749) issuing a Keycloak JWT that is presented as an RFC 6750 bearer token on every other…
- [Green Screens AI Analytics API](https://apis.io/apis/green-screens-ai/green-screens-ai-analytics-api/) — Analytics service v1 — lane top carriers and lane Triumph carriers, returned with SCAC, FMCSA MC and USDOT identifiers. The only paginated collection in the…
- [Green Screens AI Bids API](https://apis.io/apis/green-screens-ai/green-screens-ai-bids-api/) — Carrier bids service v1 — save, read, update and delete bids, search carriers, accept a bid, and send a bid request to an external carrier. Spec version…
- [Green Screens AI History API](https://apis.io/apis/green-screens-ai/green-screens-ai-history-api/) — Historical rate data and similar lanes analysis v1 — load history and recent rates. Spec version 1.0.0, 2 paths.
- [Green Screens AI Pricing API](https://apis.io/apis/green-screens-ai/green-screens-ai-pricing-api/) — Pricing service v1 — priority rules, combination rules and threshold rules (full CRUD each), 3PL pricing, and marketplace broker partners. Spec version…
- [Green Screens AI Quotes API](https://apis.io/apis/green-screens-ai/green-screens-ai-quotes-api/) — Quotes service v2 — list quotes, import and batch import. Spec version 2.0.0, 3 paths. NOT a superset of v1: the accept, reject, update, delete,…
- [Green Screens AI TMS API](https://apis.io/apis/green-screens-ai/green-screens-ai-tms-api/) — TmsConnector service v2 — import loads, carriers and shippers, singly or in batches, from a broker transportation management system. Spec version 2.18.6, 6…
- [Green Screens AI Market Intelligence API](https://apis.io/apis/green-screens-ai/green-screens-ai-market-intelligence-api/) — Market Intelligence service v1 View separately Try it in swagger

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [green-screens-ai-mcp.yml](https://apis.io/servers/green-screens-ai/green-screens-ai-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Green Screens Ai Agentic Access](https://apis.io/agentic-access/green-screens-ai/green-screens-ai-agentic-access/)

#### Collections (10)

Postman and Open Collection request collections.

- [Triumph Intelligence Connect](https://apis.io/collections/green-screens-ai/open-green-screens-ai/)
- [Triumph Intelligence Connect Analytics API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-analytics-api/)
- [Triumph Intelligence Connect Analytics Auth API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-auth-api/)
- [Triumph Intelligence Connect Analytics Bids API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-bids-api/)
- [Triumph Intelligence Connect Analytics History API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-history-api/)
- [Triumph Intelligence Connect Analytics MarketIntelligence API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-marketintelligence-api/)
- [Triumph Intelligence Connect Analytics Prediction API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-prediction-api/)
- [Triumph Intelligence Connect Analytics Pricing API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-pricing-api/)
- [Triumph Intelligence Connect Analytics Quotes API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-quotes-api/)
- [Triumph Intelligence Connect Analytics TMS API](https://apis.io/collections/green-screens-ai/open-green-screens-ai-tms-api/)

#### Overlays (12)

OpenAPI overlays, including conversational phrasing for each operation.

- [Green Screens Ai Analytics Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-analytics-overlay/)
- [Green Screens Ai Auth Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-auth-overlay/)
- [Green Screens Ai Bids Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-bids-overlay/)
- [Green Screens Ai Datalake Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-datalake-overlay/)
- [Green Screens Ai History Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-history-overlay/)
- [Green Screens Ai Marketintelligence Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-marketintelligence-overlay/)
- [Green Screens Ai Prediction V2 Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-prediction-v2-overlay/)
- [Green Screens Ai Prediction V3 Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-prediction-v3-overlay/)
- [Green Screens Ai Pricing Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-pricing-overlay/)
- [Green Screens Ai Quotes V1 Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-quotes-v1-overlay/)
- [Green Screens Ai Quotes V2 Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-quotes-v2-overlay/)
- [Green Screens Ai Tms Overlay](https://apis.io/overlays/green-screens-ai/green-screens-ai-tms-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Green Screens Ai Authentication](https://apis.io/security/green-screens-ai/green-screens-ai-authentication/)
- [Green Screens Ai Domain Security](https://apis.io/security/green-screens-ai/green-screens-ai-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Green Screens Ai Plans Pricing](https://apis.io/plans/green-screens-ai/green-screens-ai-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Green Screens Ai Rate Limits](https://apis.io/rate-limits/green-screens-ai/green-screens-ai-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Green Screens Ai Finops](https://apis.io/finops/green-screens-ai/green-screens-ai-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://triumph.io/solutions/rates/)
- [Documentation](https://connect.greenscreens.ai/)
- [Getting started](https://intelligencehelp.triumph.io/en/collections/8387516-partners-and-integrations)
- [API reference](https://connect.greenscreens.ai/)
- [Support](https://triumph.io/support/)
- [Changelog](https://intelligencehelp.triumph.io/en/articles/8520083-what-s-new)
- [Blog](https://triumph.io/blog/broker/)
- [Terms of service](https://triumph.io/terms-of-service/)
- [Privacy policy](https://triumph.io/privacy-policy/)
- [Status](https://triumph.statuspage.io/)

## API Evangelist rating

**Kin Score 43.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 46.8 |
| Contract governance | 4.5 |
| Operational transparency | 31.6 |
| Developer ergonomics | 73.2 |
| Access clarity | 27.6 |

**Agent readiness 29.4** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 22.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/green-screens-ai/](https://apis.io/providers/green-screens-ai/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Green Screens AI: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/green-screens-ai/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
