# Pixel Lobster

A pixel art lobster that lives on your desktop and lip-syncs to audio. Built with Electron.

```
git clone https://github.com/JoeProAI/pixel-lobster.git
cd pixel-lobster
npm install
npm start
```

## Features

- 120px pixel art lobster rendered on a transparent overlay
- 6 distinct mouth shapes (visemes) for natural lip sync
- Spring physics jaw with syllable detection
- Swims around your screen like a fish tank
- Click-through mode (F9) so it doesn't block your desktop
- Two audio modes: system audio or TTS server

## Audio Modes

### System Audio (default)

Captures your system's audio output and lip-syncs to everything -- music, voice calls, games, videos. Just start the app and click to begin audio capture.

### TTS Server Mode

For use with a TTS server (like XTTS, OpenAI-compatible, or [OpenClaw](https://github.com/openclaw/openclaw)). The lobster polls an envelope endpoint and only moves its mouth when speech is detected. Music and other audio are ignored.

Set `"audioMode": "tts"` in `config.json` and configure `ttsUrl` to point at your server.

**Required server endpoint:** `GET /audio/envelope` returning:
```json
{
  "id": 1,
  "envelope": [0.1, 0.4, 0.8, 0.6, ...],
  "elapsedMs": 1200,
  "intervalMs": 50
}
```

## Configuration

Edit `config.json`:

| Key | Default | Description |
|-----|---------|-------------|
| `audioMode` | `"system"` | `"system"` for all audio, `"tts"` for TTS-only |
| `ttsUrl` | `"http://127.0.0.1:8787"` | TTS server URL (tts mode only) |
| `ttsEnvelopePath` | `"/audio/envelope"` | Envelope endpoint path |
| `ttsPlayStartOffsetMs` | `1100` | Delay for audio playback startup |
| `monitor` | `"primary"` | `"primary"`, `"secondary"`, `"left"`, `"right"`, or index (0, 1, 2) |
| `lobsterScale` | `4` | Sprite scale (4 = 480px lobster) |
| `alwaysOnTop` | `true` | Keep lobster above other windows |
| `clickThrough` | `false` | Start in click-through mode |
| `swimEnabled` | `true` | Enable swimming animation |
| `swimSpeed` | `1.0` | Swimming speed multiplier |

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| F9 | Toggle click-through mode |
| F12 | Toggle DevTools |

## Viseme Shapes

The lobster has 7 mouth states driven by audio analysis:

- **X** -- Closed (flat line)
- **A** -- Wide open "ah" (tongue + corner teeth)
- **B** -- Wide grin "ee" (tooth row)
- **C** -- Round "oh" (circular opening)
- **D** -- Small pucker "oo"
- **E** -- Medium "eh" (tongue peek)
- **F** -- Teeth bite "ff" (teeth + gum + lower lip)

## Using with OpenClaw

If you use [OpenClaw](https://github.com/openclaw/openclaw) with local XTTS, set:

```json
{
  "audioMode": "tts",
  "ttsUrl": "http://127.0.0.1:8787"
}
```

The lobster will only animate when your AI agent speaks.

## License

MIT
