---
title: Zotero 基础设置填坑记
description: 工欲善其事，开始利其器。
date: 2017-12-18 19: 44
categories: 
 - strong tools
tags: [Zotero]
---

Zotero 是一款文件管理软件，阳志平老师力荐，入门有一些门槛，上一周终于破门而入，基础设置成功，记录下来，以备参考、学习。我的设置是按照阳志平老师的 zotero 系列博文来设置的，我记录一下自己遇到的坑以及解决方案。请先参考  [Zotero 入门系列](http://www.yangzhiping.com/tech/zotero1.html)。

### 下载、安装及注册

1. 关于 Zotero sandstone 的版本选择

  Zotero 最新的版本是 5.x，经过实践，到这篇文章的写作时间，仍然有部分插件不支持 Zotero 5，因此，我还是退回到 Zotero 4 版本。

  下载地址：[Zotero - Downloads](https://www.zotero.org/download/)
  
2. 除了 PC 版本的 Zotero sandstone，再下载一个 Zotero Connector 作为浏览器插件。

3. 然后在 Zotero 网页版点击 Register 注册一个用户。

### 配置 Zotero

按照  [Zotero（1）：文献管理软件Zotero基础及进阶示范 ](http://www.yangzhiping.com/tech/zotero1.html) 一路设置下去，我遇到过的坑，可能也是你遇到的问题。

1. 关于 Windows 客户端 Search（检索）--> PDF Indexing（PDF 索引）的设置，请参考 [研发狗日记17-Zotero小白安装记（1）](http://www.jianshu.com/p/ffa2e1d49cdb) 。诗颖小伙伴想尽叙述了这一过程和解决方案。 mac 客户端没有这一道坎儿。

2. 云盘同步

  Zotero 自己提供的空间有限，因此，我们要将存放文档的文件夹提出来放在云端，达到节约空间的目的。具体的思路就是：将 Zotero 中存放文档的 storage 文件夹剪切到云端，然后建立一个软连接到 Zotero 下的 storage 文件夹，实现两个文件夹的同步，而又不占用 Zotero 的空间。
  
   这里又涉及到几个问题：
   
  * 关于云端的选择
     
    阳老师使用的是 Dropbox，经过实践，还是跟阳老师的步调一致比较好，方便后面的设置。因为后面如果要使用 [Notability](http://gingerlabs.com/)（一款笔记 App）标记 PDF 的话，并且实现电脑和平板之间的互动传递，Dropbox 是首选云端，并且没有国内云端的选项。
	
  * 关于软连接的建立，也就是如何同步。
    
	第一步就是将 Zotero 目录下 storage 文件夹剪切出来。有的同学找不到 storage，那么你去找一篇 PDF 文档储存到 Zotero 它就出来了，而 Zotero 5 版本直接就有。
	
	第二步也是关键的一步，建立软连接。阳老师使用的是命令行：
	
	```
	ln -s /users/ouyang/dropbox/zotero/storage /users/ouyang/dev/zotero/storage
	```
	技术小白咋办？思路：找到你电脑的终端，把上面的命令行拷贝到你的终端，并且把文件的路径修改为你自己的路径，按回车。（此处搜索关键词：软连接，终端）操作成功的样子：
	
	![](http://wx3.sinaimg.cn/large/6a959c93ly1fmlaigz9lxj216w0vu4fc.jpg)

  基础配置完成以后，就可以尝试一下各种导入了，神奇到爆！


### 建立一些自己的搜索分类

参考：[Zotero（2）：作为知识管理工具的Zotero](http://www.yangzhiping.com/tech/zotero2.html)

按照阳老师博客的示范，建立一些神奇又方便的搜索如下：

![](http://wx3.sinaimg.cn/large/6a959c93ly1fmlai6mdy9j216y0nun54.jpg)

熟悉 Zotero 操作之后可以自己开发新的搜索需求。

### 在 iPad 上使用 Zotero

参考：[Zotero（3）：平板与社交：再谈研究辅助工具Zotero兼配套APP ](http://www.yangzhiping.com/tech/zotero3.html)

最开始没太懂原理，看了几遍之后明白了，就是在 iPad 的 Safari 创建一个类似浏览器插件的按钮，只不过这个按钮的形式是 Safari 收藏夹中的书签，每当有需要导入到 Zotero 的内容，则点一下书签，便成功地导入到 Zotero 了。具体步骤按照阳老师文章中的提示，难度不大，iPad Safari 设置成功入下图，比如我想把豆瓣《自私的基因》这本书的信息导入到 Zotero：

![](http://wx1.sinaimg.cn/large/6a959c93ly1fmlapt5l8fj20u0140nhy.jpg)

再来看一下电脑端 Zotero 里面的内容，《自私的基因》马上导入进来了。

![](http://wx3.sinaimg.cn/large/6a959c93ly1fmlaifwiysj21200qgwwv.jpg)

### 使用 Notability，通过 Dropbox 导入到 Zotero 里面的 PDF 文档，并写批注。

Notability 是一款 PDF 阅读器，好评如潮。设置请参考 [Zotero（3）：平板与社交：再谈研究辅助工具Zotero兼配套APP](http://www.yangzhiping.com/tech/zotero3.html) 基本没有难度。

但是我稍微做了一些自己的调整。使用 Notability 之后，被其强大吸引，不仅可以批注 PDF，其笔记功能也十分强大，因此，打算用它做笔记，就不局限在 zotero 的文档。在之前的设置中 Dropbox 云端建立了 zotero 文件夹，不想把其他的杂乱东西也同步上去，因此在设置 Notability 自动同步到 Dropbox 的时候仅选择了 Notability 中的一个主题。具体方法是现在 Notability 建立一个 note 主题，然后设置同步的时候，「目标位置」选择 /zotero/, 备份主题选择 note，如下图：

![](http://wx4.sinaimg.cn/large/6a959c93ly1fmlai6kh0tj20u0140q84.jpg)

其它的主题我打算同步到 Google Drive，这也是前两篇文章存在的原因。

### 插件安装

1. zotfile 

  zotero/storage 目录导出的文档是下面（图一）这样的，比较凌乱，因此需要用 zotfile 插件方便在 iPad 上找到文档，使用 zotfile 后的呈现（图二）
  
  ![](http://wx2.sinaimg.cn/large/6a959c93ly1fmlaierrlcj216i0hgtgx.jpg)

  （图一）
  
  ![](http://wx4.sinaimg.cn/large/6a959c93ly1fmlaiftuxlj217s0iqgt7.jpg)
  
  （图二）

  参考 [Zotero（4）：Zotero之Zotfile插件的使用 ](http://www.yangzhiping.com/tech/zotero4.html) 进行设置。

  基本思路是导入到 Zotero 的 PDF 文档使用 「Manage Attachments」选项（安装 zotfile 才有），可以 「Rename Attachments」，然后将其发送到 iPad 「Send to Tablet」，在 iPad 上阅读批注之后，还能导回来「Get from Tablet」。

  在这个过程中我遇到过一个错误报告，复述如下：

  > Zotfile: Renamed Attachments
  Attachments skipped because they are top-level items, snapshots or the file does not exist.
  
  Google 了很多英文文档都没能解决问题，结果一个知乎解决了。抱歉我暂时找不到这篇文章了，简单说一下，就是我保存的 PDF 不是附件的形式，因此 Zotfile 找不到。解决的办法是右键点击 PDF 文档 --> Retrieve Metadata for PDF（检索 PDF 元数据）。

  ![](http://wx2.sinaimg.cn/large/6a959c93ly1fmlaig3w5fj21840rannv.jpg)

  之后 按照阳老师文章中的方法，Zotfile 就起作用了。具体操作参考官方文档： [ZotFile - Advanced PDF management for Zotero](http://zotfile.com/index.html#changelog)
  
2. papermachine
  
  这个插件可以对一个类别论文进行「文献可视化」分析，下载安装基本没有难度，但是我并没有实现可视化词云，也许是我的 Zotero 还没有那么多文档的缘故，过一段时间在看一下。
  
  下载地址：[Paper Machines](http://papermachines.org/install/)
  
3. Markdown here

  用 Markdown 在 Zotero 里做笔记用的，参考 [Zotero（5）：电子文献管理攻略 ](http://www.yangzhiping.com/tech/zotero5.html) 问题 6
  

到此，Zotero 基础设置完成，用了大概 48 小时的探索，时间跨度一周。接下来，开启神奇之旅……

2017-12-18 10: 02

参考文档

* [Zotero（1）：文献管理软件Zotero基础及进阶示范 - 阳志平的网志](http://www.yangzhiping.com/tech/zotero1.html)
* [Zotero（2）：作为知识管理工具的Zotero - 阳志平的网志](http://www.yangzhiping.com/tech/zotero2.html)
* [Zotero（3）：平板与社交：再谈研究辅助工具Zotero兼配套APP - 阳志平的网志](http://www.yangzhiping.com/tech/zotero3.html)
* [Zotero（4）：Zotero之Zotfile插件的使用 - 阳志平的网志](http://www.yangzhiping.com/tech/zotero4.html)
* [Zotero（5）：电子文献管理攻略 - 阳志平的网志](http://www.yangzhiping.com/tech/zotero5.html)
