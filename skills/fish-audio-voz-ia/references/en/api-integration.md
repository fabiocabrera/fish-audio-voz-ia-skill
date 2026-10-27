# API integration

Always check Fish Audio's official documentation; model names and prices change.

## The call

`POST https://api.fish.audio/v1/tts`

- Header `Authorization: Bearer <your key>`.
- Header `Content-Type: application/json; charset=utf-8`.
- Header `model`: the model. There is a free model for development and paid models. If omitted, the account default applies.
- Minimal JSON body:

```json
{ "text": "Hello! This is a test.", "reference_id": "<voice id>", "format": "mp3", "language": "pt" }
```

- The response is the audio (MP3 by default), streamed. Common error codes: 401 invalid key, 402 payment, 503 service overloaded.

Useful parameters: `format` (mp3, wav, opus), `latency` (normal gives the best quality), `prosody.speed` (0.5 to 2.0), `prosody.volume`, `language`, and a pronunciation dictionary for acronyms and brand names.

## Node.js example (no dependencies)

```js
const resp = await fetch('https://api.fish.audio/v1/tts', {
  method: 'POST',
  headers: {
    Authorization: `Bearer ${process.env.FISH_AUDIO_API_KEY}`,
    'Content-Type': 'application/json; charset=utf-8',
    model: process.env.FISH_AUDIO_MODEL || 'your-account-model',
  },
  body: JSON.stringify({ text, reference_id: voiceId, format: 'mp3', language: 'pt' }),
  signal: AbortSignal.timeout(90000),
});
if (!resp.ok) throw new Error(`TTS failed: HTTP ${resp.status}`);
fs.writeFileSync('speech.mp3', Buffer.from(await resp.arrayBuffer()));
```

## Cautions

- **Accents in the Windows terminal:** sending JSON directly with `curl -d` in a Git Bash style terminal breaks the encoding (a 400 "invalid unicode" error). Use a file (`--data-binary @request.json`) or Node code.
- **Speed:** `ffmpeg -i speech.mp3 -filter:a atempo=1.1 out.mp3`.
- **Character limit:** the 500-character limit mentioned for the website's free plan belongs to the web interface, not the API. Check your plan.
- **Concurrency:** the account has a simultaneous request limit; generate scene lines one after another, with a short retry.
