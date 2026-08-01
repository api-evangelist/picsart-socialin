---
name: Upscale and enhance an image with Picsart
description: Increase resolution and enhance quality of an image using the Picsart Programmable Image API upscale/enhance operations.
api: openapi/picsart-socialin-image-tools.yaml
operations: [image-upscale, image-ultra-upscale, image-ultra-upscale-getresult, image-ultra-enhance, image-face-enhance]
---

# Upscale and enhance an image with Picsart

Increase image resolution and quality using the Picsart Programmable Image API.

## Auth
Send `X-Picsart-API-Key: <your key>`. Base URL: `https://api.picsart.io/tools/1.0`.

## Steps
1. For a standard upscale, call `image-upscale` with the image input and an `upscale_factor`.
2. For maximum quality, call `image-ultra-upscale` (asynchronous) and poll `image-ultra-upscale-getresult` with the returned transaction id until status is `success`.
3. To improve perceived quality without changing dimensions, use `image-ultra-enhance`; for portraits, use `image-face-enhance`.
4. Retrieve the output URL from the result payload.

## Rules
- Provide the image as `image_url` (public URL or base64 DATA URI) or binary upload; `*_id` inputs were removed on 2026-06-01.
- Async operations use the getresult polling pattern; synchronous by default, opt into async with the `Prefer` header.
- Metered in credits; watch `429` and back off with `X-Picsart-RateLimit-Reset-Time`.
- Errors return `{message, detail}`; see `errors/picsart-socialin-error-codes.yml`.
