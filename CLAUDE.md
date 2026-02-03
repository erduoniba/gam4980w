# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个基于 Astro 的 GAM-4980 游戏机模拟器网站项目。使用 Nostalgist 库和 gam4980 libretro 核心来运行 .gam 格式的游戏 ROM。

## 常用命令

```bash
# 开发服务器
bun run dev

# 构建生产版本
bun run build

# 预览构建结果
bun run preview
```

## 项目架构

### 核心组件

- **Emulator.astro** (`src/components/Emulator.astro`): 核心模拟器组件
  - 使用 Web Components (`<x-emulator>`) 封装
  - 通过 Nostalgist 库初始化 gam4980 核心
  - 在启动前加载必需的 BIOS 文件 (8.BIN, E.BIN)
  - 配置 CPU 速率、定时器速率和 LCD 颜色

### 页面结构

- **index.astro**: 首页，列出所有可用游戏（从 `public/roms` 目录读取）
- **p/[rom].astro**: 动态路由页面，为每个 ROM 文件生成独立游戏页面
  - 使用 `getStaticPaths()` 静态生成所有游戏页面

### 资源文件

- **public/cores/**: libretro 核心文件
  - `gam4980_libretro.js`
  - `gam4980_libretro.wasm`
- **public/roms/**: 游戏 ROM 文件（.gam 格式）
- **public/system/gam4980/**: BIOS 文件
  - `8.BIN`
  - `E.BIN`

## 技术栈

- Astro 5.17.1 (静态站点生成)
- Nostalgist 0.20.0 (RetroArch 模拟器封装)
- Bun (包管理器和运行时)
- gam4980 libretro 核心

## 开发注意事项

- 添加新游戏时，将 .gam 文件放入 `public/roms/` 目录
- 模拟器配置在 `Emulator.astro` 的 `retroarchCoreConfig` 中
- 站点配置为部署到 `https://iyzsong.github.io`
