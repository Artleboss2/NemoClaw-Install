# 如何安装 NVIDIA NemoClaw：分步指南

NemoClaw 是 NVIDIA 提供的一个开源堆栈，旨在通过添加隐私控制、沙盒（sandboxing）和安全护栏来安全地运行 OpenClaw AI 代理。

请遵循以下简单步骤来设置和运行您的安全 AI 代理。

## 先决条件

在开始之前，请确保您的系统满足以下要求：

* **操作系统：** Linux（推荐使用 Ubuntu 22.04+）。支持 macOS 和 Windows（通过 WSL2），但处于实验阶段。
* **硬件：** 至少 8 GB 内存（强烈推荐 16 GB）和大约 40 GB 的可用磁盘空间。
* **API 密钥：** NVIDIA API 密钥（您可以在 `build.nvidia.com` 免费获取）。

## 第 1 步：准备您的系统

NemoClaw 需要安装 Docker 和 Node.js（版本 20 或 22）才能正常运行。

### 1. 验证 Docker：

确保已安装 Docker，并且您拥有适当的权限，而无需每次都使用 `sudo`：

```bash
docker ps
```

（如果您收到“permission denied”权限拒绝错误，请运行 `sudo usermod -aG docker $USER`，然后注销并重新登录）。

### 2. 安装 Node.js：

运行以下命令来安装 Node.js（版本 22）：

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

通过运行 `node --version` 来验证安装。

## 第 2 步：安装 NemoClaw

NVIDIA 提供了一个简单的安装脚本来处理繁重的工作。

在您的终端中运行以下命令：

```bash
curl -fsSL https://nvidia.com/nemoclaw.sh | bash
```

注意：根据您的系统配置，如果遇到权限错误，您可能需要使用 `sudo bash` 来运行它。

## 第 3 步：配置您的代理 (Onboarding)

安装完成后，您需要配置您的沙盒 (sandbox) 和推理 (inference) 设置。

运行配置向导：

```bash
nemoclaw onboard
```

在这个交互过程中：

* 为您的助手命名（例如，`my-assistant`）。
* 在提示时输入您的 NVIDIA API 密钥。
* 接受安全策略和沙盒设置的默认配置。

注意：该脚本将下载沙盒镜像（约 2.4 GB）。这可能需要几分钟的时间。

## 第 4 步：连接并聊天！

您的安全环境现在已准备就绪。是时候连接到您隔离的代理了。

### 1. 连接到沙盒：

将 `my-assistant` 替换为您在第 3 步中选择的名称。

```bash
nemoclaw my-assistant connect
```

### 2. 启动聊天界面：

进入隔离的沙盒后，启动 OpenClaw 文本用户界面 (TUI)：

```bash
openclaw tui
```

恭喜！您现在可以安全地输入消息并与隔离的 AI 代理进行交互了。

## Советы по устранению неполадок

* **Ошибки нехватки памяти (OOM):** Если установка прерывается на машине с 8 ГБ оперативной памяти, попробуйте добавить файл подкачки (swap space) в вашу систему.
* **Пользователи WSL2:** Если вы используете подсистему Windows для Linux и сталкиваетесь с проблемами проброса GPU (GPU passthrough) во время `nemoclaw onboard`, вам может потребоваться запустить шлюз OpenShell вручную без флага `--gpu`.
