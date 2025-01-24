+++
title = "windows 配置go grpc环境"
description = "windows 配置go grpc环境"
date = 2025-01-25
draft = false

[taxonomies]
tags = ["windows","go", "grpc"]
[extra]
keywords = "Windows, Go, Golang, Grpc"
toc = true
series = "go"
+++

windows 配置go grpc环境
<!-- more -->

# windows 配置go grpc环境

1. 安装 libprotoc, 配置环境变量

   1) 下载地址: [https://github.com/protocolbuffers/protobuf/releases/tag/v29.3](https://github.com/protocolbuffers/protobuf/releases/tag/v29.3)

   2. 把bin路径加入PATH环境变量

2. 安装 gen code 插件

```
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest 
```
