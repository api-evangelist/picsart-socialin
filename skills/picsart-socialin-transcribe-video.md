---
name: Transcribe a video's audio with Picsart
description: Upload a video and transcribe its audio track using the Picsart Programmable Video API.
api: openapi/picsart-socialin-video-tools.yaml
operations: [video-upload, video-transcribe-audio, video-transcribe-audio-getresult, video-credits-balance]
---

# Transcribe a video's audio with Picsart

Use the Picsart Programmable Video API to transcribe the audio of a video.

## Auth
Send `X-Picsart-API-Key: <your key>`. Base URL: `https://video-api.picsart.io/v1`.

## Steps
1. Provide the video as a public URL or upload it first with `video-upload`.
2. Call `video-transcribe-audio` with the video input.
3. Transcription is asynchronous — poll `video-transcribe-audio-getresult` with the returned job id until status is `success`.
4. Read the transcript from the result payload. Track spend with `video-credits-balance`.

## Rules
- Async operations use the getresult polling pattern.
- Metered in credits; handle `429` with the `X-Picsart-RateLimit-Reset-Time` header.
- Errors return `{message, detail}`; see `errors/picsart-socialin-error-codes.yml`.
