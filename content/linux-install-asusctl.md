+++
title = "Liunx 安装 ROG Asus 控制台"
description = "ROG Asusctl是一个使用rust编写的linux平台的开源项目，为linux用户提供华硕/ROG设备控制器"
date = 2022-05-16
draft = false

[taxonomies]
tags = ["Linux","ROG"]
[extra]
keywords = "Code, Code Blocks, Syntax, Syntax Highlighting, Theme"
toc = true
series = "Linux"
+++

ROG Asusctl是一个使用rust编写的linux平台的开源项目，为linux用户提供华硕/ROG设备控制器
<!-- more -->
## Code Blocks


## 基础环境

### 适用系统：

- linux mint 21
- ubuntu 22.04
	
### 安装版本：

- asusctl-5.0.10
- rust 1.77.2

## 构建

1. 安装编译环境

```bash
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install -y \
    libasound2-dev \
    libfreetype6-dev \
    libexpat1-dev \
    libxcb-composite0-dev \
    libssl-dev \
    libx11-dev \
    cmake \
    build-essential \
    libclang-dev \
    libclang-dev \
    libfontconfig-dev \
    pkg-config \
    libgdk-pixbuf2.0-0 \
    libpangomm-1.4-dev \
    libgtk-3-dev \
	libgtk-4-dev \
	libudev-dev \
	libsystemd-dev \
	libseat-dev \
    libinput-dev \
    libgbm-dev
```

2. 下载源码

```bash
wget https://gitlab.com/asus-linux/asusctl/-/archive/5.0.10/asusctl-5.0.10.tar.gz
tar -zxvf asusctl-5.0.10.tar.gz
```

3. 编译
```bash
cargo build --release
make && make install
```

4. 启动服务
> 详细用法请自行查阅文档
```bash
sudo systemctl status asusd.service
```
