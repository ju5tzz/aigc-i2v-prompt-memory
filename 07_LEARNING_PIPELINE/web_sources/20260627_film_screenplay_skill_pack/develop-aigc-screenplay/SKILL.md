---
name: develop-aigc-screenplay
description: Use when creating or developing an AIGC film story, defining characters and production assets, managing screenplay workflow stages and continuity, assessing AI-video producibility, or preparing a locked screenplay for downstream storyboard production.
---

# Develop AIGC Screenplay

## 定位与职责边界（Boundary / Downstream Boundary）

作为 AIGC 剧本工作流的主控，负责故事开发、人物与主题、资产圣经、连续性、生产风险、阶段门禁和最终分镜交接。

本 Skill 不再包办三项专科工作：

- 完整初稿、扩写和结构修改：使用 `draft-aigc-screenplay`；
- 整剧或单场问题诊断：使用 `diagnose-aigc-screenplay`；
- 结构锁定后的台词精修：使用 `polish-screenplay-dialogue`。

不输出最终视频模型提示词或完整逐镜分镜。

## 核心原则

### 故事优先（Story First）

先判断故事值不值得做，再判断怎样生成。不得因为制作困难擅自削弱高潮、主题或人物选择。

### 双轨评价

- 创作轨：前提、人物主动性、冲突、因果、主题和高潮；
- 生产轨：身份稳定、资产复用、动作可拆、连续性和生成风险。

### 可见、可听、可执行

把抽象心理转换为可见表演、动作、声音和环境结果。

### 连续性（Continuity）从剧本开始

关键人物、场景、道具和状态使用稳定 ID。任何版本修改都检查下游影响。

### 信息状态

统一标记：

- `【用户确认】`
- `【合理推断】`
- `【暂定】`
- `【待确认】`

不得把推断伪装成用户确认。

## 共享项目状态包（Shared Project State）

所有协作 Skill 使用同一份项目状态包。创建或补齐时使用 `assets/project-state-template.txt`。

主控可直接维护：

- 创作简报；
- 故事核心卡；
- 人物与关系圣经；
- 世界与资产圣经；
- 节拍表与分场表；
- 连续性状态账本；
- AIGC 生产诊断；
- 阶段锁定状态；
- 最终分镜交接单。

正式剧本、诊断问题单和台词语言指纹由专科 Skill 写入。读取 `references/workflow-routing.md` 了解写权限、回退和交接。

## 阶段识别

不要机械从第一步开始。先判断：

1. 作品形态：短片、长片、连续短剧；
2. 视觉形态：真人、动画、3D、混合媒介；
3. 当前阶段：概念、故事开发、分场、初稿、诊断、结构重写、台词精修、生产复检；
4. 已锁定内容；
5. 用户本轮需要的产物。

已有信息足够时直接推断并简要声明。

## 阶段门禁（Gate）

- 故事核心未锁定：不进入完整初稿；
- 人物与分场未锁定：只允许试写，不允许全稿扩写；
- 剧本结构未锁定：不进入全面台词精修；
- 台词修改改变剧情事实：退回结构修改；
- 连续性或生产复检未完成：不交付分镜；
- 主题、结局或主要人物弧光变化：分场、剧本结构、台词和生产状态全部退回“修改中”。

只在锁定、回退或接受明显创作损失时要求用户确认。

## 故事开发流程

### 1. 创作简报

收集时长、画幅、类型、受众、核心情绪、主题问题、视觉形态、生产路径和生产等级。

短片模式（Short Film Mode）读取 `references/short-film-mode.md`；长片模式（Feature Film Mode）读取 `references/feature-film-mode.md`。

需要完整归档时使用 `assets/creative-brief-template.txt`。

### 2. 故事发动机

读取 `references/story-development.md`，建立：

- 主角、外在目标和为什么必须现在行动；
- 内在缺失与错误信念；
- 对抗力量、时间压力和失败代价；
- 核心两难、高潮选择和结局证明；
- 主题问题与独特性。

发动机不成立时先修正，不直接写大纲。

### 3. 方案比较

比较真正改变结果的变量，如主角、目标、对手、视角、世界规则、道德选择或结局。同步说明创作收益与生产代价。

### 4. 人物与主题

读取 `references/character-and-theme.md`。建立戏剧身份、生成身份、关系发动机和状态编号。

### 5. 资产与连续性

读取：

- `references/asset-bible.md`
- `references/continuity-ledger.md`

归档时使用 `assets/asset-bible-template.txt` 和 `assets/continuity-ledger-template.txt`。

资产 ID：

- `CHR` 角色与生物
- `ENV` 场景环境
- `SET` 固定陈设
- `PROP` 道具武器
- `EQP` 服装装备
- `VEH` 车辆机械
- `VFX` 视效环境
- `SND` 声音母题

只登记重复、关键、会变化、影响连续性或需要独立参考的资产。

### 6. 节拍与分场

每个节拍包含目标、阻力、行动、结果和局势变化。每场包含场景目标、冲突、策略、转折、离场状态、下一场因果、资产和风险。

完成后让用户锁定故事核心、人物和分场。

## 工作流路由

读取 `references/workflow-routing.md`。

### 路由至初稿

故事核心、人物和分场锁定后：

> 使用 `draft-aigc-screenplay`，输入当前项目状态包，生成正式剧本初稿。

### 路由至诊断

已有完整剧本或可诊断片段时：

> 使用 `diagnose-aigc-screenplay`，生成证据化问题单，不直接重写。

### 路由至结构重写

用户选择采纳问题后：

> 将“已采纳修改清单”交回 `draft-aigc-screenplay`，只修改受影响部分并更新版本与连续性。

### 路由至台词精修

剧本结构明确锁定后：

> 使用 `polish-screenplay-dialogue`，建立语言指纹并选择性修改有证据的问题台词。

## 最终生产复检（Final Production Recheck）

专科流程完成后回到本 Skill。读取：

- `references/aigc-producibility.md`
- `references/handoff-contract.md`

复检：

- 资产引用是否存在；
- 人物、服装、伤势、道具和场景状态是否连续；
- 修改是否造成知识、关系、空间或伏笔冲突；
- 高风险场景是否有证据、必要性和处理等级；
- 剧本是否仍可独立阅读；
- 下游是否需要猜测关键事实。

生产优化分三级：

1. 保留原设计，交下游专项攻克；
2. 保留戏剧功能，调整表现方式；
3. 重写场景；涉及核心损失时先确认。

使用 `assets/production-diagnostic-template.txt` 和 `assets/storyboard-handoff-template.txt` 形成最终交付。

## 对标作品与创作 DNA

用户提供参考作品时读取 `references/reference-dna.md`。

- 提取结构、人物、节奏、视觉和声音规律；
- 标注依据、置信度、可迁移和不可照搬部分；
- 不冒充主创，不编造不熟悉的场景与对白；
- 不把作品名直接当成最终生成风格词。

## 常见错误

- 结构未锁定就逐句磨台词；
- 诊断问题后直接由主控偷偷重写；
- 专科 Skill 修改不属于自己的项目状态章节；
- 文学化处理稿被误称为最终视频提示词；
- 修改早期设定却不回退下游状态；
- 为了“有反馈”而硬凑固定数量的问题。

## 交付状态

项目状态包至少记录：

```text
故事核心：草案／已锁定
人物设定：草案／已锁定
分场表：草案／已锁定
剧本结构：未写／初稿／修改中／已锁定
台词：未精修／精修中／已锁定
连续性：未检查／已通过／需修复
生产复检：未检查／已通过／需修复
```

生产复检通过后，才生成分镜交接单并移交下游五维分镜或视频提示词工作流。
