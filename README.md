# 🌙 Santa — Sleep Tracker

A PWA sleep tracker that installs like a native app on your Android phone.
Detects snoring, tracks sleep stages via motion, and logs your noise environment — all stored privately on your device.

---

## Features

| Feature | How it works |
|---|---|
| 🎙️ Snore detection & recording | Microphone + frequency analysis (80–500 Hz band) |
| 📊 Sleep stage graph | Accelerometer movement → Awake / Light / Deep / REM |
| 🔊 Noise environment | Continuous dB level logging throughout the night |
| 💤 Morning report | Sleep score, hypnogram, snore playback, noise chart |
| 📅 Sleep history | Tap any past night to review its full report |
| 📴 Offline | Works without internet after first load |

---

## Deploy to GitHub Pages (free)

1. **Create a new GitHub repository** (e.g. `santa-sleep`)
2. **Upload all 4 files** into the repo root:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icon.svg`
3. Go to **Settings → Pages → Source → main branch → / (root)** → Save
4. Your app URL will be: `https://yourusername.github.io/santa-sleep/`

---

## Install on Android (Samsung Galaxy)

1. Open the URL above in **Chrome**
2. Tap the **three-dot menu → "Add to Home screen"**
3. Tap **Add** — it will appear as an app icon on your home screen
4. Open it from your home screen (it runs full-screen, no browser UI)

---

## How to Use

**Before bed:**
- Open Santa from your home screen
- Tap **Begin Sleep Session**
- Allow microphone access when prompted
- Place your phone **face-down** on your nightstand within ~1 metre of your head
- Keep it **plugged in** (the screen stays on all night to keep the session alive)

**In the morning:**
- Tap the **■ stop button** to end the session
- Your **Sleep Report** opens automatically with:
  - Sleep score (0–100)
  - Sleep stage graph (hypnogram)
  - Snore recordings you can play back
  - Noise environment log

---

## How Sleep Stages Work

Santa uses your phone's accelerometer (the same sensor apps like Sleep Cycle use):

| Movement | Stage |
|---|---|
| High (MAD > 0.28) | Awake |
| Medium (MAD 0.08–0.28) | Light Sleep |
| Low (MAD < 0.08) | Deep Sleep |
| Low + 90+ min asleep | REM (estimated) |

> **Note:** Phone-based sleep staging is an estimate — the same method used by consumer sleep apps. For clinical accuracy, a sleep lab is needed.

---

## Privacy

- All data stays **on your device** (IndexedDB)
- No account, no cloud, no ads
- Snore recordings are stored locally and can be played back in-app
- Microphone is only active during an active session

---

## Known Limitations

- **Background audio:** Chrome may pause tracking if the phone screen locks. This is why the app keeps the screen on with Wake Lock. Place the phone face-down to reduce light.
- **Heart rate:** Not available via browser (requires native app or wearable)
- **Motion accuracy:** Phone must be on the mattress (not a bedside table) for accelerometer motion to reflect your body movements

---

## Tech Stack

- Vanilla JS + HTML/CSS (no framework, no build step)
- `getUserMedia` + Web Audio API — microphone & snore detection
- `MediaRecorder` — audio clip capture
- `DeviceMotionEvent` — accelerometer / sleep stages
- `Screen Wake Lock API` — keep session alive overnight
- `IndexedDB` — local data storage
- Service Worker — offline support
- PWA manifest — installable as home screen app
