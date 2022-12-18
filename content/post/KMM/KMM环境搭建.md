---
title: "KMM环境搭建"
keywords: "KMM环境搭建"


date: 2022-12-18T21:38:01+08:00
lastmod: 2022-12-18T21:38:01+08:00

categories:
  - KMM跨平台
tags:
  - 跨平台
  - Kotlin

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
#url: "kmm环境搭建.html"
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

### 1. 操作系统 

操作系统版本：最高支持 `Monterey` ，最低支持 `Big Sur`
验证：
`左上角 ---> 关于本机 ---> macOS Monterey`
<!--more-->

### 2. iOS 环境

#### 2.1 Xcode

支持 `13.2.1` ,可直接通过 `Apple Store` 更新

```shell
xcodebuild -version 

Xcode 13.2.1 
Build version 13C100
```



#### 2.2 Cocoapods

```shell
// 安装命令
sudo gem install cocoapods -v 1.10.1 -n /usr/local/bin
sudo gem install cocoapods-generate -v 2.2.2
```

验证：

```shell
gem list | grep 'cocoapods'

cocoapods (1.10.1)
cocoapods-generate (2.2.2)
```



#### 2.3 内网源

更新本地源

```shell
// 执行
pod repo list
pod repo update
```





### 3. Android 环境

#### 3.1 Android Studio

`左上角Android Studio ---> About Android Studio ---> Android Studio Arctic Fox | 2020.3.1 Patch 3+ 或者最新版本`
建议修改配置：
Auto Import：Setting - Editor - General - Auto Import，勾选Optimize imports on the fly和Add unambiguous imports on the fly
作者信息：Setting - Editor - File and Code Templates - include - File Header

```shell
/**
 * Usage:
 *
 * author: ${USER}
 * Date: ${DATE}
 * Description:
 */

```

#### 3.2 KMM 插件

和Android Studio配套
`Android Studio ---> Preferences ---> Plugins` 搜索 `KMM` 并安装插件即可

#### 3.3 `Gradle`、Gradle插件、Kotlin

代码已经设置好，run时会自动下载
Gradle验证：
项目根目录打开 `Terminal`

```shell
//执行
./gradlew -v 
```

#### 3.4 JDK

`Android Studio ---> Preferences ---> Gradle ---> Gradle JDK 中选中JDK11即可`



### Q&A

#### 1. 非M1环境下上述环境都配置正确， `pod gen xxx` 报错，怎么办

[Git 用户名密码管理](https://support.huaweicloud.com/intl/zh-cn/usermanual-codehub/devcloud_hlp_00073.html#devcloud_hlp_00073__section33428900)

#### 2. 环境配置正确，出现如下错误

gradle 缓存问题，清理缓存重新build

#### 3. 如何清理缓存

轻度清理： `Build --> Clean Project` or 项目根目录手动删除 `build` 文件夹
彻底清理：`File` -> `Invalidate Caches/Restart`

<!--more-->