---
title: Hexo 侧边栏配置
date: 2025-04-12 16:01:54
tags:
        - Hexo
        - 问题处理
        - 配置文件
        - 博客
categories:
        - Hexo
        - 问题处理
        - 配置文件
        - 博客
---
# Hexo侧边栏功能配置

> 1.修改_config.yml文件

> 2.初始化功能区

> 3.添加tags和categories参数



##  修改配置文件

Hexo的配置文件在项目根目录，文件名称为`_config.yml`

在配置文件中添加一个名为`menu`的块，填入以下参数：

```yaml
menu:
  home: /
  about: /about
  categies: /categories
  tags: /tags
  archives: /archives
```

最好保证该代码块与前后代码块各距三行。

---

## 初始化功能区

### 生成配置

在项目的根目录使用以下命令对以下三个参数进行初始化

```powershell
hexo new page about
hexo new page tags
hexo new page categories
```

生成的文件夹在`source`目录,分别有以下三个

> \- tags
> \- about
> \- categories 

每个文件夹下都会有一个叫做`index.md`的文件，这就是初始化生成的文件。

### 修改配置

三个文件分别添加`type`和`layout`两个参数，每个参数都对应各自文件的名字

***about下index.md***

```yaml
---
title: about
date: XXXX-XX-XX XX:XX:XX
type: "about"                # 添加此行
layout: "about"              # 添加此行
---
```

***tags下index.md***

```yaml
---
title: about
date: XXXX-XX-XX XX:XX:XX
type: "tags"                # 添加此行
layout: "tags"              # 添加此行
---
```



***categories下index.md***

```yaml
---
title: about
date: XXXX-XX-XX XX:XX:XX
type: "categories"                # 添加此行
layout: "categories"              # 添加此行
---
```

---



### 添加参数

在每一个文章中都添加`tags`、`categories`两个参数，参数后跟上你文章的内容方向和类型，写在每个参数后面且严格按照规范进行，以下为文章开头的举例

```markdown
---
title: Cloudflare WARP 出口代理学习笔记
date: 2025-04-05 13:16:57
tags:
    - tag1
    - tag2
    - tag3
    - tag4
categories:
    - categories1
    - categories2
    - categories3
    - categories4
---
```

`tags`和`categories`使用符号`-`隔开可以为文章添加多个类型，也可以添加单个类型。
##############################################################################

<p style="color:red;font-weight:bold">所有配置文件修改后记得保存!!!</p>

##############################################################################

确定修改无误后使用

```powershell
                      hexo generate
```

生成静态文件

---

使用命令

```powershell
                      hexo deploy
```

将生成的静态页面通过`git`推送到GitHub action生成网页。
##############################################################################
                            ***All Done***
##############################################################################
<p style="color:red;font-weight:bold">Attention!!!注意yaml的语法规范</p>