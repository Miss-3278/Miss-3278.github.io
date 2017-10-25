---
title: git & github & SSH
description: 使用 SSH 连接 GitHub 仓库，并使用 Git 命令操作仓库
date: 2017-10-25
categories:
 - git
tags: [git]
---

> 来不及解释了，先动起来再说！

作为一个只会简单操作计算机，而对计算机世界一无所知的文科妹子，在学习过程中全是术语、反常识和一推牛人的名字，各种加一起，就是一个大写的「懵」。然而，值得庆幸的是，不懂并不代表不能完成作业，「笨方法」告诉我们，看不懂也别放弃，完成最小动作，步步为营。这篇文章记录操作过程，不解释为什么，希望能够给和我情况相同小伙伴来参考。就是这样的简单粗暴，仍然脑袋大的同学，可以跳过前面，直接看 **三、具体步骤**，先有小成就，再来深入学习思考。

## 一、 目标

使用 SSH 连接 GitHub 仓库，并使用 Git 命令操作仓库，至少包括 pull / push / commit / add / merge 5 个命令。

## 二、目标分析

### （一）术语简述

1. git 是一个版本控制系统，用他来管理你的文件版次，你将尽情地修改你的文件并且可以随时找回任何你提交过的版本，而你的文档还是那个文档。就好比写一本书，你反复推敲，改了好几个版本，git 系统将每个版本存了一个相册，当你的想要哪个版本的时候，用大脑指向那个相册，神奇的地方来了，相册动起来，把你要的版本内容呈现在你面前，还能对比差异，记录更改的时间……（这个过程像是在变魔术，哈哈~）
2. GitHub 有一个 Repositories, 这个东西叫做仓库，你电脑里的文件上传到 GitHub 仓库里，能够实现远程操作。我觉得有点儿像云盘操作，将文件从家里的电脑上传到云盘，到了办公室再从云盘下载到工作的电脑，只不过，用 git 可以控制版本，这个非常棒。
3. 要用 git 传文件到 GitHub 仓库（Repo），需要一个 SSH key，像一个密码，用户名，密码啥的都对上了，才能创建成功。

### （二）完成步骤

1. 有一个文件夹，里面是你要上传到 GitHub 的文件，比如我们的作业，我命名为 learnPython3。
2. 给 learnPython3 创建版本仓库，能够用 git 系统进行版本控制。
3. 在 learnPython3 目录中创建一个文件，将其加入 git 仓库。这里用到两组命令 git add <file> 和 git commit -m"<内容描述>" 。
3. 生成一个 SSH key, 用作上传 GItHub 仓库的密码。
4. 添加 GitHub 远程仓库。这里用到 git push 命令。
5. 然后用 git 命令把本地文件夹和远程仓库对接，并将本地文件推送到远程仓库。

## 三、具体步骤

#### 1. 创建一个文件夹 learnPython3

    
        $ mkdir learnPython3
        $ pwd
        /Users/***/Python
        $ cd learnPython3
        $ ls
   
        
#### 2. 初始化 git 仓库

   
        $ git init
        
        Initialized empty Git repository in /Users/***/Python/learnPython3/.git/
        $ ls -ah
        .	..	.git
   

#### 3. 我写了一个 ex1.py 的文件在 learnPython 目录中

  
        $ ls
        ex1.py
    

#### 4. 向 git 仓库提交这个文件

    
        $ git add ex1.py
        $ git commit -m"wrote a ex1.py file"
        [master (root-commit) 2b9f00f] wrote a ex1.py file
        1 file changed, 7 insertions(+)
        create mode 100644 ex1.py
    
        
#### 5. 创建 SSH key

（1）查看你有没有 SSH 目录。

    
      $ cd ~/.ssh 
      -bash: cd: /Users/***/.ssh: No such file or directory
    

   我的电脑上没有。
 
 （2）用命令创建 SSH。
 
    
      $ ssh-keygen -t rsa -c "youremail@exmaple.com"
    

   等待一下，会出现好几行英文字母。
   
 （3）检查创建 SSH 是否成功
   
    
      $ cd ~/.ssh
    

   此时，没有消息就是好消息，说明创建成功。列出该目录下的内容
   
    
      $ ls
      id_rsa		id_rsa.pub 
    

   id_rsa 是私钥，不可泄露；id_rsa.pub 是公钥，可以公开。
   
  （4）登录 GitHub，点你头像的下拉菜单，选择 Settings --> SSH & GPG keys --> New SSH key --> 将 id_rsa.pub 文件粘贴到 key --> Add SSH key，Title 自己取个名字。步骤图如下：
  
  ![](http://wx1.sinaimg.cn/large/6a959c93ly1fi1zbvacsqj21941crkdl.jpg)
  
  
  补充一下，.ssh 目录是隐藏的，要把 id_rsa.pub 文件全部粘贴到 GItHub 中，我用 cat 命令。
  
    
     $ cat ~/.ssh/id_rsa.pub
    
     
  然后，将输入的文件复制，粘贴到 GItHub 中，图片里 4 的位置。
  
  
#### 6. 添加 GitHub 远程仓库
 
 
（1） 登录 GitHub，点击右侧头像旁边的 + 号的下拉菜单 --> New Repository --> 填写Repository name(仓库名称) --> Creat repostiory, 创建一个新的仓库。步骤图如下：
 
 ![](http://wx3.sinaimg.cn/large/6a959c93ly1fi20iui93ej219311i4ev.jpg)
 
 (2) 根据 GitHub 的提示，在终端的本仓库路径下，输入命令：
 
    
     $ git remote add origin git@github.com: Miss-3278（换成你的 GitHub 用户名）/learnPython3.git
   

 （3）把本地库中的所有内容推送到远程库上，输入命令：
 
   
     $ git push -u origin master


 等待一小会儿，出来一推代码。然后登录 GitHub，查看该仓库，和本地的一模一样，推送成功。
 
 
## 四、这个过程中你可能遇到的小问题

### （一） 第一次添加文件到 git 仓库，会有提示设置用户名和邮箱

提示如下：
 
      Committer: 
      Your name and email address were configured automatically based
      on your username and hostname. Please check that they are accurate.
      You can suppress this message by setting them explicitly. Run the
      following command and follow the instructions in your editor to edit
      your configuration file:

      git config --global --edit

      After doing this, you may fix the identity used for this commit with:

      git commit --amend --reset-author
   

直接按照命令行的提示符直接设置就可以了，终端输入：

    
      $ git config --global user.name lixun
      $ git config --global user.name email@exmpal.com
    

查看设置的用户名和邮箱，终端输入：
      
      $ cat ~/.gitconfig | head -3

详细内容参见网页：[在 Git 中设置你的用户名](https://translate.google.com/translate?depth=1&hl=zhCN&prev=search&rurl=translate.google.com.hk&sl=en&sp=nmt4&u=https://help.github.com/articles/setting-your-username-in-git/)



***      

 附：参考资料
 
 4. 关于理解 Git & GitHub 的一篇故事型文章（带插图）：[大白话解释 Git 和 GitHub - 伯乐在线](http://blog.jobbole.com/111187/)
 1. 官方 Book：[Git - Book](https://git-scm.com/book/zh/v2)
 2. 容易上手的 git 操作教程：[Git开发中文手册 - 廖雪峰 - 极客学院Wiki](http://wiki.jikexueyuan.com/project/git-tutorial/)
 3. 有版本控制历史和 git 详细无比的教程：[Git权威指南 — GotGit](http://www.worldhello.net/gotgit/index.html) 这个教程写的比较早，篇幅也很巨大，根据需要使用。
 4. git 简明教程：[git - the simple guide - no deep shit!](http://rogerdudler.github.io/git-guide/index.zh.html)
 5. 看图了解 git 工作原理，对比文字，促进理解：[图解Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
 6. [Git远程操作详解 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)
 5. SSH 原理科普：[SSH原理与运用（一）：远程登录 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)
 
 
 
 
 
  
  
  
   
      



