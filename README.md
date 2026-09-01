# 宝可梦小手机论坛 — SillyTavern Extension 0.40.1

这是宝可梦小手机论坛的原生 SillyTavern 扩展版本。

## 0.40.1 兼容性加固

本版本继续**完全脱离 Tavern Helper**，并针对 Git URL 安装和新版 SillyTavern 原生 API 做了兼容性加固：

- 不依赖 `window.SillyTavern.chat`、`window.eventSource`、`window.chatMetadata` 等不稳定的全局属性。
- 直接动态加载 SillyTavern 原生 `script.js` / `world-info.js` 模块。
- 聊天正文、当前聊天 ID、角色信息、chat metadata、保存聊天、事件系统均优先使用原生模块导出。
- 聊天切换使用原生 `CHAT_CHANGED` 事件。
- 新聊天使用原生 `CHAT_CREATED` 事件。
- 世界书使用原生 World Info 模块。
- 帖子上下文使用原生 `setExtensionPrompt` 注入。
- 保留 0.40 原有论坛数据命名空间，升级不会主动清空已有论坛存档。
- API 请求保留 60 秒超时、刷新异常恢复等稳定性修复。

## Git URL 安装

这个项目可以直接作为 Git 仓库安装。

**重要：Git 仓库根目录必须直接包含：**

```text
manifest.json
index.js
style.css
README.md
```

不要再套一层 `宝可梦小手机论坛_酒馆扩展0.40.1/` 目录。

在 SillyTavern 的扩展安装窗口中：

1. 打开第三方扩展 / Git URL 安装。
2. 填入你的 Git 仓库 URL，例如：
   `https://github.com/你的用户名/宝可梦小手机论坛`
3. 如果需要让服务器上的所有用户都能使用，选择 **「为所有用户安装」**。
4. 安装完成后重启 SillyTavern 或重新加载扩展。

「为所有用户安装」是 SillyTavern 安装器决定的安装范围；扩展本身不需要 Tavern Helper，也没有额外的用户级依赖。

## 功能

- 宝可梦手机论坛 UI
- 论坛板块、帖子、楼中回复
- AI 自动生成帖子
- AI 自动生成回复
- NPC / 网友互动
- 当前聊天正文读取
- 最近 N 层正文设置
- 不同聊天独立论坛存档
- 聊天切换自动切换论坛
- 新聊天自动建立独立论坛
- 世界书选择与智能筛选
- 当前帖子注入聊天正文
- 手机时间
- 悬浮洛托姆按钮
- 独立 OpenAI-compatible API 设置

## 依赖

只依赖 SillyTavern 本体。

不安装、不调用、不要求 Tavern Helper。

## 注意

本包已经完成静态 JavaScript 语法检查、Manifest JSON 检查和 ZIP 完整性检查。

由于无法在这里直接启动你的 SillyTavern 浏览器实例，最终的实际运行兼容性仍建议在你的 SillyTavern 版本上安装后测试一次。
