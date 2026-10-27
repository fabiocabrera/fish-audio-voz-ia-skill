# Architecture

## Goal

Replace the default AI narration (a robotic-sounding voice) with a human-sounding voice, without rewriting your video system: only the "text becomes audio" step changes.

## Main flow

```
script (text per scene)
   -> [voice module]  text + voice id -> Fish Audio API -> MP3
   -> speed adjustment (ffmpeg atempo)
   -> per-word timing (transcription, e.g. Whisper) for captions
   -> video assembly (clips + captions + music)
   -> final MP4
```

## Design decisions

- **One module for the voice.** A function `generateVoice(text, voiceId, config)` that returns audio. The rest of the system does not know which service is behind it.
- **Provider by configuration.** A field (`provider: "fish"`) in each brand's or client's config decides which service narrates. Going back is a one-line change, with no new code deploy.
- **Voice rotation.** A list of voice ids; the item index picks one (alternate male and female, for example).
- **Speed is separate from the voice.** Fish delivers a natural pace; for short video, speed it up slightly with ffmpeg `atempo` (1.1 was a good starting point). Too much speed brings the "robot" back.
- **Captions from the script.** Use the script text for captions and the transcript only for word timing. Transcription mishears words; the script does not.
- **Plan for failure.** Retry once or twice and keep a fallback voice configured. A video delayed by an outage is worse than a video with the old voice.
- **Key outside the code.** An environment variable on the server, a local file outside the repository on your computer.

## Suggested stack

Node.js (or any language with HTTP), `ffmpeg` for speed and mixing, a transcriber with per-word timing, and the video renderer you already use.
