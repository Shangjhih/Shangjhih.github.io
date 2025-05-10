---
title: Hexo基本语法
date: 2025-01-31 15:51:30
tags:
    - Hexo
    - 部署
    - 博客
categories:
    - Hexo
    - 部署
    - 博客
---
### Hexo博客的部署      
- 安装git
- 安装NodeJS        
- 安装Hexo

### Hexo安装    

```powershell
$ npm install -g hexo-cli
```

使用此命令安装``hexo-cli``,也就是驱动Hexo的指令集    

### Hexo基本语法   

```powershell
$ hexo init
```

初始化Hexo项目，从Github拉取基本的Hexo博客源代码到本地  

```powershell
$ hexo init [blog name]
```

新建一个网站，网站名为``blog name``  

```powershell
$ hexo new [article title]
```

新建一个名为``article title``的文章

```powershell
$ hexo generate
```

生成静态文件    

```powershell
$ hexo s 或   hexo server
```

临时启动Hexo在本地4000端口的预览界面    

```powershell
$ hexo d 或  hexo deploy
```

将已经测试完成的静态页面部署到GitHub Pages
