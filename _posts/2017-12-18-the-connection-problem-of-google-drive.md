---
title: The connection problem of  Backup & sync from Google Drive 
description: 而世之奇伟、瑰怪、非常之观，常在于险远，而人之所罕至焉，故非有志者不能至也。
date: 2017-12-18 12：00
categories: 
 - FQ
tags: [Proxifier sock5, http, Google Drive]
---

昨天用 Privoxy 设置好了之后确实登录上了，可早晨打开电脑，又瞬间入坑，说啥也链接不上了，毕竟 Privoxy 没有 GUI（图形界面），需要命令行设置，太专业了。在尝试解决方案的时候，发现了 [Proxifier](https://www.proxifier.com/index.htm) 这一工具，原理和 Privoxy 一样，这个有 GUI，对于技术小白和普通用户相对友好一些，早晨设置完成之后，中午打开电脑，Backup & sync 依然是登录的状态，挺好用。同时不仅 Google Drive，其他的仅支持 http 的应用也方便了很多，实现了整个电脑走全局模式。下面依旧记录一下具体过程，以备参考学习。

### step1 下载安装 Proxifier 

1. 下载地址：[Download Proxifier](https://www.proxifier.com/download.htm) （windows 版本和 mac 版本都有）

### step2 导入配置文件

[GitHub（点击进入）](https://github.com/Jamesits/proxifier-profiles) 上有配置好的规则，有两种方法：

1. 直接下载其中的 Current.ppx 文件，导入到  ~/Library/Application Support/Proxifier/Profiles 。

2. 使用 git 命令，然后建立一个软连接。

导入配置文件之后，重新打开 Proxifier，在程序中切换配置文件。我是用的是 git 方法，因此显示不是 Current，而是开发者的名字。

![](http://wx4.sinaimg.cn/large/6a959c93ly1fmktvdhxi9j218g0rsqf5.jpg)

### step3 自定义规则

1. 检查 Proxies（代理服务器）配置，需要与 shadowsocks 的本地端口一致。我使用 shadowsocksx-ng，需要更改为 127.0.0.1:1086 。

   ![](http://wx3.sinaimg.cn/large/6a959c93ly1fmktvd3licj218g0mygq7.jpg)

2. 设置 Rules（规则）：在 Google Desktop Softwares 一处增加 Backup and Sync 。

   ![](https://i.loli.net/2017/11/25/5a19298ec59dc.jpg)

   (图片来自 [Bates' Blog](https://blog.batesma.com/))

上述步骤顺利完成，Google Drive 又重新登录啦。早晨我问自己，费劲不？为啥不放弃这个另选一个云端，这样折腾来折腾去的……我想到了高中时候学了王安石的《游褒禅山记》中的一段：

> 古人之观于天地、山川、草木、虫鱼、鸟兽，往往有得，以其求思之深，而无不在也。夫夷以近，则游者众；险以远，则至者少。而世之奇伟、瑰怪、非常之观，常在于险远，而人之所罕至焉，故非有志者不能至也。有志矣，不随以止也，然力不足者，亦不能至也。有志与力，而又不随以怠，至于幽暗昏惑而无物以相之，亦不能至也。然力足以至焉，于人为可讥，而在己为有悔；尽吾志也而不能至者，可以无悔矣，其孰能讥之乎？此余之所得也。

共勉！

2017-12-18 12: 47

参考文档

* [使用 Proxifier, 为Google Drive 的 Backup & Sync 进行代理 - Bates' Blog](http://blog.batesma.com/20170811-google-drive-proxy-solved/)
* [Jamesits'GitHub](https://github.com/Jamesits)
* [Proxifier：给某个单独应用配置代理上网服务 – 老柴的宅](http://chaishiwei.com/blog/830.html)