# VOICE.SCRIBE
### Live Speech Transcription

A lightweight, browser-native voice transcription tool with a real-time waveform visualizer, multi-language support, and continuous-mode recording — no backend, no API keys, zero dependencies.

---

## Features

- **Real-time transcription** — Words appear as you speak using the Web Speech API
- **Continuous mode** — Auto-restarts every 9 seconds to bypass Chrome's session timeout; never drops a word
- **Interim results** — See in-progress words before they're finalized (toggleable)
- **Watchdog timer** — Detects frozen recognition and self-heals every 5 seconds
- **Exponential backoff restarts** — If a session fails, retries with doubling delay (capped at 10s)
- **Lost-word recovery** — Commits unfinished interim text before any restart so nothing is lost
- **Multi-language** — Supports 11 languages/locales out of the box
- **Word & character count** — Live stats below the transcript
- **Copy to clipboard** — One-click copy of the full transcript
- **CSS waveform visualizer** — Pure CSS animation, no `getUserMedia` calls on restart (avoids repeated permission prompts)
- **Zero dependencies** — Single HTML file, no npm, no build step

---

## Tech Stack

| Layer | Technology |
|---|---|
| Speech | Web Speech API (`SpeechRecognition`) |
| Fonts | Syne (headings) + Space Mono (mono UI) via Google Fonts |
| Styling | Vanilla CSS with CSS custom properties |
| Logic | Vanilla JS (ES6+) |
| Build | None — open `index.html` and go |

---

## Browser Support

| Browser | Support |
|---|---|
| Google Chrome | ✅ Full |
| Microsoft Edge | ✅ Full |
| Safari (macOS/iOS) | ⚠️ Partial (no continuous mode) |
| Firefox | ❌ Not supported |

> The app detects unsupported browsers and shows a fallback message.

---

## Usage

1. Open `index.html` in Chrome or Edge
2. Click **Start Listening** and allow microphone access when prompted
3. Speak — transcript appears in real time
4. Click **Stop** to end the session
5. Use **Copy Text** to copy the full transcript to your clipboard
6. Use **Clear** to reset

### Settings

| Option | Description |
|---|---|
| Language | Select from 11 supported locales |
| Continuous mode | Auto-restarts the session to record indefinitely |
| Show interim | Toggles display of in-progress (not yet finalized) words |

---

## Supported Languages

- English (US / UK / India)
- Hindi / Hinglish
- Spanish
- French
- German
- Japanese
- Chinese (Simplified)
- Arabic
- Portuguese (BR)

---

## How Continuous Mode Works

Chrome's `SpeechRecognition` has an undocumented ~10-second session cap. VOICE.SCRIBE works around this with three layers:

1. **Session timer** — Proactively aborts the session at 9s before Chrome kills it
2. **`onend` restart** — Immediately schedules a new session via `scheduleRestart(150ms)`
3. **Watchdog** — A 5-second interval checks if the last result was >20s ago and force-restarts if frozen

Unfinished interim text is committed to the final transcript on every `onend` event so no spoken words are lost during restarts.

---

## File Structure

```
index.html   # Entire app — HTML, CSS, and JS in one file
README.md
```

---

## License

MIT — free to use, modify, and distribute.