---
layout: post
title: 使用 docker 封印邪神 easyconnect 与 clash parse & relay 的使用
subtitle: 深信服罪大恶极
author: RuntimeEroor
categories: config
tags: 代理 
date: 2024-01-26
---
# 1. 安装 Docker Desktop
# 2. 参照此[仓库](https://github.com/docker-easyconnect/docker-easyconnect)
1. `docker pull hagb/docker-easyconnect:latest`
2. 使用vnc客户端连接vnc，地址：127.0.0.1，端口: 5901, 密码 xxxx
# 3. 修改 clash parser项
```yaml
parsers:
- url: xxxx
    yaml:
    prepend-proxies:
        - name: easyconnect
        type: socks5
        server: 127.0.0.1
        port: 1080
        - name: amax
        type: ss
        server: xxx
        port: 2012
        cipher: aes-256-gcm
        password: xxxx
    prepend-proxy-groups:
        - name: Relay
        type: relay
        proxies:
            - easyconnect
            - amax
    prepend-rules:
        - IP-CIDR,172.16.4.12/32,Relay
```
