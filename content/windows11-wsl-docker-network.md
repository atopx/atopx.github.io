+++
title = "解决 Windows 11 无法访问 WSL2 内 Docker 服务的问题"
description = "解决 Windows 11 无法访问 WSL2 内 Docker 服务的问题"
date = 2024-08-10
draft = false

[taxonomies]
tags = ["Windows","WSL","Docker"]
[extra]
keywords = "Code, Code Blocks, Syntax, Syntax Highlighting, Theme"
toc = true
series = "Windows"
+++

在 WSL 2 中运行 Docker 时，默认情况下，Docker 会使用 `docker0` 桥接网络来管理容器的网络连接。

然而，Windows 11 的 WSL 镜像模式（mirrored mode）并不会将WSL中docker0的桥接网络映射到 Windows 系统中，从而导致从 Windows 主机访问 WSL没有问题，访问wsl中docker服务却出现问题。

<!-- more -->
## 解决方案

### 1. 将 WSL 设置为镜像模式

首先，需要将 WSL 设置为镜像模式。在 Windows 中编辑 `$HOME/.wslconfig` 文件，添加或修改以下配置：

```ini
[wsl2]
networkingMode=mirrored
firewall=false
dnsTunneling=true

[experimental]
sparseVhd=true
hostAddressLoopback=true
```

这些设置将使 WSL 2 使用镜像模式，并禁用 WSL 的防火墙，同时开启 DNS 隧道。

### 2. 关闭 WSL 中 Docker 的 iptables

接下来，需要在 WSL 中关闭 Docker 的 iptables 功能。编辑 WSL 中的 /etc/docker/daemon.json 文件，添加或修改以下配置：

```json
{
  "iptables": false
}
```
此设置将禁用 Docker 对 iptables 的修改，以防止其影响网络连接。


### 3. 在 Windows 开放对 WSL 的防火墙

为了确保 Windows 主机可以访问 WSL 中的 Docker 容器，需要在 Windows 中开放 WSL 的防火墙。打开 PowerShell，以管理员身份运行以下命令：

```powershell
New-NetFirewallRule -DisplayName "WSL" -Direction Inbound -InterfaceAlias "vEthernet (Default Switch)" -Action Allow
```
此命令将允许来自 WSL 网络接口的入站流量，从而确保 Windows 主机能够正常访问 Docker 容器服务。


### 4. 重启 WSL

完成以上所有配置后，重启 WSL 以使设置生效。在 PowerShell 中运行以下命令：

```powershell
wsl --shutdown
```
