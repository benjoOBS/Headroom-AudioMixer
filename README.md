# Headroom

A light mixing & recording console that runs entirely in the browser — no install, no plugins. Reads a multichannel USB interface (Behringer XR18 and others), mixes with per-track EQ, pan, and a mastering limiter, and exports multitrack WAV recordings.

**Live app:** `https://<your-username>.github.io/<your-repo>/headroom.html` (fill in once GitHub Pages is enabled — see below)
**Manual:** `https://<your-username>.github.io/<your-repo>/manual.html`

## Features (current build — phase 1)

- Reads any class-compliant USB audio interface, split into individual channels so multiple tracks can each listen to a different input of the same device
- Per-track channel strip: trim, pan, 3-band EQ, custom fader with a real console taper, peak meter with clip indicator
- Mute / solo (solo-in-place) / record-arm per track
- Master bus with a limiter (−1dB ceiling) and its own meter
- Output device switching (Chrome/Edge only — a browser limitation, not an app one)
- Multitrack recording — every armed track plus a master reference mix, exported as downloadable WAV files
- Live device list refresh if you plug in an interface after the page is already open

Not in this build yet: a full effects library beyond the built-in 3-band EQ, presets, parallel/aux-send routing, a mastering bus beyond the safety limiter, and 3rd-party plugin hosting. These are planned for later phases.

## Requirements

- Must be served over `http://` or `https://` — opening the file directly (`file://`) will not work, since browsers block the audio engine module in that context.
- Chrome or Edge for the full feature set (including output device switching). Firefox and Safari work for input, mixing, and recording, but can't switch the output device in-app — use your OS sound settings for that.
- Microphone/audio permission, granted on power-on.

## Hosting on GitHub Pages

1. Push `headroom.html`, `manual.html`, `README.md`, and `.gitignore` to this repo, all in the same folder.
2. In the repo's **Settings → Pages**, set the source to the branch/folder these files live in.
3. Once published, open `headroom.html` at the `github.io` URL GitHub gives you — that's the link to share and to fill in above.

The **Manual** button inside the app links to `manual.html` with a relative path, so as long as both files stay in the same folder, the link works without any further setup.

## Running locally for development

```
python3 -m http.server 8000
```

Then open `http://localhost:8000/headroom.html`. `localhost` counts as a secure origin, so the audio engine and microphone access both work the same as they would when hosted.

## Notes on multichannel interfaces (e.g. XR18)

Headroom can only see the channels your operating system has already negotiated with the interface. If a multichannel device only shows 2 channels in the app, check the device's format/channel settings in your OS's sound control panel first — this is an OS-level setting, not something the app controls.
