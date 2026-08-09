---
name: Verify the Autoderm device identity and API version
description: >-
  Read the live regulatory medical-device label and semantic version from the
  Autoderm API so an integration can record which device build produced a given
  result — a due-diligence and post-market-surveillance step, not a feature.
api: openapi/autoderm-ai-dermatology-api-openapi.yml
base_url: https://api.autoderm.ai
operations:
  - get_label_v1_label_get
  - get_version_version_get
  - get_health_health_get
generated: '2026-08-09'
method: generated
source: >-
  Grounded in openapi/autoderm-ai-dermatology-api-openapi.yml (every
  operationId verified verbatim) and a live capture of GET
  https://api.autoderm.ai/v1/label on 2026-08-09.
---

# Verify the device identity and API version

Autoderm does something most APIs do not: it serves its **regulatory medical-device label as a live API
resource**, anonymously. If you are integrating a regulated device into a clinical or triage workflow,
this is the endpoint that lets you record *which device*, at *which version*, produced a stored result.

None of these calls require authentication and none are metered.

## Step 1 — read the device label

Call `get_label_v1_label_get`:

```
GET /v1/label
```

Returns a `MedicalDeviceLabel`:

| Field | Meaning |
|---|---|
| `device_name` | Device trade name |
| `device_type` | e.g. "Registered Medical Device" |
| `version` | Device version, GS1 AI (10) prefixed |
| `manufacturer` | Legal manufacturer name and address |
| `manufacture_date` | GS1 AI (11), YYYYMMDD |
| `ce_mark` | CE marking class and directive |
| `unique_device_identifier` | Full UDI string, GS1 application identifiers |
| `eifu` | Notice pointing at the electronic Instructions For Use |
| `warning` | Consult-IFU warning text |
| `support` | Support contact |
| `uk_responsible_person` | UK Responsible Person, where appointed |

A verbatim capture is stored at
`examples/autoderm-ai-dermatology-api-get-label-200.json`.

## Step 2 — read the API version

Call `get_version_version_get`:

```
GET /version
```

Returns `{"name": "...", "version": "..."}`. Autoderm follows semantic versioning: PATCH is
backward-compatible fixes, MINOR adds features or optional parameters without breaking you, MAJOR is
reserved for breaking changes.

The same handler is also registered at `/v1/system/version`
(`get_version_v1_system_version_get`) — either is fine.

## Step 3 — liveness

Call `get_health_health_get`:

```
GET /health
```

Returns `{"status": "ok"}`. Also available as `/healthz`, `/v1/system/health` and
`/v1/system/healthz`, each with a HEAD variant, which is the cheapest form for a monitor.

This matters commercially: Autoderm's SLA commits to 99.5% monthly availability but places the burden
of proof on the customer — to claim a service credit you "must provide log files showing Unscheduled
Downtime and the date and time it occured". A HEAD poll against `/healthz` with timestamps IS that
evidence. Nobody else will collect it for you; Autoderm publishes no status page.

## What to persist

For every stored prediction, record alongside it:

- `unique_device_identifier` and `ce_mark` from Step 1
- `version` from Step 2
- the `x-request-id` response header from the inference call

That triple is what lets you answer, months later, which device build produced a given output — the
question a post-market surveillance or vigilance enquiry actually asks.

## Deprecation watch

Autoderm commits to at least 90 days' notice before deprecating an endpoint, communicated through
customer channels and documentation updates. There is no `Sunset` or `Deprecation` response header and
no dated changelog, so polling `/version` and diffing `https://api.autoderm.ai/openapi.json` is the only
machine-readable way to notice a change. See
`lifecycle/autoderm-ai-dermatology-api-lifecycle.yml`.
