---
title: Windows KMS激活
date: 2025-03-28 16:13:27
tags: 
        - 激活
        - office
        - KMS
        - Windows
categories:
        - 激活
        - office
        - KMS
        - Windows
---

​      Windows的激活方式有很多，也有很多的激活工具，本次我们将会程序性地讲一下KMS激活Windows的基本流程。（按此套路进行即可正确激活）


<p style="color:red;font-weight:bold">尽量使用powershell来运行提到的代码</p>

<p style="color:red; font-weight:700"> 家庭版不可使用此教程进行激活！！!</p>

​     此次我们背景为：为一台没有激活凭证的新系统进行KMS激活，一般你所购买的笔记本都会有一个永久密钥附带在设备的主板，也就是你的永久激活凭证。即使你重装系统,只要你重装的系统和设备购买时的系统版本一致，你的系统就会自动激活。
假如你购买设备时附带的系统版本为**家庭版**，重装系统的版本为**专业版**或者**专业工作站版**，此时你的主板激活密就无法激活现有系统，此时便符合此教程的参考环境。自己组装的台式机装系统，也符合此教程的背景。

---

### **STPE 1**  卸载系统原有密钥

​       不管当前系统有没有密钥，都建议执行该命令
```powershell
        slmgr.vbs /upk
```

---

### **STEP 2**  安装密钥

   安装Windows提供的官方kms密钥（文末会有提供），该密钥是KMS密钥，需要匹配系统版本。
不知道自己系统版本请使用`win`+`r`调起运行框，输入`winver`回车后即可查看你当前的系统版本（家庭版、专业版、教育版、LTSC版、IOT版、专业工作站版）。然后到文末找到符合你系统版本的密钥，复制替换以下命令中的密钥。（下面命令使用的是专业版密钥）

```powershell
          slmgr.vbs /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
```

---

### **STEP 3**  指定KMS服务器

​    KMS服务器可以提供激活验证，可自行部署，此处会提供几个服务器地址，请自行替换使用。KMS激活有一定的周期，每180天都需要访问一次你指定的KMS服务器，服务器停止服务的话你的激活也会失效，本次我们会提供几个长久性的服务器地址。
```powershell
           slmgr.vbs /skms kms.micaesoft.com
```
​     代码中的`kms.micaesoft.com`可替换为以下地址(推荐使用前三个)
```
fsu-kms-03.fsu.edu
kms.ghxi.com
kms.micaesoft.com
kms.digiboy.ir
hq1.chinancce.com
54.223.212.31
kms.cnlic.com
kms.chinancce.com
kms.ddns.net
franklv.ddns.net

zh.us.to
toxykz.f3322.org
192.168.2.81.2.7.0
kms.guowaifuli.com
106.186.25.2393
rss.vicp.net:20439

```

---

### **STEP4**  执行激活命令
```powershell
              slmgr.vbs /ato
```
回车等待激活成功提示

---

## 附录
| Microsoft官方激活密钥列表 |  |
| :------ | :-------: |
| 系统版本 | 密钥 |
| Windows 10/11 专业版 | W269N-WFGWX-YVC9B-4J6C9-T83GX |
| Windows 11/10 Pro N | MH37W-N47XK-V7XM9-C7227-GCQG9 |
| Windows 10/11 专业工作站版 | NRG8B-VKK3Q-CXVCJ-9G2XF-6Q84J |
| Windows 10/11 教育专业版 | 6TP4R-GNPTD-KYYHQ-7B7DP-J447Y |
| Windows 10/11 企业版 | NPPR9-FWDCX-D2C8J-H872K-2YT43 |