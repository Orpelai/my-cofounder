# Production pipeline

## Stack

Choose the lightest stack that achieves the chosen style:

| Need | Tool |
|---|---|
| General compositions, React, deterministic frames | Remotion (`npx create-video`, `npx remotion still` for keyframes, `npx remotion render` for video) |
| HTML + GSAP overlays, captions, kinetic type | HyperFrames, or Remotion with GSAP timelines driven by frame number |
| 3D scenes | Three.js via `@remotion/three` |
| Shader transitions / glitch | GLSL (gl-transitions) in a WebGL canvas |
| Depth maps | Depth Anything V2 / MiDaS (Python) |
| Background removal | rembg |
| Beat detection | librosa |
| Assembly, audio mix, verification | FFmpeg / ffprobe |

Investigate current docs on the web when an API is uncertain. If a Chromium/Chrome is already installed (e.g. Claude Code cloud sessions set `PLAYWRIGHT_BROWSERS_PATH`), point Remotion at it with `--browser-executable`; otherwise let Remotion fetch its headless shell. Remotion requires a company license above its free tier — mention it if the user is a company.

All animation must be **frame-deterministic** (derived from the frame number, no `Math.random()` without a seed, no wall-clock timers), otherwise keyframes won't match the final video.

## Hebrew / RTL

- Load a Hebrew font (Heebo, Rubik, Assistant, Secular One for display) and wait for it before rendering.
- `dir="rtl"` on text containers; never reverse strings manually.
- Letter/word staggers start from the right. When splitting Hebrew into spans, split by grapheme (keep niqqud with its letter) and keep final forms (ך ם ן ף ץ) as written.
- Mixed Hebrew + English/numbers: wrap LTR runs in `<bdi>` / `unicode-bidi: isolate`.
- Verify Hebrew visually in keyframes — this is the most common failure.

## Keyframes (Step 2)

- Render one still per scene from the real composition at its most representative frame, at full resolution.
- Build a contact sheet (e.g. `ffmpeg` tile or a simple grid) labeled by scene number and timestamp.
- Overlay the platform safe-zone guides on a copy of the contact sheet so the user can see UI collisions.
- Keyframes and the storyboard are working files: keep them in the scratchpad (or project working folder), not under `assets/`, until approved.

## Voiceover

Ask the user once (during Step 2) which option they want:

1. **User records** the script → they send audio; align scenes to it (adjust durations to the recording, not the reverse).
2. **TTS** → e.g. `edge-tts` Hebrew neural voices (`he-IL-HilaNeural`, `he-IL-AvriNeural`) if network allows, or an AI voice service the user has access to. Tell the user TTS Hebrew quality is acceptable but not human-level, and check pronunciation of names/brand words.
3. **No voice** → captions + music only.

Script rules: ~2.5 spoken Hebrew words per second; first sentence is the hook; last sentence states the CTA verbatim. Always burn in captions matching the actual audio timing.

Music: use only user-supplied, royalty-free with a clear license, or generated tracks. Never pull copyrighted music. Duck music under voice (~-18 dB under VO).

## Verification

Before reporting completion:

```bash
ffprobe -v error -show_entries stream=codec_type,codec_name,width,height,r_frame_rate -show_entries format=duration -of compact out.mp4
ffmpeg -y -ss 1 -i out.mp4 -frames:v 1 check-01.png   # also mid and end
```

Check: duration within ±1s of plan, resolution/ratio match, 30fps, audio stream present when expected, Hebrew correct and not reversed, text inside safe zones, CTA visible on the end card, no blank/black frames at start. Inspect the extracted frames visually.

## Delivery

- Final file: `assets/generated/<YYYY>/<YYYY-MM-DD>-<topic-slug>/<topic-slug>-<ratio>.mp4` plus `<filename>.metadata.md` per `assets/README.md` (payload is git-ignored; the sidecar is tracked).
- Composition source: a normal project folder outside `assets/` (or the scratchpad for one-offs). Do not commit `node_modules` or renders.
- Deliver the video (send/attach where the host supports it) and always give the absolute path.

## Host compatibility

The skill is host-neutral. Paths: canonical source `skills/motion-graphic/`; Claude Code discovers it via `.claude/skills/motion-graphic`, Codex via `.agents/skills/motion-graphic` (both symlinks).

| Concern | Claude Code | Codex |
|---|---|---|
| Invoke | `/motion-graphic` or automatic by description | `$motion-graphic` or automatic by description |
| Asking the user | `AskUserQuestion` if available, else a chat message | Chat message, then end the turn |
| Showing keyframes / video | Send the files (e.g. `SendUserFile`) or view them with `Read` | Give absolute paths; inspect images with the image-view tool if available |
| Network (npm, pip, TTS, fonts) | Governed by the environment's network policy | Sandbox may block network — request approval/escalation for installs, or ask the user to run them |
| Long renders | Run in background where supported | Run in foreground with progress; keep resolution/duration per plan |

Rules for both: never rely on a host-only tool without a fallback; never proceed past a gate without an explicit user reply; verify the final file with ffprobe and extracted frames regardless of host.
