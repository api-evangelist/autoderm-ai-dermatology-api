# Autoderm – AI Dermatology API (autoderm-ai-dermatology-api)

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

Autoderm is a white-label REST API for AI-assisted analysis of dermatological images, operated as a regulated medical device. A client POSTs a single skin photograph as multipart/form-data and receives the top five most probable conditions, each with a confidence score between 0 and 1, an ICD-10 code and an English name; a companion static catalog maps every ICD-10 code to localized and layman's names plus read-more links in seven languages. Alongside disease detection the API exposes Fitzpatrick skin-type classification, a blur/image-quality screen, a genitalia content-safety classifier, an age estimator, and — unusually — the regulatory device label itself as a live anonymous endpoint. Autoderm is CE-marked under EU MDD 93/42/EEC as a legacy Class I device, is transitioning to MDR Class IIa under EU MDR 2017/745, and holds FDA Breakthrough Device Designation. It is sold into telemedicine, pharmacy, and digital health platforms as a decision-support and triage tool, and is explicitly not intended as a means of diagnosis.

**APIs.json:** [https://autoderm-ai-dermatology-api.apievangelist.com/apis.yml](https://autoderm-ai-dermatology-api.apievangelist.com/apis.yml)

## Tags

- dermatology-api
- ai-dermatology
- medical-imaging
- telemedicine
- skin-analysis
- rest-api
- openapi
- llms-txt
- ce-marked
- white-label
- healthcare
- medical-ai
- computer-vision
- medical-device
- icd-10
- image-classification
- clinical-decision-support
- triage

## Timestamps

- **Created:** 2026-08-07
- **Modified:** 2026-08-09

## APIs

### Autoderm – AI Dermatology API Device API

The device API from Autoderm – AI Dermatology API — 1 operation(s) for device.

- **Human URL:** [https://docs.autoderm.ai/en](https://docs.autoderm.ai/en)
- **Base URL:** `https://api.autoderm.ai`

#### Tags

- device

#### Properties

- [OpenAPI](openapi/autoderm-ai-dermatology-api-device-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/autoderm-ai-dermatology-api-device-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autoderm-ai-dermatology-api-device-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Open A P I  Source](https://api.autoderm.ai/openapi.json)
- [Documentation](https://docs.autoderm.ai/en)
- [API Reference](https://docs.autoderm.ai/en/api-reference)
- [Getting Started](https://docs.autoderm.ai/en/getting-started/getting-started)
- [L L M S Txt](https://autoderm.ai/llms.txt)

### Autoderm – AI Dermatology API Inference API

The inference API from Autoderm – AI Dermatology API — 5 operation(s) for inference.

- **Human URL:** [https://docs.autoderm.ai/en](https://docs.autoderm.ai/en)
- **Base URL:** `https://api.autoderm.ai`

#### Tags

- inference

#### Properties

- [OpenAPI](openapi/autoderm-ai-dermatology-api-inference-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/autoderm-ai-dermatology-api-inference-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autoderm-ai-dermatology-api-inference-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Open A P I  Source](https://api.autoderm.ai/openapi.json)
- [Documentation](https://docs.autoderm.ai/en)
- [API Reference](https://docs.autoderm.ai/en/api-reference)
- [Getting Started](https://docs.autoderm.ai/en/getting-started/getting-started)
- [L L M S Txt](https://autoderm.ai/llms.txt)

### Autoderm – AI Dermatology API System API

The system API from Autoderm – AI Dermatology API — 6 operation(s) for system.

- **Human URL:** [https://docs.autoderm.ai/en](https://docs.autoderm.ai/en)
- **Base URL:** `https://api.autoderm.ai`

#### Tags

- system

#### Properties

- [OpenAPI](openapi/autoderm-ai-dermatology-api-system-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/autoderm-ai-dermatology-api-system-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autoderm-ai-dermatology-api-system-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Open A P I  Source](https://api.autoderm.ai/openapi.json)
- [Documentation](https://docs.autoderm.ai/en)
- [API Reference](https://docs.autoderm.ai/en/api-reference)
- [Getting Started](https://docs.autoderm.ai/en/getting-started/getting-started)
- [L L M S Txt](https://autoderm.ai/llms.txt)

### Autoderm – AI Dermatology API Utils API

The utils API from Autoderm – AI Dermatology API — 1 operation(s) for utils.

- **Human URL:** [https://docs.autoderm.ai/en](https://docs.autoderm.ai/en)
- **Base URL:** `https://api.autoderm.ai`

#### Tags

- utils

#### Properties

- [OpenAPI](openapi/autoderm-ai-dermatology-api-utils-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/autoderm-ai-dermatology-api-utils-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autoderm-ai-dermatology-api-utils-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Open A P I  Source](https://api.autoderm.ai/openapi.json)
- [Documentation](https://docs.autoderm.ai/en)
- [API Reference](https://docs.autoderm.ai/en/api-reference)
- [Getting Started](https://docs.autoderm.ai/en/getting-started/getting-started)
- [L L M S Txt](https://autoderm.ai/llms.txt)

## Common Properties

- [M C P Server](mcp/autoderm-ai-dermatology-api-mcp.yml)
- [Website](https://autoderm.ai/)
- [Developer Portal](https://app.autoderm.ai)
- [Documentation](https://docs.autoderm.ai/en)
- [API Reference](https://docs.autoderm.ai/en/api-reference)
- [Getting Started](https://docs.autoderm.ai/en/getting-started/getting-started)
- [Support](https://docs.autoderm.ai/en/support/support-contact)
- [Blog](https://autoderm.ai/blog/)
- [GitHub Organization](https://github.com/autodermai)
- [Pricing](https://autoderm.ai/pricing/)
- [Sign Up](https://app.autoderm.ai/en/auth/sign-up)
- [Login](https://app.autoderm.ai/en/auth/login)
- [Terms of Service](https://autoderm.ai/terms-of-service-autoderm/)
- [Privacy Policy](https://autoderm.ai/privacy-policy/)
- [Compliance](https://autoderm.ai/regulatory/)
- [Deprecation](https://docs.autoderm.ai/en/support/api-versioning)
- [Versioning](https://docs.autoderm.ai/en/support/api-versioning)
- [Authentication](authentication/autoderm-ai-dermatology-api-authentication.yml)
- [Conventions](conventions/autoderm-ai-dermatology-api-conventions.yml)
- [Error Catalog](errors/autoderm-ai-dermatology-api-problem-types.yml)
- [Lifecycle](lifecycle/autoderm-ai-dermatology-api-lifecycle.yml)
- [Conformance](conformance/autoderm-ai-dermatology-api-conformance.yml)
- [Data Model](data-model/autoderm-ai-dermatology-api-data-model.yml)
- [Rate Limits](rate-limits/autoderm-ai-dermatology-api-rate-limits.yml)
- [Plans](plans/autoderm-ai-dermatology-api-plans.yml)
- [Packages](packages/autoderm-ai-dermatology-api-packages.yml)
- [S D Ks](packages/autoderm-ai-dermatology-api-packages.yml)
- [Examples](examples/_index.yml)
- [JSON Schema](json-schema/) — [JSON Schema](https://json-schema.org/specification)
- [Overlay](overlays/autoderm-ai-dermatology-api-openapi-overlay.yaml)
- [L L Ms Txt](llms/autoderm-ai-dermatology-api-llms.txt)
- [Agent Skill](skills/_index.yml)
- [Agentic Access](agentic-access/autoderm-ai-dermatology-api-agentic-access.yml)
- [Domain Security](security/autoderm-ai-dermatology-api-domain-security.yml)

## Maintainers

**FN:** Alexander Börve
**Email:** support@autoderm.ai
**URL:** https://autoderm.ai/
