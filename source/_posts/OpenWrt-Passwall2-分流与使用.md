---
title: OpenWrt Passwall2 分流与使用
date: 2025-04-07 20:29:26
tags:
        - 代理
        - Proxy
        - OpenWrt
        - 软路由
        - Passwall 2
categories:
        - 代理
        - Proxy
        - OpenWrt
        - 软路由
        - Passwall 2
---
# OpenWrt Passwall2 分流与使用

###########################################################################
​    OpenWrt是一个基于Linux的嵌入式操作系统开源项目，主要用于嵌入式设备上路由网络流量，其主要工作组件包括Linux、util-linux、musl和busybox，所有的组件都得到简化，体积小、兼容性好。常用于在路由器设备上部署。因其基于arm Linux，很多x86的程序无法在上面运行，且搭载该系统的设备硬件都较差，很多都是用于跑一些个人博客或者Docker容器，比如青龙面板之类的。

​    OpenWrt像大多数linux系统一样，使用shell命令行界面操作，如今的OpenWrt系统都带有Web界面(LuCi),可轻易通过鼠标与Ui界面交互，包管理系统为opkg。操作逻辑较为简单，容易上手。OpenWrt面板有较多分支，immortalWrt、ledeWrt等都是较为常见的版本，此篇文章我们以immortalWrt作为讲解对象。

###########################################################################

### 登陆界面


![image.png](https://s2.loli.net/2025/04/07/kO6veTKZ7N2M9lX.png)

![image.png](https://s2.loli.net/2025/04/07/z1yuiCJxeQIFGrB.png)

###########################################################################
​    进入系统后可以看到左侧的菜单栏，我们常用的菜单栏为【首页】【网络向导】【服务】。首页可以查看系统的各项参数，包括Docker的状态。右侧的【IP地址】点击后可以设置设备的静态IP，当然，你也可以使用ssh命令登入后台找到etc目录下的network文件手动进行修改，此时你修改的IP就是未来你登入后台的局域网IP，该IP需要牢记，每次登陆都需要该IP。

配置文件的绝对路径为：

```
/etc/config/network
```

配置文件的内容大概如下：

###########################################################################

```yaml
config interface 'loopback'
        option device 'lo'
        option proto 'static'
        option ipaddr '127.0.0.1'
        option netmask '255.0.0.0'

config globals 'globals'
        option ula_prefix 'lfkfa:d8dhf:3ubfbc::/48'
        option packet_steering '1'

config device
        option name 'br-lan'
        option type 'bridge'
        list ports 'eth0'

config interface 'lan'
        option device 'br-lan'
        option proto 'static'
        option ip6assign '60'
        option gateway '此处为网关地址'   # 填入你的上级路由器地址
        option peerdns '0'
        list dns '223.5.5.5'
        option ipaddr '静态IP地址'        # 静态IP地址为你日后登录使用的IP
        option netmask '255.255.255.0'

config interface 'docker'
        option device 'docker0'
        option proto 'none'
        option auto '0'

config device
        option type 'bridge'
        option name 'docker0'
```

###########################################################################
仅需要修改第20行和23行的内容。

请自学`Vim`或者`Vi`以及`nano`编辑器的基础用法！！！

###########################################################################

   假定你现在使用的是[网关代理](https://baike.baidu.com/item/%E7%B6%B2%E9%97%9C%E4%BB%A3%E7%90%86/5005818)模式，你只需要在系统的【网络向导】部分将路由器设置为【连接现有路由器】，再进入你的路由器，将路由器的【网关】设为OpenWrt的IP，此时你的路由器就会作为一个信号发射器，所有的数据便交由OpenWrt设备处理。(此处无佐证，不修改也可以)

###########################################################################

## 软件源修改

​    
###########################################################################
​    因此系统使用的是opkg包管理器，其官方软件源在中国大陆访问有问题，建议手动修改为国内的镜像源，以保证软件的正常下载(不然会遇到搜索不到软件的情况)。

修改软件源路径:

<p style="font-weight:bold">【系统】-【软件包】-【配置opkg】</p>

###########################################################################
![image.png](https://s2.loli.net/2025/04/07/irUKQvXYO2f4HBx.png)

---

###########################################################################

<p style="color:red">将原有的软件源前面加上  #  ，把原有的注释掉，使其不再生效。</p>

在下面选取合适的软件源复制到后面并保存：



###########################################################################

1.中科大软件源
###########################################################################

```yaml
src/gz openwrt_core https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/targets/rockchip/armv8/packages
src/gz openwrt_base https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/base
src/gz openwrt_luci https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/luci
src/gz openwrt_packages https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/packages
src/gz openwrt_routing https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/routing
src/gz openwrt_telephony https://mirrors.ustc.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/telephony

```

###########################################################################

2.清华源

###########################################################################

```yaml
src/gz openwrt_core https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/targets/rockchip/armv8/packages
src/gz openwrt_base https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/base
src/gz openwrt_luci https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/luci
src/gz openwrt_packages https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/packages
src/gz openwrt_routing https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/routing
src/gz openwrt_telephony https://mirrors.tuna.tsinghua.edu.cn/immortalwrt/releases/21.02.0/packages/aarch64_generic/telephony

```

---

###########################################################################

此后便可以在软件下载目录中输入你想要的软件名字进行下载，此处仅提供一些参考：

###########################################################################


![image.png](https://s2.loli.net/2025/04/07/brna5DH4ICtUfwP.png)

   

  接下来我们会讲一下Passwall2的用法。代理软件中明星众多，为什么讲Passwall 2？当然是因为它以Xray为内核，完全支持自建节点（不支持新协议），它还有简单明了的Socks和HTTP代理服务了。

###########################################################################

## Passwall 2

###########################################################################

![e0ca0686ec4e01015116860f5e5c820.png](https://s2.loli.net/2025/04/07/AyndShEfIMgvTco.png)


​    在【节点列表】中有一个【新增】按钮，点进去有一个【导入分享URL】,点击进入后会弹出一个输入框，把你的节点信息复制进去，点击【确定】，再点击右下角的【保存】。然后重新点击【节点列表】，重新此步骤添加。<span style="color:red">为什么不在列表内持续添加？ 因为不支持</span>

多次添加节点后即可，不用添加太多，几个就够了。

###########################################################################

### 分流节点

###########################################################################

​    在【节点列表】内，你将会看到一个【分流总节点】，点击右侧的编辑，编辑设置，按下图所示，需要修改【proxy】和【默认】的节点为你添加的节点，其它的内容都要和图示内容对上，假如你没有部分规则也不要紧，只要显示的规则跟图示对上就可以，该直连的直连，该黑洞的黑洞（封锁）。

###########################################################################




![image.png](https://s2.loli.net/2025/04/07/PcqCihaD8gYJ1pG.png)




---

  

 ###########################################################################

随后在Passwall 2的主页选则【总分流节点】作为你的节点即可。<span style="color:red;font-weight:bold">假如我不听，非要自己选择之前添加的节点会怎么样？答：接入此设备的网络流量都会被代理，包括国内的app流量，一边会造成流量浪费，一边会拖慢你国内网络速度。</span>

###########################################################################

### 订阅链接添加

###########################################################################

​    点击上面的【节点订阅】，左下角【新增】，【备注】随意填，【订阅URL】填你的订阅链接，开启【自动更新订阅】，然后右下角【保存并应用】。再回到【节点订阅】页面，找到已经添加的订阅，右侧【手动订阅】。随后你就会在【节点列表】看到从订阅链接导入的节点了。

###########################################################################

![image.png](https://s2.loli.net/2025/04/07/4hczRWidBMNG1pE.png)



### Socks&HTTP服务

###########################################################################

​     Socks 和HTTP服务是通过开通端口，将服务暴露到局域网，允许局域网设备通过socks和HTTP协议接入的一种方法，你可以通过开启这种服务，仅仅在你的设备添加此服务，设备作为单独的路由存在，不影响其他网络设备。

仅仅需要填入任意端口即可，设置如下：

#![image.png](https://s2.loli.net/2025/04/07/18hpbtyUMeoi57R.png)

###########################################################################

大功告成！！！

###########################################################################



### 防火墙


---


<p style="color:red;font-weight:bold">注意：假如连接此网络后，你的国内网站无法接通，海外网站可以正常访问。此时你就要警惕了，你的防火墙出问题了！！！</p>

此时你需要在防火墙规则内添加如下一条规则：


```
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
```

<p style="color:red;font-weight:bold">如何添加，添加到哪里？</p>

在主页的功能栏找到【网络】-【防火墙】-【自定义规则】，在最后一行假如此条规则即可。

##################################################################

---

![image.png](https://s2.loli.net/2025/04/07/PNWnZYShx1tIdE2.png)

###################################################################

​                                         恭喜你，你已经完成了所有的设置项，Enjoy it.

###################################################################