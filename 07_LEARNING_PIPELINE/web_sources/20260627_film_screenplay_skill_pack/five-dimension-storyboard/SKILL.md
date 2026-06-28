---
name: five-dimension-storyboard
description: Turn scripts, scenes, outlines, or dialogue into a high-fidelity five-dimension cinematic storyboard table or copyable shot prompts. Use when the user asks for 五维度分镜, 分镜提示词模板, 剧本拆分镜, 跑视频分镜, 保真分镜, detailed shot tables, character-performance storyboard beats, Hong Kong film/noir/action-style shot planning, or an upstream storyboard intended for later Seedance 2.0 prompt conversion.
---

# Five-Dimension Storyboard

Use this skill to convert a user-provided script into a production-style cinematic storyboard. Default to **跑视频保真模式**: preserve script information, inherit original shot instructions, and expand key action causality instead of summarizing the scene. The output is an upstream storyboard, not the final Seedance 2.0 prompt. If the user later asks to run or optimize for Seedance, hand the storyboard to `seedance-shot-prompt`.

Default language: Chinese.

## Core Positioning

Produce a storyboard that thinks like a small film crew:

- **Director lens**: character chemistry, subtext, emotional rhythm, atmosphere as story.
- **Action lens**: action geography, physical realism, force path, injury/cost, environmental interaction.
- **Storyboard lens**: precise shot scale, angle, lens, camera movement, composition, visual hook, continuity.

Keep the output executable and faithful. Prefer concrete visible behavior over literary explanation, but do not remove script-specific visual, action, equipment, monster, worldbuilding, or relationship details.

## Intake

Before writing the storyboard, identify or infer:

- script type: 对峙冲突, 动作打斗, 独白抒情, 追逐紧张, 暧昧亲密, 群戏调度, 闪回回忆, 大场面定场
- characters, exact names, dialogue, setting, props, emotional arc
- style reference, art direction, image quality target, and film/genre references; if absent, infer from the script and state the inference
- output mode: 跑视频保真模式, 分镜概览模式, or 小镜头提示词模式
- whether the user needs only storyboard output or also a Seedance-ready rewrite

If the script is ambiguous, make conservative assumptions and state them briefly before the table. Do not rewrite user dialogue unless explicitly asked.

## Output Modes

Choose the mode from the user's wording:

- **跑视频保真模式 (default)**: Preserve the script as fully as possible. Expand all key visual details and action causality. Use this when the user wants to test video generation, copy prompts, or compare against the original script.
- **分镜概览模式**: Shorter director-facing overview. Use only when the user asks for a quick structure, summary, or rough split.
- **小镜头提示词模式**: Output copyable blocks where the technical metadata is prefixed before each shot prompt: `【S01-01｜0-3s｜景别｜角度｜焦段｜机位｜运镜】`.

Do not silently switch 跑视频保真模式 into summary mode. If the script is long, split into more segments instead of compressing plot-critical information.

## Timecode Rule For Video Generation

For 跑视频保真模式 and 小镜头提示词模式, treat every segment as a separate video-generation module:

- Reset timecode to `0s` at the start of every segment/module.
- Keep each module no longer than `15s`.
- Use segment IDs (`S01`, `S02`, `S03`) for full-story order, not continuous cumulative time.
- Use shot IDs inside each module, e.g. `S03-01｜0-3s`, `S03-02｜3-7s`.
- Do not output global cumulative timecodes like `51-55s` unless the user explicitly asks for an edit timeline.

## Workflow

1. **Parse the script**
   - Extract characters using exact names. Do not normalize names.
   - Preserve dialogue verbatim.
   - Preserve dialogue punctuation verbatim and use punctuation to infer delivery, pause, breath, pressure, and emotion.
   - Extract and preserve visual assets: character body/face/hair/costume, equipment, weapons, creature anatomy, environment, VFX, sound, subtitles, and narration.
   - Identify scene changes, emotional reversals, action conflicts, reveals, original shot instructions, and important physical beats.

2. **Segment**
   - Each segment is 4-15 seconds unless the user requests otherwise.
   - Reset each segment's internal timecode to 0s. Do not carry cumulative timeline time into copyable prompts.
   - Force a new segment when the location, time, major emotional state, or physical continuity changes.
   - In 跑视频保真模式, split dense scripts into more segments instead of merging actions or deleting details.
   - Prefer continuity over fragmentation, but never merge separate attack/result/reaction beats into one overloaded shot.

3. **Run the five-dimension pass**
   - Subject and physical motion: who/what dominates the frame; force, speed, body state.
   - Environment and emotional light: how space, light, weather, sound, and texture affect the scene.
   - Optics and camera: shot scale, vertical angle, focal length, camera position, movement, composition.
   - Time and state evolution: what changes from opening to final frame.
   - Aesthetic medium: film texture, contrast, saturation, grain, visual clarity.
   - Visual anchor: art style, image quality, genre/film references, color palette, lighting behavior, material rendering, and negative style constraints.

4. **Design performance space**
   - After key dialogue, include a reaction shot or a visible listener response.
   - At emotional peaks, include a beat shot with concrete silent performance.
   - Important physical gestures get their own shot, not a side note inside dialogue.
   - For every dialogue line, run the punctuation-emotion pass: convert punctuation into voice action, pause length, breath state, and actor performance notes without changing the quoted words.
   - Calculate dialogue duration with video-generation-safe speech rates: `spoken characters / safe speech rate + punctuation pauses + performance buffer`.

5. **Output the storyboard**
   - Start with a global visual bible when output is for video generation.
   - Then provide a segment overview table.
   - Then provide each segment with a header, shot table, and ending state.
   - For every segment/module, output a segment visual anchor before the shot prompts.
   - In 跑视频保真模式, add a fidelity check after each segment: retained source details and omitted source details.
   - If using 小镜头提示词模式, place the metadata header before every copyable shot block.

## Required Output Structure

### 1. Global Visual Bible

For 跑视频保真模式 and 小镜头提示词模式, output this before the segment overview:

```text
【全局视觉圣经】
题材对标：电影/剧集/广告/游戏CG/动画等题材参照；若引用具体作品，只提可控原则，不模仿在世艺术家的个人风格。
画风画质：写实/CG/动画/胶片/广告片等；清晰度、质感、渲染层级。
色彩光影：主色、辅色、光源方向、对比度、色温、曝光倾向。
材质锚定：角色服装、皮肤/装甲/武器/怪物/环境材质的关键词。
镜头基调：摄影风格、景深倾向、运动节奏、画面密度。
负面风格约束：不要出现的画风、质感、画面缺陷、字幕水印等。
```

### 2. Segment Overview

Use this table:

```markdown
| 段落 | 时间范围 | 类型词 | 核心情绪 | 关键事件 | 转场 |
|---|---|---|---|---|---|
```

### 3. Detailed Segment

For each segment:

```text
【场景空间(内/外+地点+时段) · 时长 · 类型词】
视觉锚定：
  题材对标：本段具体电影/题材参照或镜头气质
  画风画质：本段画面质量、渲染、真实度
  色彩光影：本段光源、色彩、阴影、氛围
  材质/VFX：本段必须稳定出现的材质、粒子、能量、液体、烟尘等
  负面约束：本段最容易跑偏的风格和画面错误
人物：角色1, 角色2
场景起始状态：
  角色1 = 姿态[...] · 伤势[...] · 持有道具[...] · 情绪[...] · 朝向关系[...]
空间布局：角色1在画面左1/3，角色2在画面右2/3；核心物件...
本段主线：不超过15字
```

Then use this shot table:

```markdown
| 时间码 | 景别 | 角度 | 焦段 | 机位 | 运镜 | 构图 | 拍摄速度 | 站位 | 视线 | 画面内容描述 | 台词 | 表演重点 | 微表情 | 音效 | 视觉钩子 | 镜头功能 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
```

Close each segment with:

```text
总时长：XX秒
结尾状态：
  角色1 = 姿态[...] · 伤势[...] · 持有道具[...] · 情绪[...] · 朝向关系[...]
不变元素：光线/服装/关键道具/镜头基调
渐进变化：情绪链或动作链
保真检查：
  已保留：原剧本中的关键外观/装备/动作/台词/设定
  已省略：省略内容；若无则写“无”
```

## Hard Rules

- Script fidelity outranks brevity. Do not compress away character design, costume, equipment, monster anatomy, worldbuilding, narration, key sound, subtitles, or relationship beats.
- Visual anchoring must be explicit in the final output. Do not leave art style, image quality, film/genre references, color, lighting, material rendering, or negative style constraints only as internal reasoning.
- For video-generation outputs, every segment/module must include a `视觉锚定` block before shot prompts.
- If the user does not provide a style reference, infer one from genre and script content and label it as an inference.
- Preserve user dialogue verbatim. Split long lines only at natural punctuation.
- Preserve punctuation verbatim. Do not “clean up” ellipses, exclamation marks, question marks, dashes, tildes, or quotation marks unless the user asks for dialogue editing.
- Use punctuation as performance direction: infer pause, breath, speed, volume, pressure, uncertainty, collapse, teasing, or emotional release from the punctuation and write it into 表演重点/音效/小镜头提示词 outside the quoted dialogue.
- Use video-generation-safe speech rates, not human maximum speech speed. Always leave time for breath, facial reaction, and mouth-shape readability.
- Do not fill a shot's entire duration with speech. Reserve 0.2-0.5s before speaking and 0.3-1s after important lines for emotional residue unless the user asks for rapid-fire dialogue.
- Preserve original shot instructions. When the script contains `【镜头:...】`, inherit its shot intent first; only add lens, blocking, performance, sound, or light. Do not replace it with a different shot design unless the user asks for redesign.
- Keep each segment no longer than 15 seconds.
- Keep segment ending state continuous with the next segment opening state.
- Use exact character/entity names throughout.
- Split action causality into separate beats: setup, strike/trigger, impact, reaction, consequence, and next tactical move. Do not pack two or more major action results into one short shot.
- Use geometric blocking: 画面左1/3, 画面中, 画面右2/3. Avoid vague blocking such as "两人对峙".
- Fill every shot's 视线, 表演重点, 微表情, 音效, 视觉钩子.
- Do not use placeholders such as "(略)", "见对话", "自然表现", "按剧情".
- Do not create characters, props, injuries, or powers not grounded in the script unless clearly marked as an assumption.
- If any original source information is omitted, list it in the segment fidelity check with a short reason.

## Option Libraries

Use these controlled values unless the script requires a careful exception:

- 景别: 大全景, 远景, 全景, 中景, 近景, 特写, 大特写
- 角度: 平视, 仰拍, 俯拍, 顶拍, 手持拍摄
- 焦段: 8mm, 16mm, 35mm, 50mm, 85mm, 100mm(微距), 135mm, 200mm
- 机位: 正面机位, 正侧机位, 斜侧机位, 背面机位, 过肩机位
- 运镜: 推, 拉, 摇, 移, 跟, 升, 降, 甩, 环绕, 希区柯克变焦, 跟焦, 俯仰, 旋转, 微移, 一镜到底, 急推, 速摇, 手持跟拍
- 构图: 黄金分割, 中心, 对称, 框架式, 引导线, 对角线, 荷兰角, 前景, 留白
- 拍摄速度: 正常, 升格, 降格
- 镜头功能: 铺垫, 蓄势, 爆发, 收束, 过渡, 信息交代, 反应, 留白

## When More Detail Is Needed

Read `references/storyboard-rules.md` for the full compact rule set: segmentation heuristics, performance beat rules, pacing tables, and Seedance handoff guidance.

Read `references/dialogue-punctuation-emotion.md` whenever a script contains dialogue, narration, voiceover, or emotionally meaningful punctuation.

Read `references/visual-anchoring.md` whenever output is intended for image/video generation, Seedance testing, or copyable shot prompts.
