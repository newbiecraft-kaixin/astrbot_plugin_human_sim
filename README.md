# astrbot_plugin_human_sim

AstrBot 4.x 插件，让机器人在群里像普通群友：多数时间不说话，偶尔接一句，被拍会回拍。发言频率受概率、冷却、每分钟上限、活动时段四项限制。

仓库从 [dafeiyu-open](https://github.com/newbiecraft-kaixin/dafeiyu-open) 拆出，代码相同。

## 功能

- 插话：按上述四项限制决定要不要发言，发言前随机等 4~20 秒，带上最近群聊内容
- 冷场时主动起一个话题
- 回复可以带 QQ 黄脸或本地表情包
- 拍一拍：被拍会回戳、同一人连拍会回戳，回完话顺手拍回去；“拍拍我”“戳我”这类纯动作在本地处理，不调用模型
- 活动时段之外不发言
- 频控计数和冷却时间写入磁盘，重启不清零

## 安装

1. WebUI → 插件 → 插件市场，搜索 `human_sim`
2. 或在“从 URL 安装”里填 `https://github.com/newbiecraft-kaixin/astrbot_plugin_human_sim`

装好后到插件配置页填要启用的群。默认不启用，不填群不会发言。

## 配置

配置项在 AstrBot 插件配置页，字段说明和推荐值见 [参数说明.md](参数说明.md)。常用的几项：

| 配置 | 作用 |
| --- | --- |
| 启用群列表 | 只在列出的群里活动 |
| 活动时段（起止小时） | 时段外不发言 |
| 插话概率 / 冷场开话头概率 | 主动程度 |
| 冷却秒数 / 每分钟上限 | 发言频率上限 |
| 夜间降频 | 深夜减少发言 |

## 搭配的其他插件（可选）

以下插件装了效果更完整，不装也能运行，只是对应功能不生效：

- [astrbot_plugin_humanizer](https://github.com/newbiecraft-kaixin/dafeiyu-open/tree/main/astrbot_plugins/astrbot_plugin_humanizer)：清理 Markdown、去 AI 腔
- `astrbot_plugin_speaker_tag`：给消息加昵称、时间
- `astrbot_plugin_group_window`：记录群聊窗口，作为上下文
- `astrbot_plugin_sticker_pack`：表情包库
- `astrbot_plugin_basic_tools`：超级表情和基础工具
- `data/plugin_data/fy_send_gate.py`：发送节流，没有就不节流

## 已知问题

- 只在 `aiocqhttp`（NapCat / OneBot）适配器下测试过，其他平台的动作类接口不一定支持
- 频控默认值偏保守，需要按群的活跃度调整

## 许可与来源

AGPL-3.0，见 [LICENSE](LICENSE)。

本项目是 [dafeiyu-open](https://github.com/newbiecraft-kaixin/dafeiyu-open) 的一部分，单独建仓库为了发布到插件市场。开发时使用 [AstrBot](https://github.com/AstrBotDevs/AstrBot)（AGPL-3.0）的插件接口，没有分发 AstrBot 自身的代码。署名见 [NOTICE.md](NOTICE.md)。
