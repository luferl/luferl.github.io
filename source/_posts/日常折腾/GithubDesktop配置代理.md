---
title: Github Desktop配置代理
date: 2021-04-09 12:08:58
tags: [日常折腾]
categories: 日常折腾
---
随手记一下，省的以后还要到处找

打开`C:\users\username\.gitconfig`文件，最后加上
```conf
[http]
    proxy = socks5://127.0.0.1:1080
[https]
    proxy = socks5://127.0.0.1:1080
[git]
    proxy = socks5://127.0.0.1:1080
```