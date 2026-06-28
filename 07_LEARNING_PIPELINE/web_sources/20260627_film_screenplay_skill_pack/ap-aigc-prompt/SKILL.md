---
name: ap-aigc-prompt
description: Create production-ready AIGC video storyboard prompts for Seedance and GPT-Image-2. Use when the user asks for AIGC video prompts, Seedance prompts, cinematic分镜, 镜头拆解, five-dimensional shot prompts, scene/character/prop asset extraction, role-reference images, keyframe/first-frame/last-frame prompts, mask transitions, prompt cleanup, or converting scripts, IP references, metaphors, emotions, or abstract concepts into camera-readable visual instructions.
---

# AP-AIGC-prompt

Use this skill to turn scripts, scenes, or abstract ideas into practical AIGC video production prompts. Prefer Chinese output unless the user asks for another language.

Before producing any Seedance, GPT-Image-2, first/last-frame, character-locking, continuity, QA, or final file-delivery prompt, read `references/model-rules.md`.

## Workflow

1. Identify the deliverable:
   - **Storyboard**: shot table or copy-friendly shot blocks with purpose, duration, camera, action, light, sound, and continuity.
   - **Seedance prompt**: moving-clip text written as continuous prose after style lock.
   - **GPT-Image-2 prompt**: character reference, keyframe, first frame, last frame, or still-composition correction.
   - **Production package**: `.txt` prompt files with pure English filenames.
2. If the user is brainstorming, offer 2-3 directions and wait before writing many full prompts.
3. If the user gives a script and asks to test or proceed, do not over-ask. Make reasonable assumptions and state them briefly.
4. Extract assets before designing shots: character/creature, scene, prop/equipment, VFX, audio, and continuity states.
5. Translate metaphors, memes, IP references, director references, emotions, and abstract words into visible camera behavior before they enter prompts.
6. Keep the project first: choose style, pacing, shot size, duration, and visual strategy from the genre, audience, runtime, and emotional arc.
7. Draft the storyboard or prompts, then run the relevant self-check from `references/model-rules.md`.
8. For final prompt delivery, write actual `.txt` files with English filenames and give the user the paths.

## Asset Extraction

For script-to-storyboard work, create an asset layer before writing shots. Use it to prevent visual drift and support later reference-image or production-prompt generation.

### Character / Creature Assets

Extract each recurring character or creature as a reusable visual asset:

- identity: name, role, age/scale/species, body silhouette
- face/head: hair, eyes, helmet, mask, horns, sensory organs, scars, skin/shell texture
- costume/body: clothing, armor, material, damage state, color system
- motion logic: fighting style, gait, posture, micro-performance, weight
- light signature: eye glow, weapon glow, armor circuit, biological glow
- continuity state: wound, dust, wet/dry, broken parts, weapon position

### Scene Assets

Extract every reusable location as a scene asset, not just a background:

- location name and story function
- geography and scale: horizon, elevation, landmarks, travel direction
- architecture/nature: rock, ruin, vegetation, machinery, terrain material
- atmosphere: weather, dust, smoke, mist, heat shimmer, visibility
- lighting: time of day, sun/moon direction, practical sources, color temperature
- continuity anchors: fixed objects, entrances/exits, repeated occluders, distance between characters
- style locks: cinematic reference, palette, texture, lens/depth behavior

### Prop / Equipment Assets

Extract props that affect action, identity, or continuity:

- weapon/tool name and owner
- silhouette and scale relative to the body
- material, color, damage state, moving parts
- energy/VFX behavior: charge, glow, heat, recoil, particle trail, cooldown
- sound signature: click, hum, blade scrape, hydraulic release, impact tone
- continuity state: loaded/unloaded, folded/unfolded, broken, stained, attached/dropped

### Shot-Level Asset Tags

When writing a copy-friendly storyboard, put asset tags in every shot block when useful:

```text
Scene Assets: [location / terrain / fixed landmarks / atmosphere]
Prop Assets: [weapons / armor modules / HUD / creature parts / practical objects]
```

Use these tags to make each shot independently copyable without losing what needs to remain visually consistent.

## Storyboard Output

For a script-to-storyboard request, produce a compact table unless the user asks for a different format:

| Shot | Duration | Visual Purpose | Camera | Action | Light / Atmosphere | Sound | Generation Notes |

For copy-friendly cinematic scripts, prefer one block per shot:

```text
## Shot 01
Shot:
Duration:
Visual Purpose:
Scene Assets:
Prop Assets:
Camera / Cinematography:
Action:
Light / Atmosphere:
Sound:
Generation Notes:
```

Keep each shot executable. Avoid vague labels such as "epic", "高级感", "压迫感", or named IP shorthand unless translated into visible scale, posture, lensing, motion, texture, and lighting.

Add continuity notes when clips must connect:
- entering/exiting direction
- body position at cut points
- shared occluder or mask object
- first-frame/last-frame dependency
- props, costume, wet/dry, damage, dirt, blood, smoke, or debris state

## Seedance Prompt Pattern

Use Seedance for moving clips. Write the prompt as continuous prose after a short style lock.

Required content:
- style lock: cinematic reference, film stock/lens language, real texture, aspect ratio, and light quality
- visible character anchors: `@[character_id]` only when reference images exist
- camera: start/end position, movement type, speed, angle, what/who the camera follows or circles
- action: executable body motion, direction, strength, timing
- light: source, hardness, contrast, color temperature, changes across the shot
- expression: eye direction and facial state, without redefining locked facial features
- details: hair, fabric, water, sand, sparks, grass, dust, foreground/midground/background
- sound: embed environmental/action sounds alongside the corresponding movement; avoid standalone sound blocks

For Seedance, only describe what is visible in the current shot. Keep unwanted things absent from the text instead of naming them. Do not use negative anchors, offscreen objects, meta-continuity words, or CG/3D/render language for live-action realism.

## GPT-Image-2 Prompt Pattern

Use GPT-Image-2 for character references, keyframes, first frames, last frames, and still composition fixes.

Use this structure:

```text
[Image prompt - title]
If based on a reference character, use the provided reference only to lock face and identity. This prompt controls composition, pose, light, and environment.

# CHANGE
...

# PRESERVE
...

# CONSTRAINTS
...
```

Put every identity-critical feature in `PRESERVE`: face, hair, costume, material, expression, body type, scars, props, and any visible state that must not drift.

## Collaboration Rules

Be direct. If an idea is weak or average, say so plainly and suggest the better production path. Do not cushion with automatic praise.

Translate rather than transcribe. User phrases like "像某个IP", "某导演那种", "宿命感", "高级感", or "猫和老鼠那样" must become concrete camera-readable visuals, actions, staging, light, texture, and motion.

Avoid speculative model-risk warnings. Warn only from verified experience or when the requested operation is a known weak area such as precise speed ramps, dolly zoom, major camera flips, complex cross-environment dissolves, or exact multi-point geometry.

When the user shows emotional strain or gets stuck, pause lightly and ask whether to continue or rethink. If they say continue, continue.
