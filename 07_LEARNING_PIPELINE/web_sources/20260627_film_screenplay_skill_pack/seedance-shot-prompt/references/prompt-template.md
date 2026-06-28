# Seedance 2.0 Prompt Template

Use this reference when generating final prompts, checking a storyboard conversion, or debugging a failed Seedance result.

## Reference Role Table

Start by clarifying reference roles. Do not let "reference image" mean everything.

```text
【参考素材角色表】
@image1: 首帧。锁定开场构图、人物位置、机位角度、景别、光线色块、画面裁切。
@image2: 角色A身份参考。只用于脸型、发型、服装、年龄感、材质，不改变首帧构图。
@image3: 角色B身份参考。只用于身份和外观，不要求在每一帧清晰出现。
@image4: 场景参考。用于空间风格、家具/道具、色彩气质，不覆盖首帧机位。
@image5: 尾帧。仅在首尾帧模式下锁定最终状态。
@video1: 动作/镜头运动参考。只学习运动节奏，不复制人物身份。
@audio1: 角色A音色或环境声参考。普通话对白按 prompt 文本执行。
```

If no references are available, state that character and scene consistency will rely on text only.

## Asset Bible Template

Use this before writing industrial storyboard shots when the user wants professional shot planning.

```text
【资产拆解总表】
ENV001｜场景资产｜名称：
描述：地理、尺度、光照、天气、地形、可拍摄角度。
视觉锚点：观众一眼识别它的元素。
状态变化：从开场到结尾是否改变。
镜头使用：A01, B03...
参考素材：@[REF_ENV_...]

SET001｜置景资产｜名称：
描述：前景/背景中反复出现的岩石、废墟、家具、灯具、桌面物。
互动：角色是否趴、坐、躲、撞、攀爬。

PROP001｜道具/武器资产｜名称：
描述：造型、材质、比例、发光部件、机械结构。
状态变化：收起、展开、充能、破损、沾血/沾沙。

CRE001｜生物资产｜名称：
描述：体型、解剖结构、甲壳/皮肤、弱点、攻击方式。
状态变化：完整、受伤、断裂、死亡、体液喷溅。

VFX001｜特效资产｜名称：
描述：沙尘、热浪、能量、电弧、爆炸、体液、HUD抽象图形。
使用规则：不要遮挡核心动作；是否后期叠加。

SND001｜声音资产｜名称：
描述：环境底噪、武器声、怪兽声、装甲声、冲击声。
使用规则：是否持续、是否盖过对白。
```

After the asset bible, include a compact call sheet:

```text
【镜头资产调用表】
A01：ENV001, SET001, VFX001, SND001
A02：ENV002, EQP001, PROP001, VFX002, SND002
B07：CRE001, PROP002, EQP002, VFX004, VFX006, SND005
```

## Core Prompt Skeleton

```text
【生成目标】
Seedance 2.0 生成真人电影实拍质感视频，时长约[4-15]秒，[16:9 / 2.35:1]，非CG、非动画、非游戏渲染、非AI插画。输入模式为[文生视频 / 首帧图生视频 / 首尾帧 / Omni Reference / 多模态参考]。[一镜到底 / 包含明确剪切]。

【参考素材】
@image1作为[首帧/角色/场景/道具/风格]参考：[具体作用]。
@image2作为[角色身份]参考：[只锁定哪些特征，不锁定哪些内容]。
@video1作为[动作/镜头]参考：[只学习什么]。
@audio1作为[音色/环境声]参考：[对应角色或环境]。

【本段资产调用】
场景：[ENV001 名称]；置景：[SET001 名称]；角色装备：[EQP001 名称]；道具/武器：[PROP001 名称]；生物：[CRE001 名称]；特效：[VFX001 名称]；声音：[SND001 名称]。

【全局硬锁】
摄影机[完全固定 / 缓慢推近 / 明确运动方式]；画面裁切为[胸口以上/中近景/全景/特写]；[主体A]位于画面[位置]；[主体B]位于画面[位置/画外/虚化前景]；[前景/道具/桌面]从首帧到尾帧保持[不变/基本不变]。禁止新增未指定角色，禁止改变首帧机位角度，禁止出现字幕或画面文字。

【构图与可见性】
清晰主体：[谁或什么]。焦外主体：[谁或什么]，只允许出现[肩膀/手臂/头发轮廓/色块/局部]。画外主体：[谁]，只通过声音或反应存在。背景为[浅景深/深景深]，[允许/禁止]识别具体物件。

【时间段落】
0-[T1]秒：[一个主动作]。写清动作起因、身体部位、方向、速度、可见变化和对应音效。
[T1]-[T2]秒：[第二个主动作]。明确承接关系，不留模型自由误读的空白。
[T2]-[T3]秒：[对白或关键反应]。写清谁说话，声音来自画内还是画外，表情和身体反应。
[T3]-[N]秒：[收束动作]。明确尾帧前的姿态、视线、道具状态、画面中谁不出现。

【对白与声音】
所有对白为普通话。精确保留台词。
[角色A]（音色参考@audio1，声音位置：[画内/画外/画后方]，语气：[可听见的语气描述]）："台词"
环境声：[空调/车流/餐厅人声/衣料摩擦/道具声]，音量不盖过对白。
动作音效：[按时间段对应写具体声音]。

【光影与质感】
[实拍电影质感]，[具体摄影质感或镜头风格]；主光源来自[窗光/壁灯/霓虹/台灯/自然光]，方向为[左/右/后/顶]；色彩为[低饱和暖中性/冷蓝与暖橙对比/霓虹粉紫与冷蓝]；景深为[极浅/中等/大景深]；胶片颗粒[轻微/明显]。影视参考最多保留1-2个。

【负面约束】
不要CG感、不要动画感、不要游戏渲染、不要西方面孔（如是中国故事）、不要鱼眼变形、不要画面闪烁故障感、不要字幕文字、不要改变首帧构图、不要新增人物、不要让画外角色突然入画、不要出现与裁切冲突的全身动作。

【尾帧】
最后一帧定格为：[主体位置、姿态、视线、道具状态、光线状态、谁在画面内、谁必须画外或焦外]。
```

## Storyboard Conversion Pattern

When converting upstream storyboard fields, use this compact structure:

```text
【段落ID】B01a
对应上游：[B01-分镜1到分镜2]
预计时长：[约9秒]
输入模式：[首帧图生视频/纯文生视频/Omni Reference]
参考素材：[列出@image/@video/@audio角色]

【Seedance提示词】
[完整prompt]

【执行风险】
1. [最可能失败的画面/动作/声音]
2. [参考素材可能冲突点]
3. [抽卡建议或替代写法]
```

## Split Rules

- 4 seconds or less: usually merge with adjacent action.
- 4-15 seconds: acceptable single Seedance segment.
- More than 15 seconds: split by emotional beat, location change, or action chain boundary.
- Never split one sentence of dialogue.
- Never split one continuous action chain such as "伸手-接过-放下".
- A 0.5-2 second cutaway should usually become one timed beat inside a larger prompt.

## Feasibility Checklist

Before returning a final prompt, verify:

- Input mode is named.
- First frame, if any, is the strongest visual authority.
- Reference images are assigned roles instead of treated as generic inspiration.
- Camera instruction is not contradictory.
- Crop supports the required action.
- Hidden, blurred, or offscreen details are not written as visible requirements.
- Each timed beat has one primary action.
- Dialogue is exact, in Mandarin when requested, and source position is clear.
- Negative constraints target likely failures instead of bloating the prompt.
- Final frame is explicit.

## Common Failure Diagnosis

If Seedance output does not match the prompt, diagnose by symptom:

| Symptom | Likely cause | Rewrite move |
|---|---|---|
| Character identity drifts | Reference role unclear or text description weak | Bind identity reference explicitly and repeat only stable traits |
| First frame changes | First-frame authority too weak | Move first-frame lock to top and state "do not change opening composition" |
| Camera moves unexpectedly | Mixed fixed and push/pan language | Keep one camera rule and move all motion to actors/props |
| Actor appears full-body in close-up | Crop/action conflict | Rewrite action within visible crop or change shot scale |
| Offscreen character appears | Offscreen rule too soft | State "only through voice/foley; never enters frame" |
| Action is too broad | Abstract emotion/action | Convert to hand, gaze, breath, posture, contact, object movement |
| Dialogue tone wrong | Tone described as emotion only | Add audible delivery: speed, pitch, pause, tail tone |
| Background overwhelms subject | Environment over-described | Reduce background to color blocks/depth and foreground hierarchy |

## Compression Priority

If the prompt is too long:

1. Cut film-camera brand names and extra film references.
2. Shorten environment decoration lists.
3. Merge repeated negative constraints.
4. Remove explanatory intent such as "this expresses..."
5. Preserve reference roles, action beats, exact dialogue, hard locks, and final frame.
