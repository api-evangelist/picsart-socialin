---
name: Remove an image background with Picsart
description: Upload or reference an image and remove its background using the Picsart Programmable Image API, then retrieve the result.
api: openapi/picsart-socialin-image-tools.yaml
operations: [image-upload, image-remove-background, image-getresult, image-credits-balance]
---

# Remove an image background with Picsart

Use the Picsart Programmable Image API to strip or replace an image background.

## Auth
Send every request with the header `X-Picsart-API-Key: <your key>`. Base URL: `https://api.picsart.io/tools/1.0`.

## Steps
1. Provide the source image either as a public `image_url`, a base64 DATA URI in `image_url`, or a binary upload. To reuse an image, first call `image-upload`.
2. Call `image-remove-background` with the image input and optional parameters (output type, background color/blur, format).
3. Requests are synchronous by default. To run asynchronously, send the HTTP `Prefer` header; then poll `image-getresult` with the returned transaction id until status is `success`.
4. Check remaining credits any time with `image-credits-balance`.

## Rules
- Operations are credit-metered — avoid aggressive automatic retries (each retry can consume credits). See `conventions/picsart-socialin-conventions.yml`.
- Handle `429` by backing off using the `X-Picsart-RateLimit-Reset-Time` header.
- Prefer `*_url` or binary inputs; `*_id` inputs were removed on 2026-06-01.
- Errors return `{message, detail}`; see `errors/picsart-socialin-error-codes.yml`.
