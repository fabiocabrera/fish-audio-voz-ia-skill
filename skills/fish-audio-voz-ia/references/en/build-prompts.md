# Build prompts

Paste into Claude, in your video project's folder, in order.

## 1. API test

> Read the Fish Audio text-to-speech documentation. Create a script that reads the key from an environment variable, generates audio for a Portuguese sentence with accents and saves it as MP3. Send the JSON from code (UTF-8), not from the command line. Do not print the key.

## 2. Choosing voices

> Search the Fish Audio catalog for Portuguese voices that fit my kind of video (describe the tone). Generate a sample of each candidate with the same text, tell me which is which and wait for my approval. Then save the approved ones in a list with nickname, id, gender and use.

## 3. Voice module

> Create an isolated `generateVoice(text, voiceId, config)` module, with a timeout, that returns the MP3. Add tests that do not hit the network (mock the response) and tests for errors 401, 402 and 503.

## 4. Pipeline wiring

> Wire the voice module into my video pipeline behind a `provider` setting, so I can go back to the old voice by changing one line. Use rotation across the approved voices. Apply speed with ffmpeg. Captions use the script text; the transcript is only for word timing.

## 5. Failure safety

> If voice generation fails, retry twice and use the configured fallback voice. Log the reason without printing the key. Do not let the video stop because of this.

## 6. Check

> Generate a short real video with the new voice. Show me the audio and the captions so I can approve before turning on the automatic routine.
