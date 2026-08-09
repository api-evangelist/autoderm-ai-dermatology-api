---
name: Screen an image for quality and content safety before inference
description: >-
  Run Autoderm's cheap pre-checks — blur detection and the genitalia content
  classifier — to reject unusable or sensitive uploads before spending a
  metered disease detection.
api: openapi/autoderm-ai-dermatology-api-openapi.yml
base_url: https://api.autoderm.ai
operations:
  - detect_blur_v1_utils_detect_blur_post
  - infer_genitals_v1_v1_infer_genitals_v1_post
  - infer_skin_tone_v1_v1_infer_skin_tone_v1_post
generated: '2026-08-09'
method: generated
source: >-
  Grounded in openapi/autoderm-ai-dermatology-api-openapi.yml (every
  operationId verified verbatim) plus
  https://docs.autoderm.ai/en/medical-device/eifu
---

# Screen an image for quality and content safety

Autoderm bills per detection. Every unusable image that reaches
`infer_diseases_v1_v1_infer_diseases_v1_post` is money spent on a prediction nobody can trust. This
skill runs the cheap gates first.

## Authentication

```
Authorization: Bearer YOUR_API_TOKEN
```

## Gate 1 — local validation (free)

Reject before any network call if the image:

- is smaller than 224 × 224 pixels
- exceeds 5 MB
- is not JPG, PNG, BMP, GIF, TIFF, WebP or DICOM

## Gate 2 — blur detection

Call `detect_blur_v1_utils_detect_blur_post`:

```
POST /v1/utils/detect-blur
Authorization: Bearer YOUR_API_TOKEN
Content-Type: multipart/form-data

image=@upload.jpg
```

Returns `{"is_blurry": bool, "variance": number}` — `variance` is the variance of the Laplacian. If
`is_blurry` is true, stop and ask for a new photo.

Coaching to hand back to the user, taken from Autoderm's eIFU:
- Tap the lesion to auto-focus before capturing; hold the camera steady.
- Use bright, even light — natural daylight or soft white. No flash, no filters.
- Fill the frame with the lesion, on a plain neutral background.
- Send the original, unedited photo.

## Gate 3 — content safety

Call `infer_genitals_v1_v1_infer_genitals_v1_post`:

```
POST /v1/infer-genitals/v1
Authorization: Bearer YOUR_API_TOKEN
Content-Type: multipart/form-data

image=@upload.jpg
```

Returns `{"prediction": bool, "confidence": number}`. Use this to route the image down a restricted
handling path — reviewer consent, restricted logging, no thumbnailing — rather than to silently discard
it. Genital dermatology is legitimate clinical use; the classifier exists so you can handle it
appropriately, not so you can refuse it.

## Optional — Fitzpatrick skin type

Call `infer_skin_tone_v1_v1_infer_skin_tone_v1_post`:

```
POST /v1/infer-skin-tone/v1
Authorization: Bearer YOUR_API_TOKEN
Content-Type: multipart/form-data

image=@upload.jpg
```

Returns `{"fitzpatrick": 1-6, "confidence": number}` where 1 is lightest and 6 is darkest. Useful for
auditing whether your own population coverage is skewed.

If you are going on to run disease detection anyway, do **not** call this separately — pass
`include_skin_tone=true` on `infer_diseases_v1_v1_infer_diseases_v1_post` and get it in the same
response for one detection.

## Anonymity

Autoderm's own anonymity check is a parameter on the detection call
(`require_anonymous=true`), not a standalone endpoint. It rejects images where the subject is
identifiable. Autoderm states it "does not guarantee full anonymisation of submitted images, replace
client-side filtering, validation, or review processes, nor does it transfer responsibility for data
protection or privacy compliance to Autoderm." Do your own face and metadata stripping first.

## Errors

- `401` — `{"detail": "Missing Authorization header"}`
- `422` — `{"detail": [{"loc": [...], "msg": "...", "type": "..."}]}`; deterministic, never retry.

No idempotency key exists on this API. See
`conventions/autoderm-ai-dermatology-api-conventions.yml`.
