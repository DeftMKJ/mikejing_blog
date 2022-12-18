---
title: "IOS内存管理初始篇"
description: "iOS内存管理初始篇"
keywords: "iOS内存管理初始篇"
expand: false
toc: true

date: 2022-12-18T12:28:58+08:00
lastmod: 2022-12-18T12:28:58+08:00

categories:
  - iOS
tags:
  - iOS
  - 内管管理
  - Autorelease Pool

# 原文作者
# Post's origin author name
#author:
# 原文链接
# Post's origin link URL
#link:
# 图片链接，用在open graph和twitter卡片上
# Image source link that will use in open graph and twitter card
#imgs:
# 在首页展开内容
# Expand content on the home page
#expand: true
# 外部链接地址，访问时直接跳转
# It's means that will redirecting to external links
#extlink:
# 在当前页面关闭评论功能
# Disabled comment plugins in this post
#comment:
#  enable: false
# 关闭文章目录功能
# Disable table of content
#toc: false
# 绝对访问路径
# Absolute link for visit
#url: "ios内存管理初始篇.html"
# 开启文章置顶，数字越小越靠前
# Sticky post set-top in home page and the smaller nubmer will more forward.
#weight: 1
# 开启数学公式渲染，可选值： mathjax, katex
# Support Math Formulas render, options: mathjax, katex
#math: mathjax
# 开启各种图渲染，如流程图、时序图、类图等
# Enable chart render, such as: flow, sequence, classes etc
#mermaid: true
---

iOS内存管理初始篇(测试)

###  1. Why Reduce Memory

- 更好的用户体验
  - 启动更快
  - 系统表现更好
  - App存留时间更长

<!--more-->

### 2. Memory Footprint

Not all memory is created equal

https://juejin.cn/post/6844903621276991502#heading-3


### 3. 命令

#### 3.1 `vmmap`

查看详细报告

```shell
vmmap xxx.memgraph
```

查看摘要报告

```shell
vmmap --summary xxx.memgraph
```

配合`grep`命令查看所有动态库的Dirty Pages的综合

```
vmmap -pages xxx.memgraph | grep '.dylib' | awk '{sum += $6} END { print "Total Dirty Pages:"sum}'
```

只显示内存异常相关模块的数据`CGImage`

```
vmmap xx.memgraph | grep 'CG image'
```

更多文档

```
man vvmap
man leaks
man heap
```



#### 3.2 leaks

查看泄漏的内存

```
leaks xxx.memgraph
```

查看某处的内存泄漏

```
leaks --traceTree [address] xxx.memgraph
```



#### 3.3 heap

查看所有堆区对象的内存使用

```
heap xxx.memgraph
```

默认情况下是按照对象数量进行排序的，通常情况他们不会造成什么内存问题。我们关心的是内存大小，因此按照`-sortBySize`的方式进行大小顺序来查看所有堆区对象的使用

```
heap xxx.memgraph -sortBySize
```

有了这些对象的内存地址后，我们还需要工具进行下一步分析。



#### 3.4  malloc_history 

开启：

在 `Product -> Scheme -> Edit Scheme -> Diagnostics` 中，开启 `Malloc Stack` 功能，建议使用 `Live Allocations Only` 选项

查看内存分配历史

```
malloc_history xxx.memgraph [address]
malloc_history xxx.memgraph --fullStacks [address]
```



<!--more-->
