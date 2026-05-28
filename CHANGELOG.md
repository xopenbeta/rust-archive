# Changelog

## v1.1 (2026-05-29) - 精简版本矩阵，支持最新 Rust

### 变更

- 保留以下 5 个版本:
  - **1.75.0**（1.7x latest）
  - **1.85.0**、**1.86.0**（保留）
  - **1.89.0**（1.8x latest）
  - **1.96.0**（1.9x latest / 当前最新 stable）
- 构建矩阵: 5 个 Rust 版本 × 5 个平台 = **25 个构建任务**

---

## v1.0 (2026-04-27) - 初始配置

### 新增

- 支持 Rust 版本: 1.70.0, 1.75.0, 1.80.0, 1.85.0, 1.86.0
- 支持平台:
  - macOS x64 (x86_64-apple-darwin) — 在 Apple Silicon 上编译
  - macOS aarch64 (aarch64-apple-darwin) — Apple Silicon 原生支持
  - Linux x64 (x86_64-unknown-linux-gnu)
  - Linux aarch64 (aarch64-unknown-linux-gnu)
  - Windows x64 (x86_64-pc-windows-msvc)
  - Windows aarch64 (aarch64-pc-windows-msvc) — 暂时注释，等待 GitHub Actions 公共 runner
- 包含组件: rustc, cargo, std, clippy, rustfmt
- 自动生成 SHA256 校验和
- 通过 Git tag 触发构建（`v*` 或 `release-*`）
- 自动创建 GitHub Release
- 构建矩阵: 5 个 Rust 版本 × 5 个平台 = 25 个构建任务
