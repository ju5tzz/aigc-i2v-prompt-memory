# 影视剧本 Skill 包索引

这是从当前 Codex 本地技能库整理出的影视剧本/AIGC 视频创作工作流包。包内每个 skill 目录都保持在顶层，方便直接复制到 `.codex/skills` 使用。

## 核心剧本工作流

1. `develop-aigc-screenplay`
   - 用途：故事开发主控、人物和主题设计、资产圣经、连续性、生产风险、阶段门禁和最终分镜交接。
   - 适合：从概念、故事核心、人物关系、分场表到下游交接的统筹。

2. `diagnose-aigc-screenplay`
   - 用途：诊断剧本、故事大纲、场次、段落的问题。
   - 适合：找出结构、人物、节奏、观众理解、原创性和 AIGC 生产风险，不直接重写。

3. `draft-aigc-screenplay`
   - 用途：把已锁定的故事核心、人物和分场扩写为正式剧本，或按已采纳问题清单进行局部重写。
   - 适合：初稿、续写、压缩、局部结构修改、版本交接。

4. `polish-screenplay-dialogue`
   - 用途：在剧本结构锁定后精修台词。
   - 适合：人物声纹、潜台词、冲突、节奏、信息效率、口型和视频段落切分优化。

## 下游分镜与视频提示词

5. `five-dimension-storyboard`
   - 用途：把剧本、场景、大纲或对白转成五维度影视分镜表或可复制镜头提示词。
   - 适合：保真分镜、角色表演节拍、镜头拆解、后续 Seedance 提示词上游准备。

6. `qingdaofu-storyboard`
   - 用途：按“清道夫”模板生成工业化分镜提示词。
   - 适合：资产锁定、竖屏调度、微表演、环境参与、时间预算和物理连续性要求较高的分镜。

7. `seedance-shot-prompt`
   - 用途：把分镜转成 Seedance 2.0 可生产提示词，并调试角色一致性、首尾帧、参考图/视频/音频等。
   - 适合：Seedance 2.0 实拍感镜头提示词、固定机位、时间节拍、中文对白等工作。

8. `ap-aigc-prompt`
   - 用途：生成 Seedance 与 GPT-Image-2 生产级 AIGC 视频分镜/提示词。
   - 适合：镜头拆解、资产提取、角色参考图、关键帧、遮罩转场和提示词清理。

## 推荐调用顺序

```text
develop-aigc-screenplay
  -> diagnose-aigc-screenplay
  -> draft-aigc-screenplay
  -> polish-screenplay-dialogue
  -> five-dimension-storyboard / qingdaofu-storyboard
  -> seedance-shot-prompt / ap-aigc-prompt
```

## 安装方式

将本包内除 `_PACK_INDEX.md` 之外的 skill 目录复制到：

```text
C:\Users\1\.codex\skills
```

复制后重新打开或刷新 Codex，skill 会按各自 `SKILL.md` 的 description 自动触发。
