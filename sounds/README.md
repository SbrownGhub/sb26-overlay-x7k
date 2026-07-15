# Sounds Folder — What Goes Here

The overlay expects exactly these four files, named exactly this way (lowercase, .mp3):

| Filename | Fires when | What to look for |
|---|---|---|
| `win.mp3` | WIN flash (green) — challenge completed, contestant saved | Triumphant sting or rising chime, 1–2 seconds. Think game-show "correct answer" |
| `lose.mp3` | LOSE flash (red) — elimination, failed challenge | Descending buzzer or dramatic hit, 1–2 seconds. Think "wrong answer" klaxon |
| `cash.mp3` | Cash burst — prize moments, money on screen | Coins, register cha-ching, or money-counter riffle, 1–2 seconds |
| `penalty.mp3` | Every -$ penalty hit — buzzes, falls, wrong flips | Short, sharp, punchy — a single buzz or metallic hit, UNDER 1 second. This one fires dozens of times per day; if it's long or annoying, the whole room will hate it by Room 2 |

## Rules that matter

1. **Names must match exactly** — `Win.mp3` or `win.MP3` will silently fail. Lowercase everything.
2. **MP3 format.** WAV works in most browsers but MP3 is the safe universal choice for OBS/StreamLabs' embedded browser.
3. **Keep them SHORT.** The penalty sound especially — it needs to land and get out of the way before the next one fires.
4. **Normalize the volume across all four** before committing. A quiet win sting next to a deafening penalty buzz sounds amateur on stream. Aim for consistent loudness (drop them all into any editor — even QuickTime/GarageBand — and level-match by ear).
5. **Copyright: use royalty-free only.** This stream goes out on YouTube, which WILL Content-ID match copyrighted audio and can mute or strike the broadcast. Safe sources:
   - pixabay.com/sound-effects (no attribution needed)
   - freesound.org (check each file's licence — CC0 is safest)
   - zapsplat.com (free with account)

   Search terms that work: "game show correct", "buzzer wrong answer", "cash register", "coin drop", "error buzz short".

## Testing

Open `overlay.html` in a normal browser tab after adding the files, then fire each button from `control.html` — every effect should make its sound. If one is silent, it's almost always a filename mismatch. Then test again inside StreamLabs: right-click the Browser Source → ensure "Control audio via OBS" is ON and the source is routed to your stream mix, or sounds will play on the PC but never reach the broadcast.
