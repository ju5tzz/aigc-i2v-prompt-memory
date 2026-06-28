# Visual Anchoring Rules

Use this reference whenever storyboard output is intended for image/video generation, Seedance testing, or copyable shot prompts. Visual style must be explicit in the final answer, not only internal reasoning.

## Required Layers

### Global Visual Bible

Output once before segment prompts:

```text
【全局视觉圣经】
题材对标：...
画风画质：...
色彩光影：...
材质锚定：...
镜头基调：...
负面风格约束：...
```

### Segment Visual Anchor

Output before every Seedance module:

```text
【S01｜视觉锚定】
题材对标：...
画风画质：...
色彩光影：...
材质/VFX：...
负面约束：...
```

Then output the copyable shot prompts.

## Field Guidance

### 题材对标

Describe genre and cinematic references as controllable principles:

- desert sci-fi monster-hunt blockbuster
- tactical hunter action sequence
- high-end CG trailer
- dark urban noir
- clean commercial product film
- intimate dialogue drama

If using specific film references, translate them into controllable style elements. Do not ask for exact imitation of a living filmmaker or artist.

Example:

```text
题材对标：沙漠科幻怪兽猎杀片；参考《沙丘》的荒漠尺度与逆光压迫、《怪物猎人》的巨兽狩猎动作、《环太平洋》的重量级怪兽存在感。
```

### 画风画质

Specify the image-generation target:

- 写实CG电影质感
- 真人电影实拍质感
- 高规格游戏CG预告片
- 2D动画/日漫厚涂/赛璐璐
- 胶片颗粒、低饱和、高反差
- 8K级细节、真实材质、体积光、清晰边缘

Avoid vague phrasing like only "cinematic" or "high quality".

### 色彩光影

Specify:

- main color and accent colors
- light source direction
- contrast level
- color temperature
- exposure tendency
- shadow behavior
- atmospheric effects

Example:

```text
色彩光影：双子恒星正午硬光，金色沙丘高亮，黑岩深阴影，蓝白电弧与橙红等离子形成冷暖对撞，热浪造成背景轻微扭曲。
```

### 材质锚定

List stable material keywords:

- skin, hair, sweat, dust, blood/fluid
- tactical fabric, elastic fiber, metal armor, carbon fiber
- weapon glow, plasma, electric arcs
- creature shell, translucent membrane, red core, green fluid
- sand grains, rock, smoke, heat shimmer

### 镜头基调

Specify:

- lens tendency
- depth of field
- camera movement style
- density of frame
- action readability
- handheld/stabilized/aerial/locked-off behavior

### 负面风格约束

Use only relevant constraints:

- 不要卡通化
- 不要二次元扁平上色
- 不要塑料质感
- 不要低清游戏CG
- 不要过度磨皮/过度美颜
- 不要字幕/水印/Logo
- 不要无关新增角色
- 不要改变服装、武器、怪物结构
- 不要画面过曝、过暗、糊成一团

## Default Inference

If no style reference is provided, infer from the script:

- sci-fi combat + monsters: 写实CG电影质感 / high-end CG trailer / monster-hunt blockbuster
- urban crime/noir: 真人电影质感 / high contrast / wet street reflections / neon
- romance/intimacy: shallow depth, soft practical light, restrained color
- fantasy costume: ornate fabric, practical torch/moonlight, epic scale
- product or commercial: clean lighting, controlled reflections, premium material focus

Always label inferred style as:

```text
题材对标：根据剧本推断为...
```

## Seedance Stability Notes

- Keep visual anchors concise and repeated per module.
- Do not overload a module with too many unrelated style references.
- Preserve the same global visual bible across all segments unless the script changes location/time/style.
- Segment visual anchors should only add local light, material, VFX, or mood changes.
