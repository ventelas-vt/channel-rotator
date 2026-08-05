# Channel Rotator — Project README

A single-file web app that rotates through a static list of YouTube live
channels, playing each for a per-channel duration, then fading through black
to the next. Loops forever. Zero-distraction fullscreen playback.

**Cross-device by design** — plain HTML + YouTube IFrame API. The same file
runs in any modern browser: Fire TV (Silk), iPad/tablet (Safari/Chrome),
laptop/desktop (any browser, F11 for fullscreen), Android TV/phone (Chrome).

## Files
- `channel_rotator.html` — the whole app (edit the channel list at the top)

## Use
Edit the `CHANNELS` array near the top:
```js
const CHANNELS = [
  { url: "https://www.youtube.com/watch?v=jfKfPfyJRdk", seconds: 60 },
  { id: "VIDEO_ID_ONLY", seconds: 30 },   // raw ID form also works
];
```
- Accepts full URLs (`watch?v=`, `youtu.be/`, `/live/`, `/embed/`) or a raw ID.
- `seconds` is per channel.

`CONFIG` block (below the list): `loopForever`, `fadeMs`, `defaultSeconds`, `muted`.

## Run
- Any browser: open the file/URL, go fullscreen.
- Fire TV Stick 4K (B0C6W3D4RM): host at an HTTPS URL (Netlify Drop / GitHub
  Pages), install Amazon Silk Browser, open the URL.

## Controls
- Right arrow / OK / Enter — next channel now
- `i` — toggle status chip

## How the transition works
Two stacked players (A/B). Next channel is pre-loaded in the hidden player
before the fade, so it's already running when the black overlay fades up — no
reload flash. Auto-skips if a stream ends/errors.

Device note: Fire TV Stick 4K 2nd gen is memory-constrained (~2 GB RAM). Keep
to one visible + one pre-loading player (as the app does).

## Caveats
- Ads: YouTube embeds may show ads on some streams (can't be blocked like
  SmartTube). Music/lofi channels usually have none.
- Some channels block embedding and won't play — swap those out.

## Backlog
- [ ] Test a real channel list, flag any that block embedding
- [ ] Wrap into an installable Fire TV app (WebView/Cordova + ADB sideload)
- [ ] On-screen channel name/number label
- [ ] Remote-friendly menu (pause, jump to channel N)
- [ ] Netlify/GitHub Pages hosting walkthrough

*Targeted first: Fire TV Stick 4K Select / 2nd gen (2023), Fire OS 8. Also
runs on tablets, iPad, laptops, and other TVs.*
