# AIGC Video Prompt Model Rules

Use this reference before producing Seedance or GPT-Image-2 prompts. Prefer Chinese prompt output unless the user asks otherwise.

## Seedance Video Prompt

### Structure

```text
[STYLE LOCK]
<一句话锁定风格：参考影像系统/胶片型号/镜头语言/自然光/真实肌理/画幅>
<一句话锁定场景光影、色调、环境底色>

@[character_id] 作为<角色>的形象视觉锚定。  // 仅在有角色参考图时逐角色写

<连续散文正文：按时间顺序写运镜 + 人物动作 + 光影变化 + 表情神情 + 细节 + 随动作出现的环境声/动作声>
```

Do not place a separate negative sentence such as "画面中不出现文字/UI". For Seedance, keep unwanted elements absent from the prompt and catch them in QA instead.

### Required Dimensions

- **运镜**：写清机位起止、运动方式、速度、角度，以及镜头跟着谁、绕着什么、从哪里到哪里。
- **动作**：拆成可执行的姿态、招式、移动、力度、方向和时间推进，不用空泛情绪词代替动作。
- **光影**：写光位、硬软、光比、色温，以及光随动作或场景变化的过渡。
- **表情**：写眼神方向和面部状态；如果有角色图锚定，不重新描述五官长相。
- **细节**：写发丝、衣摆、布料、水、沙、火星、草屑、尘、前景/中景/远景层次。

### Seedance Prohibitions

- **禁负向锚定**：不写"不要 X"、"不出现 X"、"NOT"、"X 在画面外"。不要的东西完全不写。
- **禁画面外元素**：只写当前镜头内可见物。角色看向画外时，只写视线方向，不写画外物体。
- **真人实拍禁 CG/3D 语言**：不要写 CG、3D、CGI、render、写实CG、游戏引擎、材质渲染、shader。用胶片型号、自然外光、真实皮肤发丝肌理、结构性描述建立真实感。
- **禁参考图打架**：有参考图时，不堆砌会和参考图冲突的景观或构图描述。
- **禁双语冗余**：同一信息不要中英重复。
- **禁正文列表化**：正文写连续散文，不写 sub-list、分阶段小标题、时间戳，除非用户明确要求。
- **禁音效独立成块**：环境声和动作声嵌进对应动作里。

### First/Last-Frame

- 首帧和尾帧是固定端点，prompt 的任务是写中间可见过渡：运镜、形变、消融、光变、动作延续。
- 不写"收束"、"定格"、"屏息"、"稳住"、"凝固"。这些词容易让过渡后变成静图。
- 如果必须抵达尾帧构图，写"抵达尾帧构图后仍保持动态"，并点名风、衣发、飘带、呼吸、尘、水、火等继续运动。
- 承接下一条 clip 时，正文不写"上一段"、"上一圈"、"承接"、"接着"、"继续"。连续性靠下一条首帧和状态锁定实现。

### State Change: "Pour Water" Method

When the reference image's default state differs from the target state, make the change visibly happen inside the shot instead of only naming the target state.

- 干到湿：开头 1-2 秒让水从画面上方浇下，淋透身体、头发和衣物。
- 站到倒：角色失衡、侧倾、砸落，倒地过程在镜头内发生。
- 完整到破碎：冲击、裂纹扩散、碎片剥落在镜头内发生。

Write the `@[character_id]` anchor according to the reference image's real default state, then put the change in the action.

### Mask Transitions for Multi-Clip Continuity

For long-shot stitching, use a real in-scene occluder moving right to left.

- Clip 1: occluder sweeps from right to left until it fills the frame with black.
- Clip 2: begin from black; the same occluder continues moving right to left and reveals the next image.
- Use the same object and direction on both sides so the black frame joins cleanly.
- The occluder must naturally exist in the scene: tree, rock, pillar, wall edge, vehicle side, or a character's back.
- If using a character back as the occluder, that character must already be present throughout the shot.
- Connected clips should share one continuous action, not two unrelated actions.

### Speed and Complex Camera Moves

Seedance often has low obedience for exact speed control, speed ramps, bullet time, dolly zoom, major camera flips, and cross-environment dissolves. Use visible proxies such as suspended debris, stretched impact sound, slow fabric motion, or track-like camera movement, but expect retries, splitting, hard cuts, or post-production speed work.

## GPT-Image-2 Keyframe / Character Prompt

### Structure

```text
[图像生成 prompt - <标题>]
若基于参考角色：以放入的<角色>作为身份锚定。本 prompt 只规定构图、姿势、光线和环境，不重新设计五官。

# CHANGE
<要改变或生成的新内容：构图、景别、主体占比、姿势、背景、光线、可见关系>

# PRESERVE
<必须严格保留的内容：长相、发型、服装、材质、神情、体型、伤痕、道具、状态。凡没列的都可能漂移>

# CONSTRAINTS
<去除项、必须明显呈现的关系、不要的风格>
```

### Key Differences from Seedance

- GPT-Image-2 可以且应该使用负向约束，把"不要文字/UI/多余元素"放入 `CONSTRAINTS`。
- 要无文字画面时，`CHANGE` 不提文字，`CONSTRAINTS` 明确去除文字、字幕、UI、标志、水印。
- `PRESERVE` 是核心。参考角色的脸、发型、服装、身体特征、道具、状态要逐项列出，未列项容易漂移。

### Common Pitfalls

- **景别拉不开/主体显大**：删掉浅景深、主体清晰、近距离暗示，改写为大远景、小占比、主体约占画面几分之一。
- **精确多点位构图服从一般**：过度精确的顶胯、后仰、交叉线、头在中线等几何关系要简化，或多生成几张挑选。
- **矛盾姿势易塌缩**：低头但抬眼看镜头这类姿势要加重关键措辞，明确头部方向和眼神方向可以同时成立。
- **双人不同参考/不同着装易串脸串装**：必要时分两次生成再合成，或先画一人再 inpaint 另一人。
- **参考图看不到全身着装**：用文字锁定衣服、配件、材质和颜色，否则模型会乱穿。

## Translation Rule

Translate user language into camera-readable visuals before writing prompts.

- 比喻：转成站位、动作、节奏、视线、距离变化。
- IP/梗：转成体型、姿态、运动逻辑、场面关系、光效，不原样写 IP 名。
- 情绪词：转成镜头距离、呼吸、停顿、手部动作、光比、色温、空间压迫。
- 导演/作品引用：只当审美入口，落地到镜头、胶片、构图、运动、质感。

## File Delivery

- Save final prompts as `.txt`.
- Use pure English filenames to avoid server encoding bugs.
- After producing prompt files, present the paths to the user.
- If the user gives an exact target word/character count, verify with code instead of estimating.
- If requested, scan for sensitive terms semantically and by risky single-character roots; replace with neutral visible language.

## Final Self-Check

- STYLE LOCK 是否符合项目？真人实拍线是否无 CG/3D/render 污染？
- Seedance 正文是否包含运镜、动作、光影、表情、细节？
- Seedance 是否误写负向锚定或画面外元素？
- 首尾帧是否误写"收束/定格/凝固/继续上一段"？
- 音效是否贴在对应动作里？
- 比喻、梗、IP、抽象情绪是否已翻译成可见镜头语言？
- 连续性状态、遮罩物、入画方向、湿干/破损/道具状态是否一致？
- GPT-Image-2 的 `PRESERVE` 是否列出所有不能漂移的身份要素？
- 文件交付时，文件名是否为纯英文？
