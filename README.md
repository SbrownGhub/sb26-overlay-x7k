# Speed Build 2026 — Stream Overlay System

Live overlay graphics for the Speed Build 2026 broadcast: draining prize pot, per-room round timer, win/lose flashes, cash burst, penalty hits — all controlled remotely from any phone or laptop via a web control panel.

## Files

- `overlay.html` — the overlay. Loads in OBS/StreamLabs as a Browser Source. Transparent background, renders over the video.
- `control.html` — the remote control. Open on any device, anywhere. Buttons for pot, timer, penalties, effects.
- `sounds/` — sound effects (see `sounds/README.md` for exactly what to add and where to source it).

## Setup — once

### 1. Ably key
Both files have this block near the bottom:
```js
const ABLY_API_KEY = 'YOUR_ABLY_KEY_HERE';
const CHANNEL_NAME = 'speedbuild-overlay-v2';
```
Create a free app at ably.com, make an API key restricted to the `speedbuild-overlay-v2` channel with publish + subscribe capability, and paste the same key into **both** files.

> Note: the key is visible in this repo once pushed. Keep the repo obscurely named and the control URL private — or for proper security, proxy publishes through a serverless function so the key never ships client-side.

### 2. GitHub Pages
Repo → Settings → Pages → deploy from `main` branch, root folder. You get:
- `https://<user>.github.io/<repo>/overlay.html` → StreamLabs
- `https://<user>.github.io/<repo>/control.html` → your phone

### 3. StreamLabs Browser Source
- URL: the overlay.html Pages link
- Size: 1920 × 1080 (match canvas)
- **Untick** "Shutdown source when not visible"
- **Untick** "Refresh browser when scene becomes active"
- Right-click source → "Control audio via OBS" ON, routed to stream mix

### 4. Phone control
Open control.html on the phone → Share → Add to Home Screen. Disable auto-lock for show day. Keep the phone on 4G/5G so control survives venue wifi problems.

## Show-day quick reference

| Action | Where |
|---|---|
| Set pot to $20,000 | Control panel → Set |
| Start the drain (clock reveal moment) | Set $/min rate → Start Drain |
| Penalty (-$50 buzz) | Red -$50 button — mash-safe |
| Custom penalty | Amount field → -Custom |
| Freeze pot (finale) | Pause |
| Room timer | Label + minutes → Start Round |
| Win/Lose/Cash effects | Bottom row |

## How it survives failures

The control panel is the single source of truth and publishes full state on every change. The overlay replays the last state on any (re)connect — so refreshing the browser source, restarting StreamLabs, or a second venue coming online mid-show all recover the correct pot value and timer automatically. If the control phone dies, open control.html on any other device: it picks up current state and carries on.
