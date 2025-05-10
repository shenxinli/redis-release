# Redis 多平台二进制发布工具

本项目是一个基于 GitHub Actions 的自动化工作流，用于下载、编译 Redis 源码并发布针对不同平台和架构的预编译二进制文件。支持 Linux (amd64/arm64) 和 Windows (x64) 平台，能够自动生成格式如 `redis-7-linux-amd64.tar.gz` 的发布包。

## 功能特点

- 支持 Redis 5、6、7 三个版本
- 支持 Linux (amd64/arm64) 和 Windows (x64) 平台
- 可选择编译特定版本和平台组合
- 自动生成规范命名的发布包
- 一键触发的 GitHub Actions 工作流
- 完整的错误处理和日志记录

## 支持的平台和架构

- Linux: amd64, arm64
- Windows: x64

## 使用方法

### 触发工作流

1. 在 GitHub 仓库中导航到 "Actions" 选项卡
2. 选择 "Redis Release" 工作流
3. 点击 "Run workflow" 按钮
4. 从下拉菜单中选择需要编译的 Redis 版本
5. 输入需要编译的平台（逗号分隔，如 `linux/amd64,windows/x64`）
6. 输入发布标签
7. 点击 "Run workflow" 确认

### 可用平台参数

- `linux/amd64` - Linux AMD64 平台
- `linux/arm64` - Linux ARM64 平台
- `windows/x64` - Windows x64 平台

### 获取发布包

工作流完成后，会在仓库的 "Releases" 页面创建一个新的发布版本，其中包含所有编译好的二进制包。

## 工作原理

工作流通过以下步骤完成 Redis 的编译和发布：

1. **下载源码**：从 Redis 官方下载指定版本的源码
2. **环境准备**：安装编译所需的依赖工具
3. **交叉编译**：
   - Linux amd64: 在 Ubuntu 环境下直接编译
   - Linux arm64: 使用 QEMU 模拟 ARM 环境进行交叉编译
   - Windows x64: 下载预编译的二进制包
4. **打包**：将编译好的二进制文件打包成规范格式
5. **发布**：创建 GitHub Release 并上传所有打包文件

## 自定义配置

如果你需要修改工作流配置，可以编辑 `.github/workflows/redis-release.yml` 文件：

- 修改支持的 Redis 版本：调整 `redis_version` 的选项列表
- 添加/删除平台：修改 `matrix.include` 配置
- 调整编译参数：修改 `make` 命令的参数

## 注意事项

- Windows 版本使用第三方预编译包，而非从源码编译
- 编译过程可能需要较长时间，尤其是 ARM64 架构
- 如需添加更多平台支持，可能需要额外配置 QEMU 环境

## 贡献

欢迎提交 Issue 或 Pull Request 来改进这个工作流！
  