---
title: 类原生WiFi叹号无网络解决方法
date: 2025-03-31 10:17:40
tags: 
        - 小记
        - 刷机
        - 类原生
        - WIFI 叹号
categories: 
      - 安卓
      - Android
      - 刷机
---


手机在刷国际版或类原生系统后，连接国内的WiFi网络会出现WIFI无网络或者连接能力受限的提醒，一定程度上影响使用。


---


其原因是：Google在Android 5.0后引入了 【Captive Portal】机制来检测WiFi网络认证，以判断WiFi的网络连接性。
aosp默认会将默认检测的服务器设为Google自身的地址，而中国网络环境特殊，无法直连Google，类原生及外版系统
默认都是以Aosp规范作为检测依据，顾导致此问题。

---

**解决方法**
**注意提前打开开发者选项的【USB调试】【USB调试(安全设置)】**
使用adb命令对【Captive Portal】服务器地址进行修改：

1.删除原有的服务器设置
```shell
adb shell settings delete global captive_portal_https_url
```
```shell
adb shell settings delete global captive_portal_http_url
```
<p style="color:red;font-weight:bold"> 除了使用上面两行删除命令，还可以直接将原参数修改为0，同样可以达到同样的效果，命令如下：</p>
```shell
adb shell settings put global captive_portal_mode 0
```

2.设置新地址
```shell
adb shell settings put global captive_portal_http_url http://connect.rom.miui.com/generate_204
```
```shell
adb shell settings put global captive_portal_https_url https://connect.rom.miui.com/generate_204
```