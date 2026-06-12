# 07 Learning Pipeline

本模块用于从 YouTube / B站 / 微信文章 / 其他公开教程中学习 AIGC、I2V、多参考、故事板、提示词工程相关经验。

这里沉淀的是“待验证经验”，不是正式规则。外部教程中的观点只能先进入本模块，不能直接写入 `01_ACTIVE_RULES/`。

## 核心原则

1. 优先抓取视频字幕。
2. 没有字幕时，才提取音频并转录。
3. 摘要和规则提炼必须分开保存。
4. 外部教程经验默认进入“待验证”。
5. 只有经过用户实测反馈后，经验才允许上升到 `01_ACTIVE_RULES/`。

## 目录说明

```text
07_LEARNING_PIPELINE/
  README.md
  video_urls.md
  VIDEO_LEARNING_RECORD_TEMPLATE.md
  transcripts/
  summaries/
  extracted_rules/
  web_sources/
  scripts/
```

- `video_urls.md`：记录待学习、已学习、待复核的视频链接。
- `transcripts/`：保存字幕或转录文本。
- `summaries/`：保存视频内容摘要。
- `extracted_rules/`：保存从视频中提炼出的待验证经验。
- `web_sources/`：保存用户提供的本地网页、文章配图和图转文来源资产。
- `scripts/`：保存给 Codex 使用的执行提示词、流程提示或辅助说明。

## 视频学习流程

### 1. 登记视频

收到视频链接后，先在 `video_urls.md` 中登记：

- 视频标题
- 平台
- URL
- 作者
- 发布时间
- 当前状态
- 学习优先级

如果标题、作者、发布时间无法确认，先留空，不要编造。

### 2. 获取文本来源

优先级如下：

1. 官方人工字幕
2. 平台自动字幕
3. 音频提取后转录

只有在无法获得字幕或自动字幕质量明显不可用时，才进入音频转录流程。

字幕或转录文本保存到：

```text
07_LEARNING_PIPELINE/transcripts/
```

建议文件命名：

```text
YYYYMMDD_platform_short-title_transcript.md
```

### 3. 生成摘要

摘要只回答“这个视频讲了什么”，不要在摘要阶段改写成规则。

摘要应包含：

- 视频主题
- 章节结构
- 核心观点
- 关键案例
- 与 AIGC / I2V / 多参考 / 故事板 / 提示词工程的相关性

摘要保存到：

```text
07_LEARNING_PIPELINE/summaries/
```

### 4. 提炼待验证经验

规则提炼只回答“哪些经验可能值得验证”，不要直接写入正式规则。

待验证经验应包含：

- 原始观点
- 可迁移到 I2V 的假设
- 适用条件
- 不适用场景
- 与现有规则的关系
- 建议实验方式
- 当前状态：待验证 / 已验证 / 不适用

待验证经验保存到：

```text
07_LEARNING_PIPELINE/extracted_rules/
```

### 5. 实测反馈后再升级

外部教程经验必须经过用户在真实 I2V 任务中的实测反馈。

只有当用户明确反馈某条经验有效，并且它具有可复用价值时，才可以考虑把它整理进：

```text
01_ACTIVE_RULES/
```

未经实测反馈，不允许直接修改 `01_ACTIVE_RULES/`。

## 禁止事项

- 不要把视频观点直接写入 `01_ACTIVE_RULES/`。
- 不要把摘要和规则提炼混在同一个文件中。
- 不要把作者观点当作已经验证的内部经验。
- 不要为了填满模板而猜测视频信息。
- 不要保存与 I2V、AIGC、故事板、提示词工程无关的泛泛内容。

