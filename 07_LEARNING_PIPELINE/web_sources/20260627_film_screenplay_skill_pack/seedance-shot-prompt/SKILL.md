---
name: seedance-shot-prompt
description: Convert, analyze, debug, and rewrite AIGC storyboards into production-ready Seedance 2.0 prompts. Use when the user asks to turn script/storyboard shots into Seedance prompts, build a personal Seedance 2.0 prompt-writing workflow, optimize first-frame image-to-video, first-and-last-frame, reference-image, video-reference, audio-reference, Omni Reference, character-consistency, fixed-camera, timed-beat, Mandarin dialogue, or cinematic live-action video prompts.
---

# Seedance Shot Prompt

Use this skill to turn upstream storyboard output into Seedance 2.0-ready prompts. Default language is Chinese unless the user asks otherwise.

## Core Positioning

Treat this skill as a downstream translator and execution diagnostician:

- Translate upstream storyboard fields into Seedance 2.0 prompt structure.
- Do not rewrite the user's story intention or secretly redesign shots.
- Do flag Seedance execution risks clearly, then offer conservative fixes.
- Prefer stable video generation over literary phrasing.

## Required First Step: Input Mode

Before writing any prompt, identify the Seedance 2.0 input mode and assign reference roles.

Common modes:

1. **Text to Video**: no visual anchor; character consistency is weakest.
2. **Image to Video / First Frame**: one image locks opening composition, subject positions, camera angle, lighting, and crop. Treat it as the strongest visual authority.
3. **First and Last Frame**: first frame locks start state; last frame locks destination state. Keep motion causal between them.
4. **Reference Image / Omni Reference**: images define character, scene, prop, style, or identity, but do not automatically lock frame composition.
5. **Video Reference**: use only for motion, camera behavior, gesture rhythm, or style when explicitly provided.
6. **Audio Reference**: use for voice tone, dialogue identity, sound texture, or music when explicitly provided.

If the user gives ambiguous references, ask for or infer a reference-role table:

```text
@image1 = first frame / character identity / scene / prop / style
@image2 = character identity / expression / costume / last frame
@video1 = motion reference / camera reference / style reference
@audio1 = voice reference / ambient sound / music reference
```

Never invent fake reference IDs such as `{{Character_A}}` unless the user explicitly wants placeholders. Use the user's actual `@image1`, `@video1`, `@audio1`, or platform IDs.

## Upstream Storyboard Intake

When the user provides a storyboard from an upstream skill, extract:

- **Big-shot unit**: event, scene, character positions, emotional direction.
- **Asset bible**: environments, set dressing, props, weapons, vehicles, creatures, costume/equipment states, VFX elements, UI/HUD, and reusable sound motifs.
- **Shot fields**: focal length, aperture/depth, camera position, composition, camera movement, subject action/expression/dialogue, constraints.
- **Continuity card**: costume, hand state, prop state, light, eye line, axis, emotional energy, final state.
- **Global suffix**: audio, no-text rules, lighting, aspect ratio, realism/rendering, color grade.

If the user gives only a script or outline, explain that prompt quality will improve after storyboard conversion. If they still want direct conversion, proceed but label it as lower-control.

## Asset Extraction Pass

Before writing a production storyboard or Seedance prompt from a script, run an asset extraction pass unless the user explicitly asks for a quick draft.

Create an asset bible with stable IDs and short production notes:

| Asset type | ID prefix | Extract |
|---|---|---|
| Environment / location | `ENV` | geography, scale, light behavior, weather, terrain, camera-use constraints |
| Set dressing | `SET` | rocks, furniture, ruins, practical lamps, foreground objects, repeated background pieces |
| Prop / weapon | `PROP` | shape, material, scale, moving parts, light/emission, damage state |
| Vehicle / machinery | `VEH` | silhouette, locomotion, exhaust, lights, cockpit/interface details |
| Creature / monster | `CRE` | scale, anatomy, shell/skin, weak points, movement, attack pattern, injury states |
| Character equipment | `EQP` | armor, costume, helmet/visor, hand state, damage, heat/sand/wetness continuity |
| VFX / atmosphere | `VFX` | dust, smoke, heat shimmer, blood/fluid, explosions, energy, screen-space overlays |
| Audio motif | `SND` | recurring ambience, weapon sound, creature vocalization, UI beep, impact texture |

For each asset, capture: `name`, `description`, `visual anchors`, `scale`, `materials`, `state changes`, `shots used`, and `reference role`. If reference IDs are unknown, use placeholders that can be replaced later, such as `@[REF_ENV_DESERT]`, without inventing fake platform IDs.

After the asset bible, add a shot/sequence asset call sheet:

```text
Shot A01 uses: ENV001 desert, SET001 black rock ridge, VFX001 heat shimmer, SND001 desert wind.
Shot B07 uses: CRE001 mid-tier beast, PROP002 Nicole axe, EQP002 Nicole armor, VFX004 plasma blade, VFX006 sand burst.
```

Use the asset call sheet to keep continuity stable: the same weapon, crack, wound, armor damage, light source, and terrain feature should not randomly change between shots.

## Segmenting for Seedance

Seedance segments should stay within the platform's current duration limits; use 4-15 seconds when no different limit is specified by the user or UI.

Segment rules:

- A single action under 4 seconds should usually merge with a neighboring shot.
- A segment over 15 seconds should split at an emotional or causal beat.
- Do not split a continuous physical action chain.
- Do not split one spoken sentence across segments.
- Treat micro cutaways as timed moments inside a longer segment unless the user wants separate clips.
- Prefer one continuous shot per prompt. If multiple cuts are necessary, label them clearly as `cut to`.

Output a short split plan before the final prompts when multiple segments are involved.

## Prompt Construction Order

Build each Seedance prompt in this order:

1. **Generation Goal**: live-action realism, duration, aspect ratio, no CG/cartoon, whether it is one take or includes cuts.
2. **Reference Inputs**: exact role of each image/video/audio reference. First frame beats ordinary references.
3. **Asset Callout**: list the environment, set dressing, props/weapons, creature, equipment, VFX, and audio motifs used in this segment.
4. **Global Hard Locks**: camera lock, crop, subject positions, foreground/background hierarchy, what cannot move or appear.
5. **Composition and Visibility**: who is sharp, blurred, occluded, offscreen; visible body range; what details are only identity references.
6. **Timed Beats**: `0-3s`, `3-7s`, etc. Use one primary action per beat with explicit causality.
7. **Performance and Motion**: physical, muscle-level action; what touches what; what does not touch.
8. **Dialogue and Audio**: Mandarin dialogue exactly preserved; indicate on-camera/offscreen source, voice reference, room tone, foley.
9. **Lighting and Texture**: concise film look, practical light source, color relation, depth of field.
10. **Negative Constraints**: only failure-prone exclusions, not a giant generic pile.
11. **Final Frame**: exact last visible state and who/what must not return.

For a full reusable template and checklist, read `references/prompt-template.md`.

## Field Mapping

Map upstream fields conservatively:

| Upstream field | Seedance prompt target |
|---|---|
| Event | Segment logic and causal context; include only if it clarifies visible action |
| Scene | Reference inputs and environment setup |
| Character positions | Hard locks and composition |
| Emotional direction | Translate into visible behavior, breath, gaze, hand tension, posture |
| Focal length + aperture + camera position | Shot scale, lens/depth, camera lock |
| Composition | Composition and visibility rules |
| Camera movement | Camera rule; avoid mixing fixed camera with push/pan language |
| Action/expression/dialogue | Timed beats and performance |
| Must-have constraints | Visual/audio/content locks |
| Must-not constraints | Negative constraints |
| Continuity card | First timed beat and final-frame carryover |

## Seedance 2.0 Reliability Rules

- Put first-frame constraints before motion instructions.
- Separate "identity reference" from "visible frame requirement."
- Replace abstract emotion with physical evidence.
- Reduce hidden or blurred details; do not ask the model to show what the composition hides.
- Avoid conflicting lens/crop/action instructions, such as chest-up framing plus visible footwork.
- Avoid overloading style: one or two strong film references are enough.
- Use timed beats such as "0-3s / 3-7s" instead of generic shot labels when the output should be one continuous clip.
- Use explicit cuts only when the user accepts multi-shot generation inside one segment.
- If the prompt approaches a platform character limit, shorten style first, then environment, then negative constraints. Preserve reference roles, action, dialogue, and final frame.

## Output Modes

Choose the mode that fits the user's request:

- **Execution Analysis**: feasibility score, likely Seedance failures, contradictions, and fixes.
- **Split Plan**: segment grouping with estimated seconds and rationale.
- **Prompt Rewrite**: final Seedance-ready prompts.
- **Reference Table**: map images/videos/audio to roles before writing.
- **Asset Bible**: extract reusable scene, set, prop, weapon, creature, VFX, UI, and audio assets before shot writing.
- **Debug Pass**: diagnose a failed Seedance output and rewrite only the failing parts.
- **Template Extraction**: produce a reusable prompt skeleton for the user's production chain.

## Project-Wide Cinematography Rules

If the user establishes a recurring cinematography reference for a project, preserve it as a rule for later prompts in the same project.

If the user says they are restarting with a new script or a new setting, treat the newest style bible as overriding prior project defaults.

For references to living cinematographers or directors of photography, do not write prompts as direct imitation of a person's exact style. Translate the reference into controllable cinematography principles: motivated light sources, lens choice, contrast, blocking, camera movement, silhouette, negative space, color restraint, and shot readability.

For the user's current desert sci-fi monster-hunt project, default to these principles unless they override them:

- Use epic desert sci-fi and monster-hunt blockbuster principles: huge scale, harsh natural light, heat shimmer, sand volume, heavy creature ecology, tactical hunters, and readable action geography.
- Keep lighting source-based: twin suns, black-rock shadow, sand bounce, weapon energy, visor reflection, monster biology, and dust occlusion.
- Extract scene assets and prop/weapon/creature assets before shot writing, then include asset callouts or call sheets in industrial storyboards.
- Avoid arbitrary beauty light, uniform fill light, music-video camera spinning, unreadable VFX clutter, and direct IP copies.
- Give each action beat an intention shot, a force-release shot, and a result shot.
- Use extreme wide shots for desert scale, low-angle shots for monsters, and stable long-lens shots for tactical or character beats.

When delivering final prompts, include only enough notes to help the user run them: segment ID, duration, reference roles, prompt text, and top risks.
