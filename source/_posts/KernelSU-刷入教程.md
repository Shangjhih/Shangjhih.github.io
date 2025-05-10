---
title: KernelSU 刷入教程
date: 2025-03-24 17:12:53
tags: 
      - 安卓
      - 刷机
      - Kernel SU
      - root
categories: 
        - 刷机
        - ROOT
        - Kernel SU
---

#### Kernel SU刷入教程

> Kernel su 是一个基于内核的root方案，是Magisk、Apach、Kitsuni等项目的同类解决方案
但是Kernel su是基于内核的root方式，Magisk是基于systemless实现的，在原理上来说KSU的隐藏能里是要高于Magisk的
此文以官方版本的Kernel su作为案例分析其刷入方式。


------------------------------------------------------------------------------------------------------


以下为Kernel su官方的[***介绍文档***](https://kernelsu.org)和[***Github项目地址***](https://github.com/tiann/KernelSU)

---
***What is KernelSU?***
	KernelSU is a root solution for Android GKI devices, it works in kernel mode and grants root permission to userspace appsdirectly in kernel space.

***Features***
	The main feature of KernelSU is that it's kernel-based. KernelSU works in kernel mode, enabling it to provide a kernel interface that we never had before. For example, it's possible to add hardware breakpoints to any process in kernel mode, access the physical memory of any process invisibly, intercept any system call (syscall) within the kernel space, among other functionalities.

​	Additionally, KernelSU provides a module system via OverlayFS, which allows you to load your custom plugin into system. It also provides a mechanism to modify files in /system partition.

---

**刷入步骤**

​	1.安装adb环境和[安卓通用驱动](https://lsdy.top/azqd/)（adb环境的安装看前文，有提到文件的下载的地址与安装方式）
​	2.解锁手机的Bootloader
​	3.获取适合当前系统的内核文件
​	4.刷入内核文件并安装管理器和相关模块

---

#### 解锁Bootlaoder

​	鉴于每家厂商的解锁政策都不同，且最近小米收紧了其解锁政策，此次就拿一加（OnePlus）作为参考
因其解锁方式极为简便，便以此为案例。



**注意**
	手机解锁Bootloader的时候会清除手机内所含的所有数据，在进行操作之前请确保您的数据已进行妥善的迁移与保存！！！

---




​	进入开发者模式，在系统的<p style="color:red" >【关于手机】</p>界面找到【系统版本号】，快速点击5-7次，桌面会弹出【您已进入开发者模式】
  搜索【开发者模式】进入其设置界面，下滑找到并开启【OEM解锁】【允许USB调试】，两项都需要打开。
  在确认都已经打开后将手机通过USB线连接至电脑，打开你的Powershell，在窗口输入

  ```
                            adb reboot bootloader
  ```

  待手机进入fastboot模式后输入以下命令对其进行解锁（命令来源于[Android官方](https://source.android.com/docs/core/architecture/bootloader/locking_unlocking?hl=zh-cn)）

  ```
                            fastboot flashing unlock
  ```

 待手机提示是否解锁Bootloader，使用音量键移动光标，使用电源键表示确认。选择确认解锁Bootloader，等待手机重启，重启期间系统会清空所有的 数据，这时你再反悔就都来不及了。随后等待进入系统即可。

 ---

​	  进入系统后到应用商店下载【Devtools】，查看你的安卓内核版本，如下图所示

![](https://s2.loli.net/2025/03/25/JaKSBWGF15g2Lhk.png)

​    	图示版本为4.19.157，假如你的内核版本在5.12以上，到此处下载符合你系统版本的内核文件[Github地址](https://github.com/tiann/KernelSU/releases)，Kernel su的管理器地址和以上提供的地址是一个，都在assets中发布，apk文件在列表的下部，请自行翻找。若你的内核版本低于5.12，那就说明你的设备不能通过此方式获取，不符合GKI的内核规范，需要自行编译或者在【酷安】【Telegram】等全平台寻找适合你手机型号的内核（非同型号内核不可互刷！！！），切勿刷入来源不明的zip文件！！！



​	此处提供的内核版本有三种格式，我不能确认你的系统是哪个版本的文件系统，所以建议你使用以下方式来对其进行临时启动，内核文件和管理器安装包下载地址见此：

|  |
| ------ |
| ![](https://s2.loli.net/2025/03/25/MAVYRNZPS2QytCb.png)  | 
| ![](https://s2.loli.net/2025/03/25/y3vWR9nrtd4OuZo.png) |

文件分别为：

* andoid14-6.1.84_2024-07-boot-gz.img.gz

* andoid14-6.1.84_2024-07-boot-lz4.img.gz

* andoid14-6.1.84_2024-07-boot.img.gz

* KernelSU_V1.0.3_12018-release.apk

​     下载文件后将其解压，得到以`img`结尾的镜像文件。其中的`gz`  `lz4`都表示系统使用的文件格式，第三个为通用格式，此时建议您使用临时刷入的方式来尝试（有些案例表示一加手机使用的是`gz`格式的文件系统），因不确定，在无准确信息的情况下建议临时启动，确保无问题后再将其刷入。在此之前请安装【Kernel su manager】，用于在开机进系统后判断刷入是否有效。最后一个apk文件问管理器的安装包，需提前安装。

#### 进入fastboot模式

```adb reboot bootlaoder
adb reboot bootlaoder
```



输入命令临时刷入：

```bash
fastboot boot <文件的绝对路径>

例
fastboot boot C://USER/NAME/Desktop/123/kernel-version-boot.img
```

进系统后查看管理器是否识别出内核


<img src ="https://s2.loli.net/2025/03/25/1j3HMvciIYtfCUJ.png" width="200" />

如此图显示，则表示已经成功刷入，如不能进系统或此管理器未能识别到内核，则换第二个文件重新执行命令，确认管理器能识别到内核后，进入fastboot模式执行以下命令永久性刷入至系统:

```
fastboot flash boot <文件的绝对路径>

例
########################################################################
fastboot flash boot C://USER/NAME/Desktop/123/kernel-version-boot.img
(使用fastboot，通过flash命令将位于`C://USER/NAME/Desktop/123/kernel-version-boot.img`的文件输入到`boot`分区)
```

刷入后便可以永久使用。



#### 推荐的模块：
---

|   **Magisk模块**   |   **作用**   |
| :----: | :----: |
|   [zygisk-next](https://github.com/Dr-TSNG/ZygiskNext/releases)   |   Standalone implementation of Zygisk, providing Zygisk API support for KernelSU and a replacement of Magisk's built-in Zygisk.   |
|   [zygisk-lsposed](https://github.com/mywalkb/LSPosed_mod/releases/download/v1.9.3_mod/LSPosed-v1.9.3_mod-7244-zygisk-release.zip)   |   LSPosed is a great XPosed Framework, but it has a big problem, only manager can manage scope. LSPosed team don't accept PR for CLI or API Module, the TODO issues are old more one year and never completed, is more important the GUI changed many times but not CLI or API Module. In my fork API Module and CLI are implemented. CLI require root user because must access files readable only by root.   |
| [Universal GMS DOZE](https://github.com/gloeyisk/universal-gms-doze/releases/download/1.9.2/gms_1.9.2.zip) |   Patches Google Play services app and certain processes/services to be able to use battery optimization Support API 23 or later Support Magisk ernelSU, and APatch root implementations   |


| **lSPosed模块** | **作用** |
| :------: | :------: |
| [Hide my applist](https://github.com/Dr-TSNG/Hide-My-Applist/releases/download/V3.4/HMA-V3.4.r436.d03edf7-release.zip) | Although it's bad practice to detect the installation of specific apps, not every app using root provides random package name support. In this case, if apps related to root (such as Fake Location and Storage Isolation) are detected, it is tantamount to detecting that the device is rooted.Additionally, some apps use various loopholes to acquire your app list, in order to use it as fingerprinting data or for other nefarious purposes. |
| [HyperCeilier](https://github.com/ReChronoRain/HyperCeiler/releases/download/2.5.154/HyperCeiler_2.5.154_20250101_154_release.apk) | 修改miui和Hyper os的系统应用，增强其功能,  **仅适用于小米官方系统和官改！！！** |
| [Play integrity Fix](https://github.com/chiteroman/PlayIntegrityFix/releases/download/v18.8/PlayIntegrityFix_v18.8.zip) | This module is not made to hide root, nor to avoid detections in other apps. It only serves to pass Device verdict in the Play Integrity tests and certify your device. All issues created to report a non-Google app not working will be closed without notice. |
| [Thanox](https://uploadrar.com/s1jzriq9foy0) | 人称‘灭霸’，可以最大限度管理和调整系统功能 |
| [Youtube Adaway](https://github.com/wanam/YouTubeAdAway) | 清除Youtube播放广告，但不能清除首页广告，可以支持后台小窗播放去除视频中穿插的广告 |

------------------------------------------------------------------------------------------
设备已虚焊，拆机中，未写完的下次再写，各位再见。
