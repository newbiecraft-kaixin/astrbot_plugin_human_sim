# astrbot_plugin_human_sim

**在群里模拟真人**：潜水观察、冷场才开话头、被拍会回拍、冒泡带 QQ 表情。所有主动行为都受「概率 + 冷却 + 每分钟限额 + 活动时段」四重闸门约束，不会刷屏。

AstrBot 4.x 插件。本仓库从 [dafeiyu-open](https://github.com/newbiecraft-kaixin/dafeiyu-open) 拆出，代码相同。

## 它做什么

- **潜水与插话**：默认不抢话，按频控决定要不要说话；插话前随机延迟 4~20 秒，带最近群聊上下文，接话要接得住
- **冷场开话头**：群里长时间没人说话时主动起话题
- **冒泡表情**：发言可带 QQ 黄脸 / 本地表情包
- **拍一拍全链路**：被拍必回（回戳 / 冒话 / 甩表情）、同一人连拍回戳、回完顺手拍一下；「拍拍我 / 戳我」这类纯动作在本地处理，不进大模型
- **夜间静默**：活动时段之外不说话，真人是会睡觉的
- **状态落盘**：频控计数、冷却时间、冷场判断都写盘，重启不清零

## 安装

1. AstrBot WebUI → 插件 → 插件市场，搜索 `human_sim`；
2. 或在「从 URL 安装」里填：`https://github.com/newbiecraft-kaixin/astrbot_plugin_human_sim`

装完在 AstrBot 的插件配置页填要启用的群，插件默认是关闭状态，不填群不会说话。

## 配置

配置项在 AstrBot 插件配置页（`config.json` 同名），完整字段说明、推荐取值和调参思路见 [参数说明.md](参数说明.md)。

最常用的几项：

| 配置 | 作用 |
| --- | --- |
| 启用群列表 | 只在列出的群里活动 |
| 活动时段（起止小时） | 时段外完全静默 |
| 插话概率 / 冷场开话头概率 | 决定主动程度 |
| 冷却秒数 / 每分钟上限 | 硬性防刷屏 |
| 夜间降频 | 深夜保持安静 |

## 可选搭配

以下插件是增强项，**不装也能单独运行**（对应能力不生效）：

- [astrbot_plugin_humanizer](https://github.com/newbiecraft-kaixin/dafeiyu-open/tree/main/astrbot_plugins/astrbot_plugin_humanizer) — 去 AI 腔、清 Markdown
- `astrbot_plugin_speaker_tag` — 给消息补「昵称 / 时间」标签
- `astrbot_plugin_group_window` — 被动记录群聊窗口做上下文
- `astrbot_plugin_sticker_pack` — 表情包库
- `astrbot_plugin_basic_tools` — 超级表情与基础工具
- 发送节流模块 `data/plugin_data/fy_send_gate.py`（可选，缺省时不节流）

## 已知限制

- 只在 `aiocqhttp`（NapCat / OneBot）适配器下测试过；其他平台的动作类接口不一定支持
- 频控参数需要按群活跃度调，默认值偏保守

## 许可与来源

AGPL-3.0，见 [LICENSE](LICENSE)。

本项目是 [dafeiyu-open](https://github.com/newbiecraft-kaixin/dafeiyu-open) 的一部分，单独拆仓以便插件市场分发。基于 [AstrBot](https://github.com/AstrBotDevs/AstrBot)（AGPL-3.0）的插件接口开发，未分发 AstrBot 本体代码。完整署名见 [NOTICE.md](NOTICE.md)。
