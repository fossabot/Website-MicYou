---
title: 更新日誌 - MicYou 版本歷史
description: MicYou 更新日誌，查看所有版本的新功能、改進和修復內容。
keywords: MicYou更新日誌,MicYou版本更新,MicYou新功能,MicYou更新記錄
aside: false
---

# Changelog

## [v1.1.5](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.5)

**Update Date:** 2026/03/08 22:54

### 主要功能
- 首次启动引导 - 新用户引导弹窗
- 自动检查更新 - 支持应用内更新
- 增益控制 (AGC) - 音频自动增益控制功能
- 快速设置 Tile - Android 快速设置快捷操作

### 核心优化
- 音频处理重构 - Ulunas 改用 Kotlin 实现

### What's Changed
* 补全繁体中文及粤语本地化 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/125
* Translate visualizer and background settings to Chinese by @Jack-Huang-2020 in https://github.com/LanRhyme/MicYou/pull/127
* feat: 添加移动端保持屏幕常亮功能 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/132
* feat: 添加快速设置Tile服务及相关功能 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/135
* ref: 重构文档结构 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/137
* docs: 优化贡献指南和常见问题部分的描述，提升可读性 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/138
* refactor(audio): migrate ONNX to Maven, update Ulunas to Kotlin, add JTransforms by @a2heng in https://github.com/LanRhyme/MicYou/pull/139
* feat(音频处理): 实现增益控制功能并重构放大器效果器 by @a2heng in https://github.com/LanRhyme/MicYou/pull/141
* feat: 添加OLED优化功能，支持深色模式下使用纯黑背景 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/140
* docs: 添加 Issue 模板 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/142
* feat: 应用内更新 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/143


**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.1.4...v1.1.5

## [v1.1.4](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.4)

**Update Date:** 2026/03/03 14:36

### 主要更新
* UI大改
* 增加悬浮窗功能
* 增加自定义背景功能
* 增加音频可视化样式选择功能
* 增加毛玻璃效果开关
* 部分bug修复
### 其他内容
* i18n(en): polish wording and add missing cancel key by @PabloLIONA in https://github.com/LanRhyme/MicYou/pull/103
* chore(i18n): 从Crowdin更新翻译 by @github-actions[bot] in https://github.com/LanRhyme/MicYou/pull/108
* Update closeConfirmCancel message in strings_cat.json by @Jack-Huang-2020 in https://github.com/LanRhyme/MicYou/pull/111
* Replace local image paths with GitHub image links by @Jack-Huang-2020 in https://github.com/LanRhyme/MicYou/pull/113
* Revert "Replace local image paths with GitHub image links" by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/116
* Optimize screenshot localization. by @Jack-Huang-2020 in https://github.com/LanRhyme/MicYou/pull/117
* fix: Windows 防火墙检查优化和对话框显示改进 by @moumoum0 in https://github.com/LanRhyme/MicYou/pull/120
* chore(i18n): 从Crowdin更新翻译 by @github-actions[bot] in https://github.com/LanRhyme/MicYou/pull/122

### New Contributors
* @PabloLIONA made their first contribution in https://github.com/LanRhyme/MicYou/pull/103
* @moumoum0 made their first contribution in https://github.com/LanRhyme/MicYou/pull/120

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.1.3...v1.1.4

## [v1.1.3](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.3)

**Update Date:** 2026/02/27 23:04

这个版本我们重构了 PC 端的 UI 界面， 完善了各平台的的 Ulunas 降噪实现，重构了托盘实现，并修复了一众 Bug 。

### 新增功能
- macOS ONNX 降噪 - 新增对 macOS 平台的 ONNX 降噪支持
- 袖珍模式 - 桌面版新增袖珍模式切换功能
- HEX 颜色自定义 - 调色盘支持 HEX 颜色值自定义输入
- 深色背景适配 - 完善深色主题支持
- 高级动画组件 - 添加高级动画组件和视觉效果
- 关闭确认优化 - 添加取消按钮并优化关闭确认对话框
### Bug 修复
- 修复 macOS DMG 打包问题
- 修复音频处理器库加载问题
- 修复 Kotlin 字符串模板与 PowerShell 管道变量冲突
- 优化桌面端启动性能
- 优化 Windows 防火墙检测逻辑，避免界面卡顿
- 修复 C# 代码编译错误
- 避免 VBCable 安装后自动更改系统音频输出设备
- 修复 PipeWire 虚拟音频设备创建问题
- 修正 pw-loopback 命令参数格式为 JSON
- 移除 USB 模式下的 IP 输入框
### 改进
- 升级 Compose Multiplatform 至 1.10.1
- 使用 ComposeNativeTray 替换 dorkbox SystemTray（提升 Linux/macOS 托盘兼容性）
- 添加 ONNX Runtime 库和 PFFFT 库的预编译支持
- 改进原生库加载机制
- 添加 AUR 安装指南
- 多项国际化翻译更新

## [v1.1.2-20260223-0254](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.2-20260223-0254)

**Update Date:** 2026/02/23 10:54

### What's Changed
* refactor(jvm): 重构包结构，优化代码组织 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/47
* 添加繁体中文本地化 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/54
* Add support for macOS by @WhatDamon in https://github.com/LanRhyme/MicYou/pull/50
* 添加粵語本地化 by @WingChunWong in https://github.com/LanRhyme/MicYou/pull/59
* chore(i18n): 从Crowdin更新翻译 by @github-actions[bot] in https://github.com/LanRhyme/MicYou/pull/61

### New Contributors
* @WingChunWong made their first contribution in https://github.com/LanRhyme/MicYou/pull/54
* @WhatDamon made their first contribution in https://github.com/LanRhyme/MicYou/pull/50
* @github-actions[bot] made their first contribution in https://github.com/LanRhyme/MicYou/pull/61

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.1.1-20260220-0620...v1.1.2-20260223-0254

## [v1.1.1-20260220-0620](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.1-20260220-0620)

**Update Date:** 2026/02/20 14:20

### What's Changed
* chore: 添加 .gitattributes 将第三方库标记为 vendored by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/41


**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.1.0-20260216-1523...v1.1.1-20260220-0620

## [v1.1.0-20260216-1523](https://github.com/LanRhyme/MicYou/releases/tag/v1.1.0-20260216-1523)

**Update Date:** 2026/02/16 23:23

### What's Changed
* docs: 更新Readme中有关Linux与构建相关内容 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/24
* docs: 更新README中的截图与安装方式 by @xpe-online in https://github.com/LanRhyme/MicYou/pull/29
* 由于 pffft 和 ONNX Runtime 版本已稳定，不再更新 ，将其直接嵌入项目 by @a2heng in https://github.com/LanRhyme/MicYou/pull/30
* chore: 更新ulunas.onnx模型文件 by @a2heng in https://github.com/LanRhyme/MicYou/pull/31
* 修复 Linux 环境下 Tray 问题 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/32
* 从 AudioEngine.jvm.kt 中剥离实现 ADB 工具的代码为独立文件 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/34
* 异步执行防火墙检查 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/36
* 修复 Linux 环境下缺少二进制包的图标路径导致托盘图标不显示的问题 by @raindropQWQ in https://github.com/LanRhyme/MicYou/pull/33

### New Contributors
* @xpe-online made their first contribution in https://github.com/LanRhyme/MicYou/pull/29
* @raindropQWQ made their first contribution in https://github.com/LanRhyme/MicYou/pull/33

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.6hotfix-20260213-1447...v1.1.0-20260216-1523

## [v1.0.6hotfix-20260213-1447](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.6hotfix-20260213-1447)

**Update Date:** 2026/02/13 22:47

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.6-20260213-1209...v1.0.6hotfix-20260213-1447

## [v1.0.6-20260213-1209](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.6-20260213-1209)

**Update Date:** 2026/02/13 20:09

### What's Changed
* feat(platform): 增加Linux系统支持 by @ChinsaaWei in https://github.com/LanRhyme/MicYou/pull/13

### New Contributors
* @ChinsaaWei made their first contribution in https://github.com/LanRhyme/MicYou/pull/13

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.5-20260213-0639...v1.0.6-20260213-1209

## [v1.0.5-20260213-0639](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.5-20260213-0639)

**Update Date:** 2026/02/13 14:39

### What's Changed
* docs: 添加FAQ文档，包含连接设备的常见问题及解决方案 by @Hakuin123 in https://github.com/LanRhyme/MicYou/pull/18

### New Contributors
* @Hakuin123 made their first contribution in https://github.com/LanRhyme/MicYou/pull/18

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.4-20260212-0803...v1.0.5-20260213-0639

## [v1.0.4-20260212-0803](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.4-20260212-0803)

**Update Date:** 2026/02/12 16:03

### What's Changed
* feat: 添加ONNX音频处理支持并实现ulunas模型降噪 by @a2heng in https://github.com/LanRhyme/MicYou/pull/10

### New Contributors
* @a2heng made their first contribution in https://github.com/LanRhyme/MicYou/pull/10

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.3-20260211-1741...v1.0.4-20260212-0803

## [v1.0.3-20260211-1741](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.3-20260211-1741)

**Update Date:** 2026/02/12 01:41

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.2-20260211-0649...v1.0.3-20260211-1741

## [v1.0.2-20260211-0649](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.2-20260211-0649)

**Update Date:** 2026/02/11 14:49

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.1-20260211-0436...v1.0.2-20260211-0649

## [v1.0.1-20260211-0436](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.1-20260211-0436)

**Update Date:** 2026/02/11 12:37

**Full Changelog**: https://github.com/LanRhyme/MicYou/compare/v1.0.0-20260211-0143...v1.0.1-20260211-0436

## [v1.0.0-20260211-0143](https://github.com/LanRhyme/MicYou/releases/tag/v1.0.0-20260211-0143)

**Update Date:** 2026/02/11 09:43

**Full Changelog**: https://github.com/LanRhyme/MicYou/commits/v1.0.0-20260211-0143
