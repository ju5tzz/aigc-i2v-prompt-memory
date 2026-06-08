# I2V Prompt Memory

本仓库是 AIGC / I2V 创作的长期记忆库，用于让 Codex 在每次撰写、分析、优化 I2V 提示词前，读取最新规则、模板、案例和用户反馈。

本仓库的目标不是保存零散资料，而是沉淀一套会持续进化的提示词工作系统。

## 使用方式

每次开始 I2V 提示词任务前，先读取：

1. `00_PROJECT_BRIEF.md`
2. `01_ACTIVE_RULES/`
3. `02_TEMPLATES/`
4. 与当前任务相近的 `04_CASE_LIBRARY/` 案例
5. 必要时读取 `05_FEEDBACK_MEMORY/`

每次获得生成反馈后，必须判断反馈属于哪一类：

- 个案问题：记录到对应案例。
- 可复用经验：沉淀到 `05_FEEDBACK_MEMORY/`。
- 已验证的新规则：更新到 `01_ACTIVE_RULES/`。
- 模板层面的改进：更新到 `02_TEMPLATES/`。

## 当前版本

v0.1：初始建档。

本版本已完成：

- 归档现有说明文档和故事板图片样例。
- 建立 I2V 核心规则。
- 建立反预训练拦截规则。
- 建立标准提示词模板。
- 建立故事板生成模板。
- 建立反馈记录模板。

## 仓库结构

```text
i2v-prompt-memory/
  00_PROJECT_BRIEF.md
  01_ACTIVE_RULES/
  02_TEMPLATES/
  03_STORYBOARD_GUIDE/
  04_CASE_LIBRARY/
  05_FEEDBACK_MEMORY/
  06_ASSET_NOTES/
  99_SOURCE_DOCS/
```

## 工作原则

I2V 提示词应像一份简化后的拍摄执行单。

它不是文学描写，不是导演阐释，不是情绪分析，而是让 I2V 模型明确执行当前 15 秒以内的视频事件。
