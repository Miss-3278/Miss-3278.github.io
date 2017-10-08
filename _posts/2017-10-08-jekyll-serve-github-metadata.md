---
title: 运行 jekyll serve 时，报错 GitHub Metadata 
description: Fixing the Jekyll + GitHub Metadata warning
date: 2017-10-08 
categories:
 - Jekyll
tags: [Jekyll]
---

### 问题描述

本地预览 Jekyll Github Pages，当运行 `jekyll serve` 命令时，出现报错信息为

```
GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.
```

### 修复过程

1. 创建个人 GitHub access token，参阅 [GitHub Documentation](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)。

   主要步骤：你的 GitHub 主页 --> 头像下拉菜单 --> Settings --> personal access tokens --> Generate new token --> 填好名称、选项之后点击 Generate token --> 复制你的 token

   ![](http://wx2.sinaimg.cn/large/6a959c93ly1fkap9l5nqrj21kw164n9b.jpg)

2. 添加新的环境变量，名字为 `JEKYLL_GITHUB_TOKEN`。 
   
   主要步骤：（提示：我的系统是 macOs Sierra Version 10.12.6）

   1）打开 ~/.bash_profile 。在终端输入 `nano ~/.bash_profile `。

   2）添加环境变量。输入 `export JEKYLL_GITHUB_TOKEN='123abc456eft'`(将 '123abc456eft' 换成刚才创建的一串字符)。按 `Ctrl+O` (字母 〇)保存，终端会提示是否保存修改以及保存的文件名，**回车确认即可**（取消按 `Ctrl+C`）。然后使用 `Ctrl+X` 快捷键组合退出编辑。

   ![](http://wx2.sinaimg.cn/large/6a959c93ly1fkap9e44ftj20v80jyqcu.jpg)

 3. 添加 OpenSSL 默认证书到环境变量

    添加完 `JEKYLL_GITHUB_TOKEN` 后，运行 `jekyll serve` 命令，出现一行报错如下：

    ```
     Error:  SSL_connect returned=1 errno=0 state=error: certificate verify failed
    ```

    因此，还要修复 OpenSSL default certificate error


    主要步骤：

    1）下载 `.pem` 文件。 [从这里 https://curl.haxx.se/ca/cacert.pem](https://curl.haxx.se/ca/cacert.pem)

    2) 使用 cp 命令，把文件复制到 `/usr/local/etc/openssl/certs/` 文件加下。

    `cp -r cacer.pem /usr/local/etc/openssl/certs/`

    3) 打开终端，输入 `nano ~/.bash_profile `。

    4）添加环境变量，输入 `export SSL_CERT_FILE=/usr/local/etc/openssl/certs/cacert.pem`。按 `Ctrl+O` (字母 〇)保存，终端会提示是否保存修改以及保存的文件名，**回车确认即可**（取消按 `Ctrl+C`）。然后使用 `Ctrl+X` 快捷键组合退出编辑。

以上完成后，重新运行 `jekyll serve` 查看是否成功。另外，可以将步骤2、步骤3一起配置。

### 参考文章

1. [Fixing the Jekyll + GitHub Metadata warning](https://mycyberuniverse.com/web/fixing-jekyll-github-metadata-warning.html)

2. [Fix the errors of GitHub Metadata and SSL certificate when running Jekyll serve - Hieu Le](https://www.hieule.info/programming/fix-errors-github-metadata-ssl-certificate-running-jekyll-serve)

3. [Jekyll with GitHub Pages - Fix the "GitHub Metadata No GitHub API authentication could be found" Error](http://knightcodes.com/miscellaneous/2016/09/13/fix-github-metadata-error.html)

4. [Problems with Ruby and OpenSSL on Mac OS X 10.10](https://spindance.com/problems-ruby-openssl-mac-os-x-10-10/)

5. [Mac OS X 系统的环境变量配置 - 简书](http://www.jianshu.com/p/1019ca95be50)



