# Extraction Report - BV183KS66EeZ

## 抓取概况

- 视频：08-AI人物真实表情精确控制
- 来源：https://www.bilibili.com/video/BV183KS66EeZ/
- 作者：GK迷
- 时长：265 秒
- 公开字幕：无
- 替代方式：音频转文字
- 视觉处理：2 秒采样抽帧、场景变化抽帧、关键帧筛选、关键帧 OCR、视觉核对

## 保存内容

- 元数据：`raw/view.json`
- 播放流信息：`raw/playurl.json`
- 音频转文字：`raw/asr_transcript.txt` / `raw/asr_segments.json`
- 视频文件：`media/video_merged.mp4`
- 音频文件：`media/audio_16k.wav`
- 2 秒采样帧：`frames/sample_2s/`，132 张
- 场景变化帧：`frames/scene/`，63 张
- 人工筛选关键帧：`frames/selected/`，29 张
- 关键帧拼图：`frames/contact_sheets/`，4 张
- OCR 结果：`ocr/selected_frames_ocr.md` / `ocr/selected_frames_ocr.json`
- 视觉笔记：`visual_notes.md`
- 检索索引：`manifest.jsonl`
- 完整转录索引：`../../transcripts/20260629_bilibili_micro_expression_control_transcript.md`
- 总结分析：`../../summaries/20260629_bilibili_micro_expression_control_summary.md`
- 可迁移规则：`../../extracted_rules/20260629_bilibili_micro_expression_control_extracted_rules.md`

## 提取数量

- 文字块：130 条音频转文字片段
- 图片帧：132 张 2 秒采样帧，63 张场景变化帧，29 张筛选关键帧
- OCR 图片：12 张关键文字帧
- 视频：成功保存 1 个合并视频文件
- 音频：成功保存 1 个转码音频文件

## 限制与误差

- B站公开字幕列表为空，因此没有官方字幕文件。
- 公开视频流只抓到 480p，本地为了 OCR 将帧放大到 1704x960，但原始画面清晰度仍有限。
- 音频转文字存在少量错字，例如“提示词”“嘴角斜挑”等需要结合画面校正。
- OCR 对小字号中文存在错别字，最终总结已用视觉检查和上下文校正。
- 全量 132 帧 OCR 耗时过长，已改用关键帧 OCR。对本视频而言，核心信息集中在模板页和示例页，关键帧 OCR 足够覆盖主要内容。

## 后续使用建议

后续总结或构建知识库时，应优先阅读：

1. `transcripts/20260629_bilibili_micro_expression_control_transcript.md`
2. `summaries/20260629_bilibili_micro_expression_control_summary.md`
3. `extracted_rules/20260629_bilibili_micro_expression_control_extracted_rules.md`
4. `web_sources/20260629_bilibili_micro_expression_control/frames/contact_sheets/`

如果要进一步固化为正式提示词 Skill，应先做实测，不要直接把外部视频的 `@` 格式、UE5/LibTV 风格词或批量生成流程写进 Active Rules。
