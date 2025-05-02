+++
title = "利用OpenDNS获取公网IP"
description = "通过OpenDNS获取当前网络环境的公网IP"
date = 2025-05-02
draft = false

[taxonomies]
tags = ["rust","network"]
[extra]
keywords = "Code, Code Blocks, Syntax, Syntax Highlighting, Theme"
toc = true
series = "Linux"
+++

使用DNS获取公网IP的优势：

- 稳定
- 高效
- 通用
- 安全

依赖环境:

```toml
[dependencies]
hickory-proto = "0.25"
hickory-resolver = "0.25"
tokio = { version = "1", features = ["macros"] }
```

功能代码:

```rust
use std::net::{Ipv4Addr, SocketAddr, SocketAddrV4};

use hickory_proto::xfer::Protocol;
use hickory_resolver::{
    config::{NameServerConfig, ResolverConfig},
    name_server::TokioConnectionProvider,
    ResolveError, ResolveErrorKind, Resolver,
};

const OPENDNS_ADDR: SocketAddr =
    SocketAddr::V4(SocketAddrV4::new(Ipv4Addr::new(208, 67, 222, 222), 53));
const OPENDNS_DOMAIN: &str = "myip.opendns.com";

async fn public_ip() -> Result<String, ResolveError> {
    let mut config = ResolverConfig::new();
    config.add_name_server(NameServerConfig::new(OPENDNS_ADDR, Protocol::Udp));
    let resolver =
        Resolver::builder_with_config(config, TokioConnectionProvider::default()).build();
    resolver
        .lookup_ip(OPENDNS_DOMAIN)
        .await?
        .iter()
        .next()
        .map(|ip| ip.to_string())
        .ok_or_else(|| ResolveErrorKind::Message("no IP found").into())
}

#[tokio::main]
async fn main() {
    let ip = public_ip().await.unwrap();
    println!("{}", ip);
}
```
