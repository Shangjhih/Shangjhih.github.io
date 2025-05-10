---
title: Office 部署与激活
date: 2025-04-06 20:32:08
tags:
        - office
        - 命令行
        - 部署
categories:
        - office
        - 部署
        - 教程
---
# Office部署



## 准备材料

- 官方Office安装包[setup.exe](https://www.microsoft.com/en-us/download/office)
> 进入此网页后会看到 <span style="color:red"> 01 Office Deployment Tool </span>,点击进入下载

- 应答文件[config.xml](https://config.office.com/deploymentsettings)



***☝点击文件名即可跳转到该文件的下载网页***<span style="color:red">   安装新版本前请自行卸载原有的office</span>

---

## 安装包文件

​       ***点击[此处](https://www.microsoft.com/en-us/download/details.aspx)获取文件下载链接(材料准备中也有提到)***



1. 点击**Download**按钮下载安装包


![image.png](https://s2.loli.net/2025/04/06/KNImZip4aCteT9V.png)

此后你将会得到一个setup.exe文件，双击文件，他将询问你安装（解压）到哪个位置，此时在桌面右键新建一个非中文的文件夹（建议名字为`office`），然后将文件解压到此位置。<span style="color:red;"> 虽然是exe文件，但它是一个压缩包，运行后会得到 <span style="color:blue"> configure.xml </span>和带有office 365标志的<span style="color:blue"> setup.exe </span>部署器。</span>

如下图所示：☟

---

![image.png](https://s2.loli.net/2025/04/06/aLlKC15eJ4tqjms.png)



![image.png](https://s2.loli.net/2025/04/06/D5S7RJbK9H6MzLB.png)

---

文件列表☟

- configuration-Office365-x64
- setup.exe

<p style="color:red;font-weight:bold"> xml文件是带有完整office套件的应答文件，使用此文件安装office会将全家桶一个不落安装完，但我们根本不需要这么多文件，所以建议将此文件删除，我们下一步配置自己需要的应答文件</p>

---

## 下载config.xml应答文件

**[点此](https://config.office.com/deploymentsettings)进入文件的下载网站**

---

![image.png](https://s2.loli.net/2025/04/06/DjSoJPAYKBOT39v.png)


![image.png](https://s2.loli.net/2025/04/06/yh61PJrCTlqFBnu.png)

---
**左侧会有文件的配置列表，按下图的标记进行修改**

---

![image.png](https://s2.loli.net/2025/04/06/yFT4IBP6xm9Mhi1.png)


![下载选项](https://s2.loli.net/2025/04/06/b8xrLYugRf9zZyt.png)

![image.png](https://s2.loli.net/2025/04/06/2pyqu1ON8chdFVA.png)

![image.png](https://s2.loli.net/2025/04/06/fc4jadku5HSBi1r.png)

![image.png](https://s2.loli.net/2025/04/06/Oa4To1IwG5RgF8z.png)

![image.png](https://s2.loli.net/2025/04/06/8U56ZTiBVJu2zNw.png)

![image.png](https://s2.loli.net/2025/04/06/51G8znlHYKmkNMO.png)

![image.png](https://s2.loli.net/2025/04/06/HjbwshySXVkxKQ3.png)

---

导出后你将会得到一个包含你选择的xml文件，将此文件复制到你桌面的`office`文件夹，将其与`setup.exe`文件放在一起☟☟☟

---

![image.png](https://s2.loli.net/2025/04/06/IUdFCRYEjoaxQhX.png)

---

此时到电脑左下角搜索`powershell`,然后以管理员身份运行☟☟☟

---

![image.png](https://s2.loli.net/2025/04/06/Wm1RgqAeNMPU5H4.png)

![image.png](https://s2.loli.net/2025/04/06/pb78nVBysaH4JcK.png)

---


**在powershell中输入** `cd` **然后加个空格，再点击鼠标右键即可将地址复制到命令框内**

参见下图☟☟☟

---

![image.png](https://s2.loli.net/2025/04/06/yqxgFdLeAmtRJDl.png)

在Powershell中输入`./set`然后按Tab键补全，加个空格，随后输入`/configure`,再空格，输入应答文件的全名，如下图：

```powershell
./setup.exe /configure config.xml
```


点击回车，即可弹出office的下载框，等待即可。
<p style="color:red;font-weight:bold">屏幕右下角展开小箭头，就可以看到下载进度，假如下载进度很久都未更新，等待即可，需要一段时间。安装成功后会提示已经部署。开始进行激活步骤</p>

---

## 激活
1.复制命令

不要关闭powershell窗口，在此复制以下命令，然后右键粘贴到powershell中，点击回车，允许运行，等待激活窗口。命令如下☟☟☟
```powershell
                 irm https://get.activated.win | iex
```

---

2. 选择激活方式
<p style="color:red;font-weight:bold">输入数字`2`</p>

---

![image.png](https://s2.loli.net/2025/04/06/hznLyCWr1xPOHpw.png)

---
<p style="color:red;font-weight:bold">输入2后回车</p>

---

<p style="color:red;font-weight:bold">等待提示第二个窗口，再输入`1`,回车</p>


![image.png](https://s2.loli.net/2025/04/06/atISuJedZPf9vUQ.png)


---


<p style="color:red;font-weight:bold"> 等待提示绿色的 </p>
<span style="color:green;font-weight:bold">successfull!</span>

**到此即安装并激活完成！！！Enjoy your paper writting **