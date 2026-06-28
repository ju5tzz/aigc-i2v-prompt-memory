# Dialogue Punctuation Emotion Rules

Use this reference when a script contains dialogue, narration, voiceover, inner monologue, or meaningful punctuation. Punctuation is treated as acting and voice direction. Preserve the user's original words and punctuation; add delivery notes outside the quoted dialogue.

## Core Rule

Do not rewrite dialogue to express emotion. Keep the dialogue exact, then derive:

- pause length
- breath state
- volume
- speech speed
- pitch/pressure
- emotional intent
- actor facial/body performance

Use video-generation-safe timing, not maximum real-human speech speed. Generated video needs extra time for mouth readability, breath, facial reaction, and emotional residue.

```text
台词时长 = 可发声汉字数 / 安全语速 + 标点停顿 + 表演缓冲
```

Count only spoken Chinese characters for the numerator. Speaker names, brackets, and stage directions do not count as spoken characters.

## Safe Speech Rate Table

Use these rates for storyboard timing and Seedance-facing prompts:

| 场景/情绪 | 安全语速 | 表演缓冲 | 适用说明 |
|---|---:|---:|---|
| 冷静汇报/战术指令 | 4-5字/秒 | 0.3-0.6秒 | 清楚、短促、少情绪，如目标确认、战术指令 |
| 日常对白 | 4-5字/秒 | 0.4-0.8秒 | 最自然的常规速度 |
| 嘴炮/轻快调侃 | 5-6.5字/秒 | 0.3-0.7秒 | 可快，但要留对方反应 |
| 愤怒争吵 | 5.5-7字/秒 | 0.4-0.8秒 | 快而有压迫，但长句要拆 |
| 战斗喊话 | 3.5-5字/秒 | 0.2-0.5秒 | 字少、爆发强、气口重 |
| 撒娇/暧昧/挑逗 | 2.5-4字/秒 | 0.6-1.0秒 | 尾音拖长，尤其有`~` |
| 冷淡压迫 | 2.8-4字/秒 | 0.5-1.0秒 | 慢、低、句尾收死 |
| 悲伤/告白 | 2-3.5字/秒 | 0.8-1.2秒 | 停顿多，眼神和呼吸重要 |
| 哽咽/虚弱/濒死 | 1-2.5字/秒 | 1.0-1.5秒 | 不按正常语速算 |
| 恐惧/卡壳/犹豫 | 1.5-3字/秒 | 0.8-1.5秒 | 省略号、断句占时间 |
| 旁白/世界观说明 | 3.5-4.5字/秒 | 0.5-0.9秒 | 稳、清楚、有画面余量 |
| 快速旁白/信息压缩 | 4.5-5.5字/秒 | 0.3-0.6秒 | 只适合画外音，不适合口型 |

## Safe Character Budgets

For a single shot, do not fill the whole duration with speech. Reserve time for reaction and punctuation.

| 单镜头时长 | 日常对白 | 嘴炮/调侃 | 情绪慢台词 | 战斗喊话 | 旁白/画外音 |
|---:|---:|---:|---:|---:|---:|
| 2秒 | 5-7字 | 7-9字 | 3-5字 | 2-5字 | 6-8字 |
| 3秒 | 8-12字 | 11-15字 | 5-8字 | 3-7字 | 10-13字 |
| 4秒 | 12-16字 | 15-20字 | 7-11字 | 4-8字 | 14-18字 |
| 5秒 | 16-20字 | 20-25字 | 9-14字 | 5-10字 | 18-22字 |

If a line exceeds the safe budget, split it at natural punctuation into multiple shots or mark it as voiceover while the image carries action.

Example:

```text
台词：凛：「...闭嘴。那是风速计算误差。」
语气：先断气式停顿约0.6-1s，声音压低，句号后完全收束；表演为下颌绷紧、视线避开、耳根轻红。
```

## Punctuation Map

| 符号 | 名称 | 声效行动作 | 典型情绪/场景 | 使用说明 |
|---|---|---|---|---|
| `。` | 句号 | 声音干脆落地，气息完全收束，停顿约0.6秒 | 陈述事实、下结论、语气冷淡、坚定、疏离 | 停顿略长于原表，约600ms |
| `，` | 逗号 | 声音微息，气息不断，停顿约0.25秒 | 正常叙事、换气、列举 | 中文推荐使用全角逗号 |
| `……` | 省略号 | 声断气连，气流微弱持续，停顿0.5-2秒 | 犹豫、思考、害羞、虚弱、话未说完、恐惧卡壳 | 制造空白张力，增强情绪留白 |
| `!` | 感叹号 | 声带加压，气流爆破，音调拔高，无停顿续接 | 愤怒、兴奋、惊恐、命令、警告 | 强情绪爆发，避免滥用 |
| `?` | 问号 | 句末语调上扬，气息悬停等待回应 | 疑问、反问、试探、挑衅、惶恐 | 双问号`??`可增强不可置信感 |
| `——` | 破折号 | 前字音拖长1.5-2倍，后音撕裂或骤停 | 声音中断、转折、崩溃、欲言又止、被打断 | 情绪撕裂感强，适合戏剧化表达 |
| `~` | 波浪号 | 单字内音高滑动上扬，尾音拖长带气声 | 撒娇、诱惑、轻佻、慵懒、欢快 | 区别于下划线式平拉长 |
| `、` | 顿号 | 字间短促断开，节奏如切音 | 强调、压抑愤怒、机械式进出、冷冰冰列举 | 一字一顿，增强压迫感 |
| `“”` | 引号 | 触发台词模式，开启对应发声状态 | 标记对话内容，常与冒号连用 | 建议配合使用，如：他说：“……” |
| `‘’` | 单引号 | 音量降低，语速略慢，语气更轻 | 自言自语、内心独白、悄悄话、心虚补充 | 表现私密感与心理活动 |
| `:` | 冒号 | 深吸一口气，准备进入正式台词，停顿约0.3秒 | 引出对话、宣布重点、情绪蓄力开口 | “说话前奏”的关键符号 |
| `；` | 分号 | 停顿略长于逗号，约0.3-0.4秒，气息未断 | 逻辑转折停顿、故作深沉叙述 | 用于复杂长句中的语义分层 |
| `()` | 括号 | 音量降低30%-50%，语速加快，常为气声或心理活动 | 补充说明、内心吐槽、心虚嘀咕、动作提示 | 非主台词，起辅助作用 |
| `[]` | 方括号 | 标注非台词指令，如[停顿2秒]、[气声] | 状态切换、镜头描述、结构化控制 | 系统级指令容器，不发音或特殊处理 |
| `<>` | 尖括号 | 标注特殊音效或发声方式，如<深呼吸>、<破音> | 插入非语言声音、强调生理动作 | 增强真实感与细节表现 |
| `/` | 斜杠 | 语音中断或自我纠正，音色短暂重叠 | 结巴、说错改口、欲言又止、快速切换 | 表现语言不流畅状态 |
| `内容` | 星号包围 | 语气显著变化：更低、更慢、更重 | 着重强调、反讽挖苦、情绪突变 | 强调标记，非标准标点但可用 |
| `_` | 下划线 | 音节拉长但音高不变 | 疲惫拖音、不情愿回应、机械拉长 | 与波浪号“上扬拉长”形成对比 |
| `#` | 井号 | 标注状态标签，如#whisper、#cry | 快速切换情绪模式、启用特定风格 | 社区通用标签，部分系统支持 |
| `.` | 坚线/点 | 表示分镜或时间点分隔 | 时间轴描述，如0-2秒 | 不作为情绪标点处理 |
| `~` | 连字符/悬挂 | 句末声音渐弱至消失，不突然切断 | 入睡呓语、虚弱至极、渐行渐远呼唤 | 表现“消散”感，非戛然而止 |
| `...!` | 省略+感叹 | 压抑后小爆发，停顿后突然短促加重 | 想发火又忍住，最后没忍住 | 情绪压抑后的释放 |
| `!...` | 感叹+省略 | 爆发后迅速泄气，声音从高峰跌落成气声 | 情绪从高点骤降 | 用于爆发后的虚脱或后悔 |
| `??` | 连续问号 | 语气持续上扬，质疑层层递进 | 强烈质疑、不敢相信、震惊、无语 | 比单问号更有冲击力 |
| `!!` | 感叹号+空格/连续感叹 | 连续重音，每词更重且有停顿 | 加强节奏与压迫感 | 用于命令、警告、强烈爆发 |

## Punctuation Pause Additions

Use these values in the timing formula:

| 标点 | 建议额外停顿 |
|---|---:|
| `，` | 0.15-0.3秒 |
| `。` | 0.45-0.7秒 |
| `、` | 0.1-0.2秒 |
| `；` | 0.3-0.5秒 |
| `：` | 0.25-0.5秒 |
| `？` | 0.4-0.8秒 |
| `！` | 0.2-0.5秒气口，可不完全停顿 |
| `……` | 0.6-2秒 |
| `——` | 0.5-1.5秒 |
| `~` | 额外尾音0.4-1秒 |

When multiple marks combine, do not add them mechanically to absurd length. Use the dominant emotional mark, then add only the meaningful pause or tail.

## How To Apply In Storyboards

For each dialogue line:

1. Keep the dialogue text exactly as written.
2. Identify the strongest punctuation cues.
3. Add a concise delivery note in `表演重点` or in the copyable prompt after the quote.
4. Add physical evidence: breath, jaw, eyes, throat, shoulders, hand tension.
5. If a punctuation cue creates a meaningful pause, reflect it in timing or a reaction/beat shot.

## Common Patterns

### Ellipsis Before A Cold Line

`「...闭嘴。」`

- Pause 0.6-1.2s before speech.
- Voice starts low and controlled.
- Actor may avoid gaze, tighten jaw, or suppress embarrassment/anger.
- Timing example: `「...闭嘴。那是风速计算误差。」` should usually take about 4-5 seconds, not 2-3 seconds.

### Tilde Teasing

`「都是风的错~」`

- Tail sound slides upward and lengthens.
- Voice is light, teasing, or deliberately annoying.
- Actor may smile with narrowed eyes or relaxed shoulders.
- Timing example: `「行行行，都是风的错~」` usually takes about 2.5-3 seconds because the tail sound carries performance.

### Command Exclamation

`「接招！」`

- High-pressure breath burst.
- Faster onset, louder volume, rising pitch.
- Pair with forceful body action.
- Timing example: `「接招！」` can fit in 0.8-1.2 seconds, but the shot still needs action wind-up and impact time.

### Colon Before Formal Report

`凛： 「目标确认。」`

- Inhale before the line.
- Delivery becomes procedural, crisp, and mission-focused.

### Question As Provocation

`「队长还挺细心嘛~」`

- If followed by `~`, read as teasing rather than real inquiry.
- The face should show playfulness rather than confusion.

## Seedance Prompt Guidance

When writing copyable video prompts:

- Put the quoted dialogue unchanged.
- Add voice direction outside the quote, e.g. `语气低冷，句号后完全收束`.
- Avoid asking Seedance to render subtitles unless the user wants visible text.
- For long narration, mark as voiceover/audio direction rather than visible mouth sync.
- For punctuation-based pauses, use timed beats: `0-1s 凛沉默吸气`, `1-3s 台词`.
