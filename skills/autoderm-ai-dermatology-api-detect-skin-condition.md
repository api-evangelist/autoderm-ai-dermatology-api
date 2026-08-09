---
name: Detect a skin condition from an image
description: >-
  Submit one skin image to the Autoderm API and return the ranked list of
  probable dermatological conditions with ICD-10 codes and human-readable
  labels, presented under the mandatory medical-device safety warning.
api: openapi/autoderm-ai-dermatology-api-openapi.yml
base_url: https://api.autoderm.ai
operations:
  - detect_blur_v1_utils_detect_blur_post
  - infer_diseases_v1_v1_infer_diseases_v1_post
  - get_disease_catalog_v1_v1_infer_diseases_v1_diseases_get
generated: '2026-08-09'
method: generated
source: >-
  Grounded in openapi/autoderm-ai-dermatology-api-openapi.yml (every
  operationId verified verbatim) plus
  https://docs.autoderm.ai/en/medical-device/interface-creation
---

# Detect a skin condition from an image

## Before you start — this is a regulated medical device

Autoderm is CE-marked under EU MDD 93/42/EEC. Its documentation imposes obligations on **whatever
surface shows the result**, including yours. You must not run this skill and then present the output
as a diagnosis, a reassurance, or an "all clear".

Non-negotiable, from Autoderm's Interface Creation notice:

- Display the text **"Results are for information only and are not a medical diagnosis."** with every
  result, visible without scrolling and never obscured.
- The device **cannot** produce a "no disease detected" result. Never infer one from low confidence.
- Prefer qualitative bands over raw percentages for lay users: High possibility ≥ 33%, Possible 10–33%,
  Unlikely < 10%.
- If you do show numeric confidence, include: *"Confidence scores sum to 100% across the five displayed
  outputs. These values are normalised from probabilities calculated across all internal subclasses."*

## Authentication

Every step below requires a bearer token issued from https://app.autoderm.ai:

```
Authorization: Bearer YOUR_API_TOKEN
```

Server-side only. Never place this token anywhere a user can reach it.

## Step 0 — load the disease catalog once (cached)

Call `get_disease_catalog_v1_v1_infer_diseases_v1_diseases_get`:

```
GET /v1/infer-diseases/v1/diseases
Authorization: Bearer YOUR_API_TOKEN
```

Cache the result. It is static for a given model version and Autoderm explicitly instructs clients
**not** to call it at runtime. Each entry is keyed by `icd_10` and carries per-language `name`,
`simple_name` (the layman's term) and `read_more_url` for en, fr, de, it, es, sv and zh.

If your cache is warm, skip this step entirely.

## Step 1 — screen the image before you spend a detection

Call `detect_blur_v1_utils_detect_blur_post`:

```
POST /v1/utils/detect-blur
Authorization: Bearer YOUR_API_TOKEN
Content-Type: multipart/form-data

image=@lesion.jpg
```

Returns `{"is_blurry": bool, "variance": number}`. If `is_blurry` is true, ask for a new photo rather
than continuing — a blurry image costs a billable detection and yields an unreliable prediction.

Also validate locally before uploading:
- at least 224 × 224 pixels
- under 5 MB (the docs say 5 MB; the OpenAPI schema description says 10 MB — use the lower bound)
- JPG, PNG, BMP, GIF, TIFF, WebP or DICOM

## Step 2 — run the detection

Call `infer_diseases_v1_v1_infer_diseases_v1_post`:

```
POST /v1/infer-diseases/v1?include_skin_tone=false&require_anonymous=true
Authorization: Bearer YOUR_API_TOKEN
Content-Type: multipart/form-data

image=@lesion.jpg
```

- `require_anonymous=true` asks Autoderm to reject images where the subject is identifiable. Set it when
  you have not already stripped identifying content. Autoderm is explicit that this "is intended as a
  supporting safeguard only" and does not discharge your data-protection duties.
- `include_skin_tone=true` adds a Fitzpatrick classification to the same response instead of requiring a
  second call to `infer_skin_tone_v1_v1_infer_skin_tone_v1_post`.

Response shape:

```
{
  "predictions": [
    {"disease": "...", "confidence": 0.0-1.0, "icd_10": "...", "name": "..."}
  ],
  "skin_tone": {"fitzpatrick": 1-6, "confidence": 0.0-1.0}   // only if requested
}
```

## Step 3 — join to the catalog and present

For each prediction, look up `icd_10` in the cached catalog to get the localized `name`, the
`simple_name` for lay audiences, and the `read_more_url`. The prediction itself only carries an English
`name`.

Present the top five ordered by descending confidence, under the mandatory warning.

## Error handling

| Status | Body | What to do |
|---|---|---|
| 401 | `{"detail": "Missing Authorization header"}` | Token missing or malformed. Do not retry blindly. |
| 422 | `{"detail": [{"loc": [...], "msg": "...", "type": "..."}]}` | Read `detail[].msg`. Usually image missing, too small, too large, unsupported format, or rejected by `require_anonymous`. Fix the input, do not retry the same bytes. |

`detail` is a **string** on 401 and an **array** on 422 — branch on its JSON type before parsing.

Every response carries an `x-request-id` header. Log it; Autoderm support asks for it.

## Retry rule — read this before adding retries

**Autoderm has no idempotency key.** `POST /v1/infer-diseases/v1` is a metered call billed per detection
($1.00 per call beyond the plan allowance on Basic). A retry after a network timeout may bill a second
detection for a call that already succeeded server-side.

Therefore:
- Never auto-retry a timeout on an inference endpoint without human or policy approval.
- Retry only on connection failures that occurred *before* the request body was sent.
- Never retry a 422 — it is deterministic.
