+++
title = "Windows Rust error: failed to run custom build command for `openssl-sys v0.9.104`"
description = "windows rust build error: failed to run custom build command for `openssl-sys v0.9.104`\nwindows vcpkg install openssl"
date = 2025-01-23
draft = false

[taxonomies]
tags = ["windows","vcpkg", "openssl", "rust"]
[extra]
keywords = "Windows, vcpkg, Rust, Openssl"
toc = true
series = "rust"
+++

windows rust build error: failed to run custom build command for `openssl-sys v0.9.104`\nwindows vcpkg install openssl
<!-- more -->

## 下载vcpkg

```
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
./bootstrap-vcpkg.bat
```

## 运行安装

```
.\vcpkg.exe install openssl:x64-windows
.\vcpkg.exe install openssl:x64-windows-static
.\vcpkg.exe integrate install
```

## 配置环境变量

#### 动态链接库

| 变量名              | 变量值                                            |
| ------------------- | ------------------------------------------------- |
| OPENSSL_DIR         | D:\lib\vcpkg\packages\openssl_x64-windows         |
| OPENSSL_INCLUDE_DIR | D:\lib\vcpkg\packages\openssl_x64-windows\include |
| OPENSSL_LIB_DIR     | D:\lib\vcpkg\packages\openssl_x64-windows\lib     |

#### 静态链接

| 变量名                                     | 变量值                                                   |
| ------------------------------------------ | -------------------------------------------------------- |
| X86_64_PC_WINDOWS_MSVC_OPENSSL_DIR         | D:\lib\vcpkg\packages\openssl_x64-windows-static         |
| X86_64_PC_WINDOWS_MSVC_OPENSSL_INCLUDE_DIR | D:\lib\vcpkg\packages\openssl_x64-windows-static\include |
| X86_64_PC_WINDOWS_MSVC_OPENSSL_LIB_DIR     | D:\lib\vcpkg\packages\openssl_x64-windows-static\lib     |

