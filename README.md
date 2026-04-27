# Rust Archive

自动构建和打包多版本、多平台的 Rust 工具链 (rustc, cargo, clippy, rustfmt)。

## 📦 支持的平台

### Rust 版本

| Rust 版本 | 发布时间 | 说明 |
|-----------|----------|------|
| 1.70.0 | 2023-06-01 | 稳定版 |
| 1.75.0 | 2023-12-28 | 稳定版 |
| 1.80.0 | 2024-07-25 | 稳定版 |
| 1.85.0 | 2025-02-20 | 稳定版 |
| 1.86.0 | 2025-04-03 | 稳定版 |

### 包含组件

| 组件 | 说明 |
|------|------|
| rustc | Rust 编译器 |
| cargo | 包管理器与构建工具 |
| std | Rust 标准库 |
| clippy | Lint 工具 |
| rustfmt | 代码格式化工具 |

### macOS (全部在 Apple Silicon 上编译)

- **x86_64-apple-darwin** (适用于 Intel 芯片 Mac) — 在 macos-14 上编译
- **aarch64-apple-darwin** (Apple Silicon M1/M2/M3/M4 原生支持) — 在 macos-14 上编译

> **注意**: GitHub Actions 不再提供 Intel Mac runners，所有 macOS 构建均在 Apple Silicon 上进行。
> x86_64 版本通过 rustup 指定 target triple 安装，完全支持 Intel Mac。

### Linux

- **x86_64-unknown-linux-gnu** (x64/AMD64) — ubuntu-22.04
- **aarch64-unknown-linux-gnu** (ARM64) — ubuntu-22.04-arm

### Windows

- **x86_64-pc-windows-msvc** (64位) — windows-2022
- ~~**aarch64-pc-windows-msvc** (ARM64)~~ — **暂不可用**

> **Windows ARM64 说明**: GitHub Actions 目前没有提供公共的 Windows ARM64 runner。
> 等待 GitHub 官方提供 `windows-11-arm` 公共 runner 后将启用。

## 🤖 自动构建

### 触发条件

构建会在以下情况下自动触发：

- 推送以 `v` 或 `release-` 开头的 Git tag

```bash
# 示例：创建并推送 tag
git tag v20260427
git push origin v20260427
```

### 构建矩阵

| 维度 | 数量 |
|------|------|
| Rust 版本 | 5 |
| 平台 | 5 |
| **总构建任务** | **25** |

### 归档命名规则

- Unix: `rust-{version}-{target}.tar.gz`
- Windows: `rust-{version}-{target}.zip`

示例:
- `rust-1.86.0-aarch64-apple-darwin.tar.gz`
- `rust-1.86.0-x86_64-unknown-linux-gnu.tar.gz`
- `rust-1.86.0-x86_64-pc-windows-msvc.zip`

## 📥 使用方法

### Unix (macOS / Linux)

```bash
# 1. 下载归档（以 macOS Apple Silicon 1.86.0 为例）
curl -LO https://github.com/<your-repo>/releases/latest/download/rust-1.86.0-aarch64-apple-darwin.tar.gz

# 2. 解压到目标目录
mkdir -p ~/.rust-toolchains/1.86.0-aarch64-apple-darwin
tar -xzf rust-1.86.0-aarch64-apple-darwin.tar.gz -C ~/.rust-toolchains/1.86.0-aarch64-apple-darwin

# 3. 添加到 PATH
export PATH="$HOME/.rust-toolchains/1.86.0-aarch64-apple-darwin/bin:$PATH"

# 4. 验证
rustc --version
cargo --version
```

### Windows (PowerShell)

```powershell
# 1. 下载归档
Invoke-WebRequest -Uri "https://github.com/<your-repo>/releases/latest/download/rust-1.86.0-x86_64-pc-windows-msvc.zip" -OutFile "rust-1.86.0-x86_64-pc-windows-msvc.zip"

# 2. 解压
Expand-Archive -Path "rust-1.86.0-x86_64-pc-windows-msvc.zip" -DestinationPath "$env:USERPROFILE\.rust-toolchains\1.86.0-x86_64-pc-windows-msvc"

# 3. 添加到 PATH（当前会话）
$env:PATH = "$env:USERPROFILE\.rust-toolchains\1.86.0-x86_64-pc-windows-msvc\bin;" + $env:PATH

# 4. 验证
rustc --version
cargo --version
```

## 🔐 校验和验证

每个归档都附带一个 `.sha256` 校验和文件：

```bash
# Linux
sha256sum -c rust-1.86.0-x86_64-unknown-linux-gnu.tar.gz.sha256

# macOS
shasum -a 256 -c rust-1.86.0-aarch64-apple-darwin.tar.gz.sha256

# Windows PowerShell
Get-FileHash rust-1.86.0-x86_64-pc-windows-msvc.zip -Algorithm SHA256
```

## 📄 许可证

本项目脚本采用 [MIT License](LICENSE)。

归档中包含的 Rust 工具链遵循 Rust 项目的双重许可证：
- Apache License 2.0
- MIT License

详见 [Rust 项目版权说明](https://github.com/rust-lang/rust/blob/master/COPYRIGHT)。
