---
name: motion-graphic
description: Turn a topic, core message, CTA and target platform into a motion-graphic video. Recommends 3 fitting visual styles with effects and Hebrew rationale, asks for platform/aspect ratio when missing, renders real keyframes plus a voiceover script for approval, and only then renders the full video. Use when the user asks for a motion graphic, animated video, reel/short from a topic or images, "מושן גרפיק", "סרטון אנימציה", or invokes /motion-graphic (Claude Code) or $motion-graphic (Codex).
---

# Motion Graphic

A generic capability skill, not a named worker. Talk to the user in Hebrew (RTL); keep code and render prompts in English.

The flow has three hard gates. Never skip or merge them: **style choice → keyframe approval → full render.** At each gate, end your turn and wait for the user's reply.

Works in Claude Code and Codex. Use whatever tools the host provides; see [host compatibility](references/production.md#host-compatibility) for questions, showing images, network and browser differences.

## Step 0 — Intake

Required inputs: **topic**, **core message** (one sentence), **CTA**, **platform**, **aspect ratio**. Optional: images, brand colors/fonts, duration, voice preference, music, real data/numbers.

- Platform missing → ask for it. Do not guess.
- Platform given but it supports several ratios (e.g. Instagram Reels 9:16 vs feed 4:5, LinkedIn 1:1/4:5/16:9) and no ratio given → ask, with a recommended default from [platforms](references/platforms.md).
- Topic, message or CTA missing → ask in the same message.
- Ask all missing items in **one** message, with a recommendation per item. Never start styling before platform and ratio are confirmed.
- If images were attached, inspect them (subject, background complexity, quality, count). They constrain style choice.
- Numbers on screen must come from the user or a cited source. Never invent statistics.

## Step 1 — Recommend 3 styles

Read [styles](references/styles.md) and [platforms](references/platforms.md). Pick the 3 best-fitting styles for this topic + audience + platform + available images. Present in Hebrew, numbered 1–3, each with:

1. **שם הסגנון** + one-line visual description.
2. **למה זה מתאים** to this topic/message/platform (specific, not generic).
3. **אפקטים מרכזיים** — 3–5 concrete effects from the catalog.
4. **מבנה מוצע** — hook (first 1.5s) → scenes → CTA, in one line.
5. **סיכון / מגבלה** — honest weakness (render time, image requirements, brand fit).

Then mark one as **מומלץ** with a one-line reason, and ask the user to pick a number (they may also combine: one main style + one effect from another — no more). Stop and wait.

## Step 2 — Storyboard, keyframes and voiceover (approval gate)

After the user picks:

1. Write the storyboard: 4–6 scenes, each with timing, on-screen text (Hebrew, ≤6 words on screen), visuals, effects, transition.
2. Write the **voiceover script (טקסט לדובר)** per scene in Hebrew: spoken, natural, ~2.5 words per second, matching scene durations. On-screen text and voiceover complement each other — do not duplicate word-for-word.
3. Build the **actual composition code** (per [production](references/production.md)) and render **real keyframe PNGs** from it — one representative frame per scene — plus a contact sheet. Do not use mockups drawn separately from the video code.
4. Show the user: the keyframes (attach/send the images if the host can; otherwise give their absolute paths and the contact sheet path), and a Hebrew table: `סצנה | זמן | טקסט על המסך | טקסט לדובר | אפקט`.
5. Ask: approve, or what to change (per scene). Ask also how the voice will be produced (see production) if not yet known. Stop and wait.

Iterate on feedback by re-rendering only the changed keyframes. Do not render the full video until the user explicitly approves.

## Step 3 — Full render

After explicit approval:

1. Render the full video with the approved composition, voiceover audio (if chosen) and burned-in captions.
2. Verify per [production](references/production.md#verification): file plays, duration, resolution, fps, audio stream present, Hebrew renders correctly, nothing inside platform UI safe zones. Extract 3 frames from the final file and inspect them.
3. Save under `assets/generated/<YYYY>/<YYYY-MM-DD>-<topic-slug>/` with a `.metadata.md` sidecar per `assets/README.md`. Keep composition source code outside `assets/`.
4. Deliver the video (send/attach it if the host can; otherwise give the absolute path) and report: path, duration, resolution, style, what was verified, and known limitations. Offer one targeted improvement, not a list.

Never claim the video is done without having inspected frames from the final file.
