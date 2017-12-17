---
title: About macOs Google Drive Sign in Problem
description: 前一秒还阴云蔽日，下一秒便云开月现，技术的快乐也许就在于此。
date: 2017-12-17 16:59
categories: 
 - FQ
tags: [Privoxy, sock5, http, Google Drive]
---

这几天在设置 zotero，基本成功，在最后却遇到了 Google Drive 的登录问题，花了三个多小时，终于顺利登录使用，趁着热乎劲儿把过程记录下来，以备参考、学习。

![](http://wx3.sinaimg.cn/large/6a959c93ly1fmjvyv7t9gj20m80euqjm.jpg)

(图片来自一位开智学友)

## 错误诊断：Proxy （代理）

登录 Google Drive 出现的错误提示：

> There was a problem signing in.
    This cloud be due to your network connection, proxy, firewall, or antivurus software.Check your setting and try sign in again.

我迅速诊断为 Proxy 的问题， ss 科学上网用的是 socks5 代理，而 Google Drive 不支持 sock5，仅支持 http。其实这种登录问题在我安装 Dropbox 的时候已经遇到过，只不过 Dropbox 在登录时能够设置网络，将其设置为 sock5 代理，就顺利登录了，而 Google Drive 不行，它事先设置不了，只好解决 proxy 的问题了。

简单的思路就是将 sock5 代理转换为 http 代理，是用的工具是 [Privoxy ](http://www.privoxy.org/)。

## 解决过程

先浏览一下官方文档，然后参考网络各位大神的文档，我记录下具体的操作流程。

### step1 安装 Privoxy

我使用 Homebrew，因此使用 brew 命令。不使用这一工具的请自己参考官方文档安装。

```
brew install privoxy
```

### step2 修改 Privoxy config （配置文件）

```
sudo vim /usr/local/etc/privoxy/config
```

这个步骤尝试了几个命令，最后使用这个进入 config，使用 [Vim](http://pizn.github.io/2012/03/03/vim-commonly-used-command.html) 命令修改成功。

修改的地方为：

1. 修改 forward。找到 「# forward-socks5t   /               127.0.0.1:9050 .」一行，在这一行后另起一行追加如下内容：

```
#    forward           /                   127.0.0.1:1086 .
#    forward-socks4    /               127.0.0.1:1086 .
#    forward-socks4a   /               127.0.0.1:1086 .
#    forward-socks5    /                127.0.0.1:1086 .
#    forward-socks5t   /               127.0.0.1:1086 .
```
需要注意的地方：

* 1086 后面的 .（点）要加上
* 前面的 # （井号）要加上
* 至于后面的端口号是 1086 还是 1080 根据自己的情况填写。

2. （可忽略）修改 listen-address（监听地址）。找到「listen-address  127.0.0.1:8118」一行，修改为：

```
listen-address  192.168.1.1:8118
```
这是为了让Privoxy公开让局域网中的其它设备访问，如果只是本机访问请跳过。

### step3 检查是否设置成功

1. 启动 Privoxy，使用命令：

```
sudo /usr/local/sbin/privoxy /usr/local/etc/privoxy/config

```

2. 查看是否启动成功，使用命令：

```
ps aux | grep privoxy
```
返回类似下面的内容，说明启动成功。

```
root             19991   0.0  0.0  2451936   1220   ??  Ss    3:34PM   0:00.02 /usr/local/sbin/privoxy /usr/local/etc/privoxy/config
```

3. 查看端口监听是否成功，使用命令：

```
netstat -an | grep 8118
```
返回如下内容，说明监听成功：

```
tcp4       0      0  127.0.0.1.8118         *.*                    LISTEN    
```

### step4 应用设置

1. Chrome 下的 SwitchOmega 扩展，按照如下配置：


  ![](https://blog.phpgao.com/usr/uploads/2015/06/3978620669.png)


  （该图片来自 [老高的技术博客](https://blog.phpgao.com/privoxy-shadowsocks.html))

2. 在 ~/.bashrc （环境变量）中加入下面的代码

  ```
  export http_proxy=http://192.168.1.1:8118
  export https_proxy=http://192.168.1.1:8118
  ```

3. Privoxy 代理所有请求的设置

  在电脑中 System Preferences（系统设置）--> Network（网络）--> Advanced（高级）--> Proxies (代理) --> Secure Web Proxy(HTTPS)（安全网页代理）and Web Proxy(HTTP)（网页代理），见下图：

  ![](http://wx3.sinaimg.cn/large/6a959c93ly1fmjy5vuf8nj210m0v0q7t.jpg)

  当我以为还缺少什么的时候，Google Drive 瞬间登录。前一秒还阴云蔽日，下一秒便云开月现，技术的快乐也许就在于此。

  ![](http://wx3.sinaimg.cn/large/6a959c93ly1fmjy61pms0j218011ydpz.jpg)

说明：我是技术小白，我不知道在 step4 的每一个步骤是否必须，我只是在尝试，最后到一个步骤的时候发现神奇地登录了，请大牛勿喷，照顾一下小白辛苦三个多小时的扫脑煎熬，还有写这篇文章花了一个多小时的劳动成果。

参考文档：

* [Privoxy - Home Page](http://www.privoxy.org/)
* [Privoxy - Wikipedia](https://en.wikipedia.org/wiki/Privoxy)
* [Socks代理和http代理的区别 – Wrfly's blog – Think|Hack|Share](https://wrfly.kfd.me/SOCKS%E4%BB%A3%E7%90%86%E5%92%8CHTTP%E4%BB%A3%E7%90%86%E7%9A%84%E5%8C%BA%E5%88%AB/)
* [你是Socket，我是HTTP Proxy – 记录点滴生活](https://davidlovezoe.wordpress.com/2017/01/05/socket-http-proxy/)
* [使用Privoxy将socks5代理转为http代理 - 老高的技术博客](https://blog.phpgao.com/privoxy-shadowsocks.html)
* [Mac上Privoxy将shadowsocks的socks5代理转为http代理(解决SublimeText无法安装插件的问题) - CSDN博客](http://blog.csdn.net/yanzi1225627/article/details/51064306)
* [socks5代理转http代理 | linsage的博客](https://linsage.xyz/2017/06/13/%E6%8A%80%E6%9C%AF/Socks5%E4%BB%A3%E7%90%86%E8%BD%ACHttp%E4%BB%A3%E7%90%86/)
* [Mac上配置Privoxy - DeviLeo - 博客园](http://www.cnblogs.com/DeviLeo/p/6033591.html)
* [如何用 Privoxy 辅助翻墙？ @ 编程随想的博客](https://program-think.blogspot.com/2014/12/gfw-privoxy.html)
