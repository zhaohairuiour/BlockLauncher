# BLOCK LAUNCHER

**方块启动器 · Minecraft Java + Bedrock，装进一台 Android 设备。**

[![最新版本](https://img.shields.io/badge/version-1.5.16-4AEDD9?style=flat-square&labelColor=0B0C0D)](https://github.com/zhaohairuiour/BlockLauncher/releases/latest)
[![Android](https://img.shields.io/badge/Android-8.0%2B-4AEDD9?style=flat-square&labelColor=0B0C0D)](https://github.com/zhaohairuiour/BlockLauncher/releases/latest)
[![arm64-v8a](https://img.shields.io/badge/ABI-arm64--v8a-4AEDD9?style=flat-square&labelColor=0B0C0D)](https://github.com/zhaohairuiour/BlockLauncher/releases/latest)

[下载最新 APK](https://github.com/zhaohairuiour/BlockLauncher/releases/latest) · [产品介绍页](https://zhaohairuiour.github.io/BlockLauncher/) · [全部版本](https://github.com/zhaohairuiour/BlockLauncher/releases)

![BlockLauncher](docs/assets/og.png)

## 这是什么

BlockLauncher 是一个原生 Android 启动器，使用 Kotlin + Jetpack Compose 构建。界面采用 Minecraft 像素风格：硬边面板、抖动阴影、青色强调色和官方像素字体。

它把 Java 版启动链和 Bedrock 客户端入口放进同一个应用：从账号、版本清单、加载器安装，到 JRE、触控布局和游戏内 HUD，都在本地完成。

## 功能

- Java 版与 Bedrock 版入口
- 微软正版登录 / 离线账号
- Mojang、BMCLAPI 版本清单
- 版本继承链与版本隔离
- 并发下载、断点续传
- Fabric / Quilt / Forge / NeoForge 安装器
- Modrinth / MC百科内容检索
- 模组、光影、资源包、整合包下载
- Java 8 / 17 / 21 运行时管理，缺失 Java 21 时自动获取
- Pojav / Amethyst 运行层、GL4ES、OpenAL
- FCL 风格触控布局编辑器与自定义 HUD
- JVM 日志落盘、上次会话恢复、退出码记录

## 下载

| 项目 | 值 |
| --- | --- |
| 最新版本 | **1.5.16** |
| 发布日期 | 2026-11-22 |
| 包名 | `com.blocklauncher.app` |
| 架构 | `arm64-v8a` |
| 最低系统 | Android 8.0 / API 26 |
| 安装包 | 约 17 MB |
| 签名 | 固定证书，可直接覆盖安装 |

前往 [Releases](https://github.com/zhaohairuiour/BlockLauncher/releases/latest) 下载 APK。

```text
SHA-256 (BlockLauncher-1.5.16.apk)
e2b6199edcd66b8f253c8a1182b561aaa21f6f119898ec843e9d17d6ea4a6124
```

## 安装

1. 下载 `arm64-v8a` APK。
2. 允许浏览器或文件管理器安装未知来源应用。
3. 使用微软账号登录，或创建离线账号。
4. 在版本库选择游戏版本；需要时安装 Fabric / Forge 等加载器。
5. 首次启动会准备 Java 运行层，随后进入游戏。

更新版本使用同一签名证书，直接覆盖安装即可，账号、版本与存档会保留。

## 当前版本状态

`1.5.16` 修复 JNA 与 LWJGL 原生库版本冲突：

- **JNA**：用 `jna-5.17.0.aar` 的 Android arm64 `libjnidispatch.so`（7.0.4）替换 APK 原带的 6.1.6 版本；启动参数保留 `-Djna.nosys=true`。OSHI 不再报 `Expected: 7.0.4 / Found: 6.1.6`。
- **LWJGL**：新增 `PojavNatives` 接管名单；安装、自动补全和启动前清理版本 natives 目录中的官方 Linux 版 `liblwjgl*.so`、`libopenal.so`、`libfreetype.so`、`libglfw.so`、`libjnidispatch.so`，只使用 Pojav 运行层的 Android 版。
- 保留 1.5.14 的启动前自动补全、1.5.13 的 `lib/server` 首段 `LD_LIBRARY_PATH` 修复和 1.5.12 的 JRE 执行位/触控编辑器修复。

已知问题：1.5.16 尚未在真实 Android 设备上验证 1.21.11 能否进入主界面。如果仍以退出码 6 结束，请把最新 `pojav-1.21.11.log` 发到 Issue。日志目录：

```text
Android/data/com.blocklauncher.app/files/BlockLauncher/logs/
```

## 产品介绍页

GitHub Pages 站点位于：

**https://zhaohairuiour.github.io/BlockLauncher/**

站点与 App 共用同一套视觉资产：`minecraft_pixel.ttf`、草方块图标和 Overworld 配色。页面包含滚动入场动画、顶部滚动进度条、1.21.11 模拟安装动画和免责声明；源码在 `docs/`。

## 仓库结构

```text
.
├── docs/                  # GitHub Pages 站点
│   ├── index.html
│   └── assets/
│       ├── site.css
│       ├── minecraft-pixel.ttf
│       ├── icon.svg
│       └── og.png
├── README.md
└── .gitignore
```

## 反馈

- Bug 与启动日志：[Issues](https://github.com/zhaohairuiour/BlockLauncher/issues)
- 版本记录：[Releases](https://github.com/zhaohairuiour/BlockLauncher/releases)

提交启动问题时，请附上设备型号、Android 版本、游戏版本、加载器和 `logs/` 目录中的最近日志。

## 说明

本项目目前以闭源方式发布，仓库只包含发布产物与介绍页，不包含完整 App 源码。

BlockLauncher 不是 Mojang Studios 或 Microsoft 的官方产品。Minecraft 是 Mojang Studios 的商标。
