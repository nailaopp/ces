# 宝可梦小手机论坛（SillyTavern Extension）

这是把原「测试论坛0.38 稳定性与并发修复版」酒馆助手脚本转换成的 SillyTavern 第三方 UI Extension。

## 安装

在 SillyTavern：

1. 打开 **扩展（Extensions）**。
2. 选择 **Install Extension / 安装扩展**。
3. 填入本仓库的 Git URL。
4. 安装后重新加载/重启 SillyTavern。

仓库根目录必须直接包含 `manifest.json` 和 `index.js`。

## 与原脚本的兼容处理

- 保留原论坛 UI、论坛数据、AI 生成、世界书筛选、聊天切换隔离、帖子注入等主要逻辑。
- 扩展不再强制要求酒馆助手存在：聊天读取、聊天 ID、聊天 metadata、聊天切换事件、提示词注入优先使用 SillyTavern 原生上下文接口。
- 如果安装了酒馆助手，则继续优先使用酒馆助手提供的增强接口，尤其是世界书读取。
- 修复原脚本中的 `trackedSetInterval` 自递归调用问题。
- API Key 仍由原脚本的本地配置机制保存；请不要把含真实 API Key 的配置文件提交到 GitHub。

## 注意

世界书智能读取仍依赖可用的酒馆世界书接口；若当前 SillyTavern 版本没有暴露对应接口且没有安装酒馆助手，论坛主体功能仍可使用，但世界书选择功能可能显示不可用。
