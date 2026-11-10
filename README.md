# MuseMate Plugins Index

MuseMate（macOS Markdown 编辑器）的官方插件/主题/模板索引仓。

应用从本仓库读取 `plugins.json`，再按条目去安装：

- GitHub 源：`repo` = `owner/repo`，按 Release tag（与版本号一致）下载资产
- npm 源：`npm` = 包名（应用侧会钉版本 + integrity）

> 本仓**不托管**完整插件运行时源码，只做目录与校验。设计说明见 MuseMate 仓库的 `docs/plugin-system.md`。

## 兼容性声明

- MuseMate 是沙箱原生 SwiftUI 应用，**不是** Obsidian / Logseq / Joplin 宿主。
- 原生包使用 Capability Capsules：`preview` / `transform` / `process`，以及无 JS 的 `theme` / `template`。
- Obsidian 社区插件仅支持 **Tier A / Tier B** 分级兼容（见 `COMPAT.md`），不承诺全量运行。

## 仓库结构

```text
plugins.json          # 主索引（应用读取）
categories.json       # 分类定义
COMPAT.md             # Obsidian 兼容档说明
schemas/              # JSON Schema
examples/             # 清单示例
.github/workflows/    # PR 校验
```

## 提交插件（社区 PR）

1. Fork 本仓。
2. 在 `plugins.json` 的 `packs` 数组追加一条（字段见 `schemas/plugins.schema.json`）。
3. 确保：
   - `id` 全局唯一；
   - 至少提供 `repo` 或 `npm` 之一；
   - `kind` / `runtimes` / `categories` 合法；
   - Obsidian 兼容包填写 `obsidianCompat.tier`（`A` 或 `B`），并保证上游 Release 含 `manifest.json` + `main.js`（及可选 `styles.css`）；
   - 原生包的 GitHub Release 含 `musemate.plugin.json` 与声明资产，且 tag == `version`。
4. 打开 PR。CI 会校验 JSON Schema 与基础字段；维护者会做人工审核（安全、权限、兼容档是否诚实）。

## 应用侧安装路径

安装后的包落在：

```text
~/Library/Application Support/Muse Mate/packs/<id>/
```

## 状态

索引仓已创建；MuseMate 客户端插件运行时仍按 `docs/plugin-system.md` 分阶段实现。当前 `plugins.json` 仅含占位/示例条目，不代表已全部上架可安装。
