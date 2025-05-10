---
title: Redmi Lime卡刷CrDroid
date: 2025-02-20 18:36:04
tags:
    - TWRP
    - 刷机
    - 救砖
    - Crdroid
    - 类原生
categories:
    - TWRP
    - 刷机
    - 救砖
    - Crdroid
    - 类原生
---
大概记录一下红米note9 4G版本刷CrDroid的简单流程

前期准备：

---
> 已经解锁的红米note9 4G  

> TWRP镜像  

> 一台电脑  

> CrDroid卡刷包（zip格式） 




| <img src="https://s2.loli.net/2025/02/20/OYupMkNtrKPZT3d.jpg" alt="红米note9" width="200"/> | <img src="https://s2.loli.net/2025/02/20/sk9TcE2w6PgXuhf.png" alt="Twrp镜像"  width="200"/> | <img src="https://s2.loli.net/2025/02/20/tHRyWAYfiSP5m2e.png" alt="CrDroid卡刷包" width="200"/> |
|:-----------------------------------------------------------------:|:-----------------------------------------------------------------:|:-----------------------------------------------------------------:|
|                                解锁BL的红米note9                                |                                Twrp镜像                               |                                CrDroid卡刷包                                |

---

1.在电脑安装ADB驱动 [驱动下载直链](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)
2.打开手机的开发者模式
3.使用adb 命令将TWRP刷入到恢复分区
4.刷入卡刷包

---


#### 驱动安装

下载提供的安装包，双击安装。
找到安装位置，找到adb.exe所在的目录，复制目录地址，进入Windows的环境变量，找到PATH，双击进入，添加一个名为adb的新变量，并将adb所在的目录粘贴到路径框
![664fa6c2c20c45177b56c332b282141.png](https://s2.loli.net/2025/02/20/NwVCncbyJgU2urQ.png)
此后你就可以在任意路径下打开powershell使用adb命令了

#### 打开开发者模式

打开手机，找到关于手机页面>>>>>找到系统版本号>>>>>>>>快速点击版本号10次等待提示开发者模式已打开>>>>>>>>>回到手机的设置界面，找到更多或者使用搜索框搜索”开发者模式“，进入开发者模式，点击开关来开启，向下滑，找到**允许USB调试**并打开。
在手机已经连接电脑的情况下手机会弹出是否允许调试的通知，点击允许。

#### 使用adb命令

使用`win+r`调出运行窗口，输入`powershell`然后回车，进入蓝色的命令窗口

输入 
                              adb devices

来检测设备设否已经连接，提示手机序列号即代表已经连接至电脑
提示如下：

```powershell
PS C:\Users\user> adb devices
List of devices attached
* daemon not running; starting now at tcp:5037
* daemon started successfully
1c17de221020    device            # 这里输出的就是手机序列号
```

此时输入命令 

                      adb reboot bootloader

进入到Bootloader模式

待手机震动后，在窗口输入

                     fastboot devices

输出设备信息即表示已经连接到fastboot端口


此时使用`cd`命令将powershell所处的路径切换到你的twrp所在路径

                    cd "C:\user\file\twrp路径"


#### 刷机详细流程
##### TWRP刷入

此时查看你的手机是否是动态分区，是的话使用命令一刷入镜像，不是的话使用命令二
```powershell
fastboot flash recovery <recovery_name>     #命令1

fastboot boot <recovery_name>               #命令2
```

此时同时按住手机的音量+和电源键，待手机进入recovery


进入recovery后电脑会叮咚一声表示连接到设备，此时将下载好的卡刷包复制到手机根目录
找到`刷入`,再找到已经传入手机的刷机包，选择后刷入，等待刷入的进度条走完后找到`清除`模块
选择恢复出厂双清（双清指的是清除cache和data分区）
，双清后即可开机。

##### ADB Sideload 模式刷入

进入Twrp后找到`高级`,找到`adb sideload`,点击后会直接双清
，然后在电脑中使用以下命令刷入

```powershell
adb sideload <刷机包绝对路径加名字>
```
等待进度条走完后会自动重启进入系统。



成品如下

| CrDroid |  |  |
| :------ | :------: | :------: |
| ![Screenshot_20250212-212232_crDroid Home.png](https://s2.loli.net/2025/02/20/M4srVdavDz92mnW.png) | ![Screenshot_20250212-211440_crDroid Home.png](https://s2.loli.net/2025/02/20/YZWF7odbnMC9RtV.png) | ![Screenshot_20250212-211433_crDroid Home.png](https://s2.loli.net/2025/02/20/i2bAstWlCc1KyOE.png) |
| ![Screenshot_20250125-193919_设置.png](https://s2.loli.net/2025/02/20/d5GhbZw2o8RVq6x.png) | ![Screenshot_20250125-194222_设置.png](https://s2.loli.net/2025/02/20/F2hgOETGNs5v4ZU.png) | ![Screenshot_20250220-195236_更新工具.png](https://s2.loli.net/2025/02/20/Hm6FI8fKMnD37ge.png) |

| Infinity |  |  |
| :------: | :------: | :------: |
| ![Screenshot_20250212-164321_Infinity_X_Launcher.png](https://s2.loli.net/2025/02/20/k5Nc3bivLDzYqIV.png) | ![Screenshot_20250212-164311_KernelSU.png](https://s2.loli.net/2025/02/20/zCqRXtwIWedZ3ro.png) | ![Screenshot_20250212-164443_设置.png](https://s2.loli.net/2025/02/20/2EX1KYlsI6rhiZb.png) |
| ![Screenshot_20250212-164342_系统更新.png](https://s2.loli.net/2025/02/20/cn2IyXmvl6RqpUg.png) | ![Screenshot_20250212-171104_Infinity_X_Launcher.png](https://s2.loli.net/2025/02/20/f6YXgVCqLJ4R8y7.png) | ![Screenshot_20250212-170922_Shell.png](https://s2.loli.net/2025/02/20/v1zhAaDu4w8xGpP.png) |

