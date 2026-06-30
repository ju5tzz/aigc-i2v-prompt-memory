# Prompt Reading Protocol

## 目标

后续把某一集剧本改写成 I2V / Seedance 分镜提示词时，避免每次读取完整 80 集剧本，同时避免人物关系、道具状态和长线剧情断裂。

## 默认读取包

写第 N 集时默认读取：

1. `06_ASSET_NOTES/queen_contract/README.md`
2. `06_ASSET_NOTES/queen_contract/PROJECT_OVERVIEW.md`
3. `06_ASSET_NOTES/queen_contract/CHARACTER_BIBLE.md`
4. `06_ASSET_NOTES/queen_contract/CONTINUITY_LEDGER.md`
5. `06_ASSET_NOTES/queen_contract/EPISODE_INDEX.md` 中第 N 集及前后一集
6. `00 FILES/projects/queen_contract/episodes/EP{N:03}.md`

## 什么时候追加读取

- 如果当前集开头强承接上一集：追加 `EP{N-1:03}.md`。
- 如果当前集结尾需要为下一集做钩子：追加 `EP{N+1:03}.md`。
- 如果涉及某个长线道具或状态：读 `CONTINUITY_LEDGER.md` 对应段落。
- 如果是新角色首次出场或关系反转：读 `CHARACTER_BIBLE.md` 对应角色。
- 如果用户给了新的分镜稿、故事板或反馈：以用户最新文件覆盖这里的旧索引。

## 写提示词前的判断

必须先判断：

- 当前片段只覆盖哪一个连续事件。
- 是否需要当前片段前置信息。
- 是否需要环境参与。
- 是否需要脸部近景 / 反应特写。
- 是否需要表情层。
- 镜头数量和时长是否能承载动作与情绪。
- 是否需要故事板支持。

## 正式提示词边界

- 只输出提示词正文层。
- 不写任何平台资产绑定标签。
- 不写参考对象职责表，除非用户明确要求。
- 不生成字幕，除非用户明确要求字幕作为画面元素。
- 保留人物名用于台词归属和调度，但不反复重写完整外貌。
