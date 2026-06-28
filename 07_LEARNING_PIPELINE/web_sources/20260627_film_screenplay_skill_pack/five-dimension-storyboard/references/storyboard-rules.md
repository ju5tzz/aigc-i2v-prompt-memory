# Five-Dimension Storyboard Rules

This reference condenses the original 五维度分镜模板 into operational rules. Use it when a script is dense, action-heavy, dialogue-heavy, or intended for later Seedance conversion. Default to high-fidelity video-test output unless the user explicitly asks for a short overview.

## Creative Lenses

Use three internal checks before output:

1. **Director check**: What is the character moment? What is the subtext? Does atmosphere participate in the story? Does the segment breathe?
2. **Action check**: Is geography clear? Does every action have motive, force path, impact, and cost? Does the environment affect the action?
3. **Storyboard check**: Does every shot reveal new information? Are shot scale, angle, lens, movement, composition, and visual hook motivated?

If a shot does not add information, emotion, physical continuity, or rhythm, merge or delete it. Do not apply this rule to source-preservation details: distinctive costume, weapon, creature anatomy, worldbuilding, original shot direction, dialogue, and key relationship beats should be retained in high-fidelity mode.

## Output Modes

### 跑视频保真模式 (default)

Use for video testing, Seedance experiments, or copyable prompts.

- Preserve script-specific details instead of summarizing them.
- Expand dense action into more short shots or segments.
- Keep original shot instructions as the primary camera intent.
- Output global and per-segment visual anchors.
- Add a fidelity check after each segment.

### 分镜概览模式

Use only when the user asks for a quick structure or rough director overview.

- Summarize lower-priority details.
- Keep fewer segments.
- Omit the fidelity check unless requested.

### 小镜头提示词模式

Use when the user wants prompts that are easy to copy.

Each shot should be a standalone block:

```text
【S01｜视觉锚定】
题材对标：...
画风画质：...
色彩光影：...
材质/VFX：...
负面约束：...

【S01-01｜0-3s｜景别｜角度｜焦段｜机位｜运镜】
画面、动作、表演、台词、音效。
```

The block must still preserve original script details and dialogue.

## Timecode Rules For Seedance Testing

When output is intended for Seedance or another per-prompt video generator, every segment/module starts at `0s`.

Correct:

```text
【S06-01｜0-4s｜全景｜仰拍｜35mm｜正侧机位｜跟】
【S06-02｜4-8s｜中景｜低角度仰拍｜35mm｜正面机位｜手持跟拍】
```

Incorrect unless the user asks for edit-timeline timing:

```text
【S06-01｜63-67s｜...】
【S06-02｜67-71s｜...】
```

Rules:

- Segment IDs preserve whole-story order.
- Internal shot timecodes describe only that segment's generated clip.
- Maximum segment duration is 15 seconds.
- If one scene needs more than 15 seconds, split it into `S06A`, `S06B` or the next sequential segment, and reset each one to `0s`.
- Segment ending state must still hand off to the next segment opening state.

## Script Fidelity Rules

In 跑视频保真模式, preserve these source details unless the user asks for compression:

- **Character design**: body posture, hair, face, costume cut, exposed materials, armor parts, damage, wetness, dust, blood/fluid.
- **Equipment and props**: weapon names, weapon modes, energy color, mechanical parts, heat vents, scope/visor state, ammo/projectile behavior.
- **Creature design**: scale, legs, shell/skin, spikes, eyes, core/weak point, fluids, wounds, movement, roar, death state.
- **Environment and worldbuilding**: location name, time, weather/light, terrain, background forces, narration, technology premise.
- **Relationship beats**: jokes, teasing, embarrassment, concern, group familiarity, reaction lines.
- **Original shot directions**: any `【镜头:...】` instruction in the script.

If a detail is impossible to fit in one segment, split the segment. If it is still omitted, list it under `已省略`.

## Original Shot Inheritance

When the script includes a shot instruction, inherit its core intent:

- Do not replace a scripted handheld close-up with a different establishing shot.
- Do not drop listed camera path details, such as "小腿装甲 -> 大腿根部 -> 臀部曲线 -> 后脑短发 -> 侧脸".
- Do not replace scripted "稳定器侧面平移", "高速摄影慢动作", "低角度仰拍", or "单次连续镜头" unless the user asks for redesign.
- Add only execution support: focal length, camera position, composition, sound, performance, lighting, timing.

If a source shot is too long for one generated clip, split it while preserving the same visual path.

## Action Causality Rules

Do not compress key action chains into one overloaded shot. Separate these beats when present:

1. setup or aim
2. trigger or strike
3. projectile/weapon travel or body movement
4. impact
5. injury, breakage, melt, explosion, recoil, or loss of balance
6. reaction or tactical follow-up
7. final consequence

For example, do not merge "索菲亚开甲" and "凛炮击核心" into one 3-second shot if both are important. Split into: 索菲亚扑出 -> 爪刃刺入 -> 撕开甲壳 -> 索菲亚报核心位置 -> 凛切炮击模式 -> 炮弹贯穿核心.

## Five Dimensions

1. **绝对主体与物理动势**
   - Identify the absolute subject.
   - Describe motion path, speed, force, body state, and post-action cost.
   - For action: write the force path, e.g. shoulder -> elbow -> fist -> impact -> recoil.

2. **环境场与情绪光影**
   - Make the environment a participant, not a backdrop.
   - State light direction, quality, color temperature, texture, weather, and sound.
   - If no style is specified, default to Hong Kong noir: wet ground reflections, neon, narrow depth, high-contrast darks, street noise.

3. **光学与摄影机调度**
   - Choose focal length, depth feel, vertical angle, camera position, and movement for emotional or narrative reasons.
   - Camera movement must have motive: push for inner pressure, pull for reveal, follow for urgency, static for performance pressure.

4. **时间轴与状态演变**
   - Track psychological state and physical state from first frame to final frame.
   - Include setup, tension, release, and aftermath where the script supports it.

5. **美学介质与底层质感**
   - Specify realism, contrast, saturation, grain, sharpness, atmosphere, and color relation only when they serve the scene.
   - Avoid generic "beautiful cinematic" phrasing without visible anchors.
   - Output art style, image quality target, genre/film references, material rendering, and negative style constraints explicitly.

For detailed visual anchor structure, read `visual-anchoring.md`.

## Segmentation

Use 4-15 seconds per segment by default. Dense dialogue or action may use shorter segments. In high-fidelity mode, allow more segments to preserve source information.

Reference ranges by script length and type:

| 字数 | 对峙/独白/暧昧 | 动作/追逐 | 群戏/大场面 |
|---|---|---|---|
| <=300 | 1段 | 1-2段 | 1段 |
| 301-800 | 2段 | 2-3段 | 2段 |
| 801-1500 | 2-3段 | 3-4段 | 3段 |
| 1501-2500 | 3-5段 | 4-6段 | 4-5段 |
| 2501-3500 | 5-7段 | 6-8段 | 5-7段 |
| 3500+ | >=7段 | >=8段 | >=7段 |

Count switch signals: speaker changes, emotional reversal, action conflict, inner monologue, spatial shift, reveal/reversal. Final segment count should generally be at least `ceil(signal count / 2)` but not so high that continuity breaks.

For video-test fidelity, use these stronger defaults:

- 1500-2500 Chinese characters with action or CG spectacle: usually 8-12 segments, not 3-5.
- A major battle sequence: split into tactical beats rather than one "fight" segment.
- Dialogue-heavy worldbuilding: keep narration intact by splitting across shots or marking it for voiceover, not by deleting sentences.
- A scripted teaser/reveal: keep the full reveal chain, including detection, reaction, emergence, scale comparison, roar, and final line.

## Performance Beats

### Reaction Shot

Use after key dialogue. It can be a dedicated shot or an active listener shot. It should show digestion, not just looking:

- eyes shift, pupils tighten, gaze avoids or locks
- jaw tightens, mouth corner trembles, breath changes
- posture hardens, recoils, or collapses

### Beat Shot

Use at emotional peaks or after major reveals:

- 2-4 seconds
- no dialogue
- static, micro-push, or micro-pull only
- write concrete silent acting: throat movement, breath, eyes, hand tension, posture

### Physical Beat

Give important physical gestures their own shot:

- hand opens/clenches, body turns, steps back, falls, touches an object, drops a prop
- include action plus after-state
- avoid "边说边..." for major gestures

## Dialogue Timing

Preserve user dialogue verbatim. Split only at natural punctuation.

Also use `dialogue-punctuation-emotion.md` to translate punctuation into delivery notes. Do not rewrite the punctuation itself; write the inferred voice and acting direction outside the quoted line.

Use video-generation-safe speech rates rather than human maximum speed. Dialogue must leave time for breath, mouth-shape readability, facial reaction, and emotional residue.

Dialogue duration formula:

```text
台词时长 = 可发声汉字数 / 安全语速 + 标点停顿 + 表演缓冲
```

Use `dialogue-punctuation-emotion.md` for the current safe speech-rate table and punctuation pause table.

Single-shot dialogue should usually stay under the safe character budget for that shot type. If it does not, split across multiple shots while preserving exact words and punctuation.

## Shot Rhythm

Use the four-beat rhythm when it fits:

| 类型 | 铺垫 | 发展 | 高潮 | 收束 |
|---|---|---|---|---|
| 对峙冲突 | 全/中景定场 | 近景切角度 | 特写强化 | 中近景留白 |
| 动作打斗 | 中景入场 | 近景冲突 | 大特写终结 | 中景后果 |
| 独白抒情 | 全景慢推 | 中景累积 | 特写爆发 | 中景余韵 |
| 追逐紧张 | 全景快跟 | 中景手持跟 | 近景急推 | 全景逃离/驻足 |
| 暧昧亲密 | 中景慢推 | 近景推进 | 大特写触碰 | 近景余韵 |
| 群戏调度 | 大全景定场 | 中景切局部 | 中景调度高潮 | 全景收束 |
| 闪回回忆 | 全景柔光 | 中景柔焦 | 特写闪回 | 中景回现实 |
| 大场面定场 | 大全景缓推 | 全景缓推 | 全景展开 | 大全景定场收 |

Avoid consecutive shots with identical shot scale and angle when shooting the same subject. Use at least a two-level shot-scale jump or shift camera angle by more than 30 degrees.

## Segment Header Requirements

Each segment header must include:

- location/time/interior-exterior
- duration and type word
- exact character list
- starting state for each character: posture, injury, prop, emotion, facing/gaze relationship
- spatial layout using frame geometry
- one-line segment spine under 15 Chinese characters

## Segment Ending Requirements

Each segment must end with:

- total duration
- ending state for all present characters
- unchanged elements: light, costume, props, sound, camera baseline
- progressive changes: emotion chain or action chain
- fidelity check: retained source details and omitted source details

The ending state is a handoff card for the next segment or for later Seedance first-frame generation.

Use this fidelity check:

```text
保真检查：
  已保留：列出本段保留的原文外观、装备、动作、设定、台词或镜头指令。
  已省略：列出被省略的原文信息；没有省略则写“无”。
```

## Seedance Handoff Notes

This skill creates upstream storyboards. For Seedance 2.0 execution, later compress each segment into:

```text
Segment ID / duration / aspect ratio / one take or cuts
Reference inputs and roles
Visible locks: characters, costume, props, positions, lighting
0-3s / 3-7s / 7-12s timed beats
Performance and motion details
Dialogue/audio if short and necessary
Final frame state
Negative constraints
```

When the user wants actual Seedance prompts, invoke or follow `seedance-shot-prompt` after this storyboard pass.
