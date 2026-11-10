# Obsidian 兼容档（Tier A / B / C）

MuseMate 对 Obsidian 社区插件采用**分级兼容**，安装前会做静态扫描并展示档位。

## Tier A — 可直接/轻量适配

适用：

- 仅 `styles.css` 的样式增强
- 只注册 Markdown 代码围栏 / post-processor，且不依赖 vault、workspace、editor 深 API

期望上游 Release 资产：`manifest.json`、`main.js`（可无逻辑）、`styles.css`（若有）。

索引字段示例：

```json
"obsidianCompat": { "tier": "A", "upstreamId": "some-plugin-id" }
```

## Tier B — 兼容层运行

适用：需要最小 Obsidian shim 的插件，例如：

- `Plugin` 生命周期
- `addCommand` / `addSettingTab`
- `loadData` / `saveData`
- `registerMarkdownCodeBlockProcessor` / `MarkdownPostProcessor`

不保证所有命令/设置 UI 像素级一致；缺失 API 会以可见错误提示，而不是静默空实现。

```json
"obsidianCompat": {
  "tier": "B",
  "upstreamId": "hotkeysplus-obsidian",
  "requiredApis": ["Plugin", "addCommand", "loadData", "saveData"]
}
```

## Tier C — 不支持

以下类型**不要**提交到索引（PR 会被拒）：

- CodeMirror 6 编辑器扩展
- Workspace Leaf / 自定义视图
- `app.vault` 任意文件系统访问
- Electron / Node API
- Dataview、Templater（任意 JS 模板引擎）、Excalidraw 整图编辑器、Kanban 深度视图等

这类需求应：

1. 重打包为 MuseMate 原生 capsule；或
2. 作为 MuseMate 官方原生功能 / 专用 adapter 讨论。

## 文案红线

- 允许：`Obsidian 分级兼容（A/B）`
- 禁止：`兼容全部 Obsidian 插件`、`可直接运行任意社区插件`
