---
name: Generate an image from text with Picsart GenAI
description: Generate images from a text prompt using the Picsart GenAI API and retrieve the async result.
api: openapi/picsart-socialin-genai-tools.yaml
operations: [genai-text2image, genai-text2image-getresult, genai-credits-balance]
---

# Generate an image from text with Picsart GenAI

Use the Picsart GenAI API to create images from a text prompt.

## Auth
Send `X-Picsart-API-Key: <your key>` on every request. Base URL: `https://genai-api.picsart.io/v1`.

## Steps
1. Call `genai-text2image` with a `prompt` (and optional `negative_prompt`, `count`, and model parameters).
2. Text2Image runs asynchronously — take the returned job/inference id and poll `genai-text2image-getresult` until the standardized status is `success` (treat `processing` as keep-waiting, `error` as failure).
3. Retrieve the generated image URLs from the result payload.
4. Monitor spend with `genai-credits-balance`.

## Rules
- Job statuses are standardized to `success` / `error` / `processing` (April 2026). Switch on `success` and `error`.
- Metered in credits; be deliberate about retries.
- Enterprise GenAI Additional Terms of Use apply (effective 2026-04-30).
- Errors return `{message, detail}`; see `errors/picsart-socialin-error-codes.yml`.
