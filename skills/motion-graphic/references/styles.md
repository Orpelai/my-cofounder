# Style catalog

Each style: fit signals, key effects, render spec, risk. Use the render spec as the core of the composition brief in Step 2. Pick by fit, not by novelty.

## Selection heuristics

| Goal / context | Strong candidates |
|---|---|
| Maximum "wow" from photos | 2.5D Parallax, 3D Hybrid |
| One sharp message, short-form reel | Kinetic Typography, Brutalist |
| Personal brand, authentic, story | Collage/Cutout, Retro Film |
| B2B, professional, LinkedIn | Swiss/Bauhaus, Data-viz, Apple-style |
| Tech / AI / product | Liquid Glass, Glitch, Apple-style |
| Launch / announcement | Apple-style, Kinetic Typography |
| Explaining a process or concept | Hand-drawn/Doodle, Swiss |
| Results, numbers, case study | Data-viz |

Image constraints: no images → typography-led styles (1, 4, 9, 10, 12). Few (1–3) strong photos → 2, 8. Many (8+) → 11, 3. Busy backgrounds / hair → avoid heavy cutouts and depth layering, or warn.

Combine at most: one main style + one effect from another style.

---

## 1. Kinetic Typography
- **Fit:** one strong message, quotes, promos, muted viewing.
- **Effects:** scale-slam, letter stagger, word stretch, split-and-reassemble, 3D-axis rotation, variable-font weight morph, beat-synced hits.
- **Spec:** Text is the hero; images only inside text masks or brief full-bleed flashes. Message broken into 4–6 punchy phrases, each with a unique typographic behavior. Huge type (70%+ of frame), 2 colors + 1 accent. Sync word hits to music beats (librosa beat timestamps).
- **Risk:** long text kills it. Hebrew letter stagger must run right-to-left.

## 2. 2.5D Parallax
- **Fit:** strong photos, cinematic mood, personal or place-based stories.
- **Effects:** depth-map layering (Depth Anything V2 / MiDaS), inpainted gaps, dolly-in/orbit camera, fog between layers, dust particles, foreground bokeh, push-through transitions, text placed between depth layers.
- **Spec:** Per image: depth map → 3–4 layers → inpaint behind foreground → slow camera move with true parallax. Cohesive cinematic grade, light grain. One short line of text per scene.
- **Risk:** tearing on hair/complex edges; heavy compute. Needs clear subject/background separation.

## 3. Collage / Paper Cutout
- **Fit:** personal brand, authenticity, "made by a human" feel (anti-AI-polish trend).
- **Effects:** background removal (rembg), white paper borders, torn edges, tape strips, scribbles, halftone, magazine-cutout letters, marker underlines drawing on, stop-motion "on twos" with jitter.
- **Spec:** Animate at 12fps-feel (hold frames) inside 30fps output, small random jitter, elements slap on with bounce + rotation. Paper/cardboard background.
- **Risk:** too-smooth motion breaks the illusion; cutout quality depends on photos.

## 4. Swiss / Bauhaus geometric
- **Fit:** B2B, professional, frameworks, clean explanations. Safest result.
- **Effects:** mask reveals (circle/rect/bar wipes), 12-column grid, primary shapes, oversized numbers, overshoot springs.
- **Spec:** Off-white + black + one bold accent. Images only inside geometric masks. Generous negative space, perfect alignment, bold sans.
- **Risk:** can feel cold — one strong accent color fixes it.

## 5. Liquid Glass / Glassmorphism
- **Fit:** tech, AI, apps, innovation, premium SaaS.
- **Effects:** frosted cards with backdrop blur, refraction, edge highlights, morphing mesh gradients, specular sweeps, liquid shader transitions, 3D drift/tilt.
- **Spec:** Glass cards floating over slow gradients (deep blue/violet/cyan); images inside cards; light-weight high-contrast type.
- **Risk:** blur is render-expensive — limit to 2–3 glass layers.

## 6. Y2K / Glitch / Cyberpunk
- **Fit:** young audience, hype, launches, high energy.
- **Effects:** RGB split, scanlines, datamosh smear, pixel sort, CRT curvature, chromatic aberration, scramble/decode text, glitch-in/out transitions.
- **Spec:** Neon magenta/cyan/acid green on near-black. Fast beat cuts with 2 calm 0.5–1s breathing moments. GLSL shaders.
- **Risk:** visual fatigue; avoid for serious or B2B topics. Avoid rapid full-frame flashing (photosensitivity).

## 7. Retro Film / VHS
- **Fit:** origin stories, journeys, nostalgia, "how it started".
- **Effects:** 16mm grain, gate weave, light leaks, dust/scratches, vignette, faded warm grade, polaroid/slide framing, projector flicker, typewriter text, film-burn transitions.
- **Spec:** Images as film frames/polaroids; typewriter type-on; optional VHS segments with tracking lines.
- **Risk:** reads as a cheap filter if the topic has no time/story dimension.

## 8. Apple-style Premium Reveal
- **Fit:** launches, product, premium positioning, one big idea.
- **Effects:** light-sweep reveals, rising spotlight, blur-to-sharp type, very slow camera, long holds, subtle glow end card.
- **Spec:** Pure black, single-source lighting, one statement per scene, 2–3s holds, minimal building music. Restraint over gimmicks.
- **Risk:** one weak image ruins it; needs strong visuals or pure typography.

## 9. Data-viz Motion
- **Fit:** results, case studies, before/after, proof.
- **Effects:** rolling counters, bars/lines drawing on, filling rings, split comparisons, pulsing hero number.
- **Spec:** Use only user-supplied or cited numbers. Images as darkened context backgrounds or icons. One highlight color for the key number; climax on the most impressive number.
- **Risk:** without real data, do not use this style.

## 10. Hand-drawn / Doodle
- **Fit:** explaining a process, education, workshops.
- **Effects:** SVG stroke draw-on (stroke-dashoffset), wobbly marker lines, circles/arrows annotating photos, handwritten notes, step-by-step build.
- **Spec:** Off-white textured paper, black ink + 1–2 marker colors, one idea per scene.
- **Risk:** without clear structure looks childish.

## 11. 3D Hybrid (Three.js)
- **Fit:** galleries, many images, tech "wow".
- **Effects:** images as 3D cards with thickness and soft shadows, camera fly-through (spiral/tunnel/wall), zoom-into-card scene changes, depth of field, particles, glossy floor reflections, 3D text planes.
- **Spec:** Three.js rendered deterministically frame-by-frame (Remotion `@remotion/three` or headless capture).
- **Risk:** most complex; longest render; insist on keyframe gate.

## 12. Brutalist / Bold Type
- **Fit:** provocative message, scroll-stopping reels.
- **Effects:** frame-overflowing condensed type, hard jump cuts, abrupt scale changes, duotone 4–6 frame image flashes, grid lines, crop marks, monospace labels, 01/02/03 numbering.
- **Spec:** Black/white + one aggressive color (#FF3B00 / acid yellow), synced to a hard beat.
- **Risk:** wrong for soft or warm brands.

---

## Cross-style effect library

- **Images:** depth parallax, background-removal pop-out, particle shatter/dissolve, GLSL transitions (gl-transitions: ripple, burn, morph), upgraded Ken Burns with motion blur.
- **Text:** split-letter stagger (RTL order for Hebrew), mask reveal, variable-font morph, scramble/decode.
- **Transitions & rhythm:** match cut, whip pan / zoom-through, beat sync, spring/custom-bezier easing (never linear).
