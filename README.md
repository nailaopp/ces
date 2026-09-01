# 宝可梦小手机论坛（SillyTavern 扩展版）

从「酒馆助手」脚本 **测试论坛 0.39 正文读取与时间修正版** 完整转换而来的 **原生 SillyTavern 扩展**。

**不再依赖酒馆助手（Tavern Helper）**，所有聊天读取、世界书、元数据保存、提示词注入、聊天切换事件均使用 SillyTavern 官方 `getContext()` / `setExtensionPrompt` / `eventSource` API。

## 功能概览

- 洛托姆风格悬浮手机按钮（支持拖动、Android 触摸）
- 安全论坛 + 成熟向论坛双区
- 按板块刷新/生成帖子、玩家发帖与回复、NPC 互聊
- 读取当前聊天正文（可配置层数）+ 智能世界书筛选
- 独立 API 配置（Endpoint / Key / 模型），与酒馆主连接分离
- 按聊天独立存档（chatId 绑定 + localStorage + chatMetadata 备份）
- 帖子注入正文（`setExtensionPrompt`，IN_CHAT）
- 设置页：深度、世界书、生成数量、身份昵称、板块提示词等

## 安装

### 方式一：手动安装（推荐）

1. 将整个 `pkmn-phone-forum` 文件夹复制到：
   - `SillyTavern/data/<你的用户名>/extensions/pkmn-phone-forum/`  
     **或**
   - `SillyTavern/public/scripts/extensions/third-party/pkmn-phone-forum/`
2. 重启或刷新 SillyTavern 页面。
3. 打开顶部 **扩展** 面板，找到并 **启用**「宝可梦小手机论坛」。
4. 页面右下角出现洛托姆手机图标即可使用。

### 方式二：Git 安装

在扩展面板「安装扩展」中粘贴你自己托管的仓库地址（需包含本目录的 `manifest.json`）。

## 使用说明

1. 点击悬浮洛托姆按钮打开手机界面。
2. 进入「设置」配置：
   - **API Endpoint**（例如 `https://api.openai.com/v1` 或中转地址）
   - **API Key**
   - 点击「检测连接」→「加载模型」→ 选择模型 →「保存 API」
   - 选择要使用的世界书、正文读取层数、刷新帖子数等
3. 选择「宝宝宝可萌大师」（安全）或「91宝可梦论坛」（成熟向）。
4. 点击「✨刷新/生成」生成当前板块帖子；可发帖、回复、NPC 互聊。
5. 在帖子详情中可将当前帖注入正文，让角色“知道”论坛内容。

## 与原脚本的差异

| 原酒馆助手 API | 扩展中的实现 |
|----------------|--------------|
| `getChatMessages` | `SillyTavern.getContext().chat` 切片 |
| `getWorldbookNames` / `getWorldbook` | `world_names` + 动态 `import('/scripts/world-info.js').loadWorldInfo` |
| `eventOn(CHAT_CHANGED / CHAT_CREATED)` | `context.eventSource.on(event_types.CHAT_CHANGED / CHAT_CREATED)` |
| `injectPrompts` / `uninjectPrompts` | `context.setExtensionPrompt`（IN_CHAT, depth 0） |
| `updateChatMetadata` / `saveChat` | `context.updateChatMetadata` + `context.saveChat` |
| 内联 CSS | 独立 `style.css`，由 `manifest.json` 加载 |

数据命名空间仍为 `pkmn_phone_forum_v9`，可尽量兼容旧存档（localStorage 与 chatMetadata）。

## 兼容性

- 建议 SillyTavern **1.12+**
- 世界书读取依赖前端可访问 `/scripts/world-info.js` 的 `loadWorldInfo`
- 若某版本 `setExtensionPrompt` 参数顺序或枚举值不同，注入功能可能需微调（见 `index.js` 中 TH.injectPrompts）

## 文件结构

```
pkmn-phone-forum/
├── manifest.json   # 扩展元数据
├── index.js        # 主逻辑（原生 ST 适配层 + 原论坛完整功能）
├── style.css       # 手机 UI 样式
└── README.md
```

## 版本

- **0.40.0**：首个脱离酒馆助手的扩展构建（基于脚本 0.39）

## 许可与声明

原脚本为社区酒馆助手脚本转换而来。请遵守 SillyTavern 扩展相关规范与当地法律法规。成熟向板块已限制不生成露骨色情内容，但仍请自行负责使用场景。
