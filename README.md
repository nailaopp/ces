# 宝可梦小手机论坛 — SillyTavern Extension 0.40.0

这是原 0.39 论坛脚本的**完全脱离 Tavern Helper 原生扩展版**。

## 依赖

- 只依赖 SillyTavern 本体。
- 不安装、不调用、不要求 Tavern Helper。
- 世界书读取使用 SillyTavern 原生 `world-info.js` 模块与 `/api/worldinfo/get`。
- 帖子正文注入使用 SillyTavern 原生 `setExtensionPrompt`。
- 聊天正文、聊天 ID、metadata、保存和事件使用 SillyTavern 原生接口。

SillyTavern 的 World Info 本身就是原生的动态提示词系统；本扩展直接读取已选择的世界书数据，并按论坛原有的智能筛选逻辑选择相关条目。citeturn0search0

## 安装

把整个 `宝可梦小手机论坛_酒馆扩展0.40.0` 文件夹复制到：

`public/scripts/extensions/third-party/`

然后重启 SillyTavern，在“扩展”面板启用“宝可梦小手机论坛”。

## 保留功能

- 宝可梦手机论坛完整 UI
- 论坛板块、帖子、楼中回复
- AI 自动生成帖子
- AI 自动生成回复
- NPC/网友互动
- 当前聊天正文读取
- 最近 N 层正文设置
- 不同聊天独立论坛存档
- 聊天切换自动切换论坛
- 新聊天自动建立独立论坛
- 世界书选择与智能筛选
- 当前帖子注入聊天正文
- 手机时间
- 悬浮洛托姆按钮
- OpenAI-compatible 独立 API 设置

## 原生注入

帖子注入不修改聊天历史，而是通过 SillyTavern 原生扩展提示注入机制加入当前生成上下文。SillyTavern 的扩展生态本身也使用 `setExtensionPrompt` 进行这类上下文注入。citeturn7search1

## 世界书

世界书列表和内容直接从 SillyTavern 原生 World Info 模块读取。当前版本的 SillyTavern 提供 `loadWorldInfo(name)`，并通过 `/api/worldinfo/get` 获取世界书数据；世界书名称也由原生 World Info 状态维护。citeturn4view0

## API

论坛自己的 AI 请求仍使用论坛设置中的 OpenAI-compatible Endpoint / API Key / Model。它不会强制切换到 SillyTavern 当前主 API。

## 数据

论坛状态继续使用自己的 localStorage 命名空间，并在可用时写入当前聊天 metadata，因此不同聊天可以保持独立论坛。

## 版本说明

0.40.0 的核心目标不是重新设计论坛，而是把 0.39 的 Tavern Helper 依赖全部移除，改为 SillyTavern 原生实现。
