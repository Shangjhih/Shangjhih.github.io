---
title: Xray-CDN节点
date: 2025-04-13 17:44:00
tags:
    - Xray
    - 面板
    - CDN
    - 优选IP
categories:
    - Xray
    - 面板
    - CDN
    - 优选IP
---
<p style="font-size:40px; text-align:center; font-weight:bold"> X-ray CDN节点配置</p>

---





## what is CDN

**谈到CDN节点，就不得不提到CDN服务了，什么是CDN？**


<p style=
"line-height: 2;
font-size:20px;
text-indent:2em"
>
​	  CDN (content delivery netwok) 内容分发网络，这是一种缓存技术，CDN的供应商会在全球各地购买并部署自己的CDN服务器，这些服务器会以付费或免费的形式供开发者使用。使用该服务的开发者可以通过CDN服务器来缓存自己网站或者服务的数据，世界各地的CDN服务器都会复制一份(可以的话)，假如你开启了CDN服务，在各地的用户访问你的网页或服务时，CDN厂家会将用户的请求转发到距离用户最近的CDN服务器。
</p>


> 假设我们在新加坡的服务器部署了一个网站，一个欧洲的用户在欧洲访问你的网站，他将会向你的域名发送请求，CDN在解析请求后会将他的请求转发至位于欧洲或者距离他最近的CDN服务器，该服务器缓存了你的网页数据，他访问该CDN服务器所获取的内容和访问你的新加坡服务器是一样的，但是这次访问会更快，因为它的物理距离和用户更近。这就起到了加速服务。

---

![绘图1.png](https://s2.loli.net/2025/04/13/LriuZXwVNxU5DAb.png)

```markdown
   │
   ├─ ① 查询本地缓存（浏览器/操作系统） → 命中则直接访问
   │
   └─ ② 未命中 → 向本地DNS服务器（递归DNS）发起查询
               │
               ├─ ③ 递归DNS查询权威DNS
               │    │
               │    ├─ a.com的权威DNS返回CNAME（指向CDN别名，如a.com.cdn.com）
               │    │
               │    └─ CDN的权威DNS通过GSLB调度，返回最优边缘节点IP
               │
               └─ ④ 递归DNS将边缘节点IP返回给用户
                   │
                   ├─ ⑤ 用户与边缘节点建立TCP/TLS连接
                   │    │
                   │    ├─ ⑥ 请求资源 → 检查CDN缓存
                   │    │    │
                   │    │    ├─ 缓存命中 → 直接返回资源（HTTP 200）
                   │    │    │
                   │    │    └─ 缓存未命中 → 回源站拉取资源 → 缓存 → 返回用户
                   │    │
                   │    └─ ⑦ 动态内容可能直接透传至源站
                   │
                   └─ ⑧ 用户接收数据，完成访问
```


## How to use

<p style=
"line-height: 2;
font-size:20px;
text-indent:2em"
>
​	首先，你需要挑选一家提供CDN服务的厂家。推荐Cloudflare。你可以使用Cloudflare的DNS解析来处理自己的域名，为自己的域名开启**小黄云** ，小黄云代表你的域名已经加入到CDN的处理范围。可使用全球CDN节点。
</p>


### Cloudflare

我们以Cloudflare作为CDN供应商来自做示例：

- 域名托管
- 添加CNAME解析
- 开启CDN

#### 1.域名托管



​	首先，注册并登入Cloudflare。在首页添加域名，等待扫描DNS记录，当扫描到你的DNS记录未指向Cloudflare时，它将会提示你去修改DNS记录，提供的有两条记录，请到你的域名提供商修改**NAME SERVER**为提供的记录地址。

![e.png](https://s2.loli.net/2025/04/13/zCFNMBUuWiSVrpe.png)

#### 2.添加CNAME解析

​	等待域名初始化成功后进入你新添加的域名的管理界面，在左侧的功能栏里你将会看到一个名为**【DNS】**的选项，进入然后点击**【记录】**，在页面可以看到**【添加记录】**按钮，点击添加记录：

> 添加记录类型为A记录，解析一级域名直接在名称部分填入**@** ，解析二级域名请添加你的二级域名内容，在IPv4栏内填入你的VPS地址。**且Proxy状态要关闭！！！**

![image.png](https://s2.loli.net/2025/04/13/o216zq7NCxRHXZh.png)

<p style="color:red;font-weight:bold">☢ \ \  注意此处的 Proxy状态 ,必须关闭小黄云！！！</p>

---

## 获取SSL证书

<p style=
"line-height: 2;
font-size:20px;
text-indent:2em"
>
在你的节点面板申请SSL证书，一般都是使用Acme脚本获取，在验证的时候需要使用cloudfalre账号，也就是账号的邮箱。来申请证书
</p>


```shell
│────────────────────────────────────────────────│
│   6. Reset Username & Password & Secret Token  │
│   7. Reset Web Base Path                       │
│   8. Reset Settings                            │
│   9. Change Port                               │
│  10. View Current Settings                     │
│────────────────────────────────────────────────│
│  11. Start                                     │
│  12. Stop                                      │
│  13. Restart                                   │
│  14. Check Status                              │
│  15. Logs Management                           │
│────────────────────────────────────────────────│
│  16. Enable Autostart                          │
│  17. Disable Autostart                         │
│────────────────────────────────────────────────│
│  18. SSL Certificate Management                │
│  19. Cloudflare SSL Certificate                │
│  20. IP Limit Management                       │
│  21. Firewall Management                       │
│  22. SSH Port Forwarding Management            │
│────────────────────────────────────────────────│
│  23. Enable BBR                                │
│  24. Update Geo Files                          │
│  25. Speedtest by Ookla                        │
╚────────────────────────────────────────────────╝

Please enter your selection [0-25]: 19
[INF] ****** Instructions for Use ****** 
[INF] Follow the steps below to complete the process: 
[INF] 1. Cloudflare Registered E-mail. 
[INF] 2. Cloudflare Global API Key. 
[INF] 3. The Domain Name. 
[INF] 4. Once the certificate is issued, you will be prompted to set the certificate for the panel (optional). 
[INF] 5. The script also supports automatic renewal of the SSL certificate after installation. 

Do you confirm the information and wish to proceed? [y/n] [Default y]: 
```

<p style="color:red;font-weight:bold">☢\\  注意此时的80端口不要运行任何服务，有服务的话请手动停止，必须保证该端口无任何服务占用，不然申请证书会失败！！！</p>

```shell
[INF] Follow the steps below to complete the process: 
[INF] 1. Cloudflare Registered E-mail. 
[INF] 2. Cloudflare Global API Key. 
[INF] 3. The Domain Name. 
```

提示列出了你需要准备的信息。

**Cloudflare Global API Key**可以在Cloudflare的账户设置中找到


![image.png](https://s2.loli.net/2025/04/13/ILkagMJA8ScyrEd.png)

<p style="color:red;font-weight:bold"> ☢\\   点击查看后会给你列出Key，马上复制下来备用，此Key只会出现一次，找不到了需要再次请求。</p>
随后根据提示的内容输入关键信息，然后等待脚本运行结果，证书申请后会将总要信息打印到控制台，请记住证书的保存位置，建议使用cp命令将证书复制一份到别的地方，以防丢失。




<p style="color:red;font-weight:bold">☢\\    证书申请后可以到Cloudflare域名设置中开启小黄云，等待CDN扩散至全部的CDN服务器。</p>



![](https://s2.loli.net/2025/04/13/RIwW9g7mc1SNqJT.png)


---

<p style="color:red;font-weight:bold">在以上所有步骤都完成后即可开启80端口运行的服务</p>

---

## 添加CDN节点

1.在面板的**【面板设置】** 中的**【证书】** 添加私钥和公钥的绝对路径

- `fullchain.pem`  ---------**公钥**

- `privkey.pem ` ------------**私钥**



2.在面板的**【入站列表】** 中新建一个80端口的VLESS节点，使用`websocket`协议，

- 主机地址-------------------------域名
- 路径----------------------------随意，但是要`/` 开头(例如   /userame)



3.sniffing开启



4. 安全   `无`





---

## 修改CDN配置

#### 1.导出节点

​	在面板中配置好Vless协议的基础节点后，以二维码的形式到入至V2ray，此后进行配置文件的修改。

#### 2.修改配置

![image.png](https://s2.loli.net/2025/04/13/oligHTDS4Q1vZFI.png)

按图示进行修改，测速，有数值即代表可以连通。



---

## 优选IP



可以使用Github开源工具或者网站进行筛选并替换



- [Github工具](https://github.com/XIU2/CloudflareSpeedTest)



- [在线优选](https://cf.vvhan.com/)



---

<p style="
          font-size:30px;
          fot-weight:bold;
          text-align:center;
          color:red
          "> 👍恭喜您学会了一个新知识<br>
                   GOOD JOB
</p>

