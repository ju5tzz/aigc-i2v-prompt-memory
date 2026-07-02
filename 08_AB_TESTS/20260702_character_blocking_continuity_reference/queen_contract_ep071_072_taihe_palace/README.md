# 皇后契约 EP071-072 太和殿台阶站位参考测试

> 建立日期：2026-07-02
> 当前状态：待真实 I2V 生成验证
> 对应场景：第 71 集后半段至第 72 集全集，太和殿广场与台阶顶部

## 测试背景

本轮测试要解决的问题不是“模型是否理解台阶”本身，而是：在同一张太和殿母场景图中，如何用图像参考精确告诉模型，苏瑾和萧珩正在参考图的哪个区域对话。

仅用文字写“二人站在台阶最高处”，目前仍不足以稳定锁定位置。模型容易把人物放到台阶中段、殿门前错误区域、广场空地，或者在镜头切换后重置空间关系。

因此本轮测试采用“母场景图 + 站位参考图”的方式，将第 71 集后半段和第 72 集拆成几个空间状态，并分别验证哪种参考图最能帮助模型锁定人物位置。

## 母场景

- 母场景图：`assets/mother_scene_taihe_palace.png`
- 场景含义：太和殿正面、中央长台阶、底部广场、中段台阶、顶部平台与殿门。
- 画幅用途：作为统一空间母版，不直接等同最终 9:16 镜头构图。

## 三个对话位置

| 状态 | 剧情位置 | 空间位置 | 主要用途 |
| --- | --- | --- | --- |
| A | 台阶底部，二人对话 | 中央台阶最下方，广场与台阶交界处 | 第 71 集，萧珩走下台阶到苏瑾面前 |
| B | 台阶中部，二人登阶上殿 | 中央长台阶中段 | 第 71 集，两人并肩登阶，旧臣反应 |
| C1 | 台阶顶部，二人站定对话 | 中央台阶最高处，殿门前平台 | 第 72 集开场，二人面对百官 |
| C2 | 台阶顶部，单膝跪地求婚 | 同 C1，但萧珩跪在苏瑾面前 | 第 72 集核心求婚段落 |

## 参考图分层

### 给模型看的参考图

模型参考图尽量不放文字标签，避免生成视频里出现文字污染。

颜色规则：

- 红色剪影：苏瑾。
- 黑金剪影：萧珩。
- 蓝色剪影：礼官。
- 剪影只表示站位、远近、朝向和动作关系，不表示人物外貌、服装和五官。

可用文件：

| 状态 | 全景站位图 | 裁切放大图 |
| --- | --- | --- |
| A | `assets/model_ref_A_bottom_dialogue_marker.png` | `assets/model_ref_A_bottom_dialogue_crop_marker.png` |
| B | `assets/model_ref_B_mid_stairs_marker.png` | `assets/model_ref_B_mid_stairs_crop_marker.png` |
| C1 | `assets/model_ref_C1_top_platform_standing_marker.png` | `assets/model_ref_C1_top_platform_standing_crop_marker.png` |
| C2 | `assets/model_ref_C2_top_platform_kneeling_marker.png` | `assets/model_ref_C2_top_platform_kneeling_crop_marker.png` |
| ABC 平面辅助 | `assets/model_ref_ABC_flat_map_marker.png` | 无 |

### 给人看的规划图

人类规划图允许保留文字、框线和说明，用来检查站位是否符合剧情，不建议直接作为 I2V 模型参考图。

可用文件：

- `assets/human_plan_ABC_full_labeled.png`
- `assets/human_plan_ABC_flat_map_labeled.png`
- `assets/human_plan_A_bottom_dialogue_labeled.png`
- `assets/human_plan_B_mid_stairs_labeled.png`
- `assets/human_plan_C1_top_platform_standing_labeled.png`
- `assets/human_plan_C2_top_platform_kneeling_labeled.png`

## 第一轮优先测试

第一轮不要一次叠加太多参考图。建议从最容易出错的 C 位开始：

1. 对照组：只用文字说明“二人站在太和殿台阶最高处、殿门前平台”。
2. 实验组 1：加入 `model_ref_C1_top_platform_standing_crop_marker.png`。
3. 实验组 2：加入 `model_ref_C2_top_platform_kneeling_crop_marker.png`。
4. 可选实验组 3：加入 `model_ref_ABC_flat_map_marker.png` 作为辅助平面图。

判断重点不是画面华丽程度，而是人物是否真的落在台阶最高处、殿门前平台，且不滑到台阶中段或广场底部。

## 暂不升级为规则

本目录中的站位图方法仍属于测试方案。只有在第 71-72 集真实生成中反复证明有效后，才可考虑写入 `09_SKILLS/i2v-prompt-workflow/SKILL.md` 或 `01_ACTIVE_RULES/`。
