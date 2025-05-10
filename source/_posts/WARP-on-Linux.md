---
title: WARP on Linux
date: 2025-04-06 13:30:42
tags:
        - WARP
        - 分流
        - 代理
categories:
        - WARP
        - 代理
        - Proxy
        - Linux

---

本章我们提供WARP-cli官方linux程序的功能解析以及各种命令的使用规范，主要目的为：完全学习warp-cli在使用上的所有潜在功能与应用。

注意：WARP有很多版本，例如warp-go、warp-wireguad、wgcf-warp之类的魔改版，本文只介绍warp-cli官方版本的使用内容。
**特别注意**：本章的主要内容围绕xray面板节点搭建中【warp解锁流媒体】中使用warp进行二级代理（路由）技术，此部分为辅助技术。

---

**STEP1 WARP-cli的安装**
warp-cli的安装非常繁琐，中间可能会遇到ssh守护进程被杀只能从VNC控制台登录调起的现象，  
**请做好心理准备，在ssh失效时即刻联想到通过VNC登录重新调起ssh服务的解决方法，不要慌张**

具体安装流程参考文章：
(因我参考的文章已经记不清是哪个，所以请您自行寻找，下面我将会给出几个质量还行但我没尝试过的链接。注意：官方安装教程不可行，因为在安装中需要添加一个GPG签名密钥之类的东西，所以建议寻找已经写好的脚本来辅助安装！！！)

- [参考脚本-github](https://github.com/P3TERX/warp.sh)
- [cloudfalre官方文档](https://blog.cloudflare.com/zh-cn/announcing-warp-for-linux-and-proxy-mode/)
- [签名密钥教程](https://jeam.org/40352f0)

---

**STEP2 基本命令**

- `warp-cli`  列出warp的命令列表类似于--help命令
- `warp-cli register`或`warp-cli registration new` 注册warp账户，可多次注册使用（前面不行的话使用后面的命令即可）
- `warp-cli connect` 连接到warp网络
- `warp-cli disconnect` 断开warp的网络连接
- `curl https://www.cloudflare.com/cdn-cgi/trace/`  检查连接后分配的IP地址
- `warp-cli set-licence <your key>`  设定warp的key，可以从telegram机器人获取
- `warp-cli set-mode proxy` 设置模式为proxy，默认开启40000端口的socks服务（系统内开启端口，不需要在防火墙放行）
- `warp-cli status` 查看warp服务的状态和分配的IP
- `warp-cli set-proxy-port <port>`  自定义端口号
- `curl -4 ip.gs -x socks5://127.0.0.1:40000`  查看分配到的ipv4地址

---

在使用中选择命令即可，以下为开启socks端口的流程

**注册**

```
warp-cli registration new
```

**连接**

```
warp-cli connect
```

**设置proxy模式**

```
warp-cli set-mode proxy
```

**打印分配到的IP**

```
curl -4 ip.gs -x socks5://127.0.0.1:40000
```

**查看warp状态及IP**

```
warp-cli status
```

设置后即可使用socks模式连接到warp服务了

---


`warp-cli set-mode`参数解读：


`warp`
此模式會連接到遠端伺服器，並使用 TUN 進行全域代理。這表示所有網路流量都會透過 WARP 傳輸。



`doh`
此模式僅啟用 DNS over HTTPS (DoH) 功能，用於加密 DNS 查詢。



`warp+doh`
此模式同時啟用 WARP 和 DoH 功能，結合兩者的優勢。



`dot`
此模式僅啟用 DNS over TLS (DoT) 功能，同樣用於加密 DNS 查詢。



`warp+dot`
此模式同時啟用 WARP 和 DoT 功能。



`proxy`
此模式會連接到遠端伺服器，並在本地開啟代理連接埠，允許您透過代理伺服器傳輸特定應用程式的流量


请根据个人需求选择合适的参数，x-ui面板解锁Netflix建议使用proxy模式