---
layout: post
title: mac下vim中文乱码及ssh远程中文乱码解决方法
categories: vim
description: mac终端本地文件的中文显示和输入都没有问题，但是在使用vim和ssh远程的时候碰到了中文乱码，记录下解决方法
keywords: mac vim乱码, mac乱码, vim乱码
---

### 问题一：vim乱码

> 解决方法：

> vi ~/.vimc

> 在文件中添加

> let &termencoding=&encoding

> set fileencodings=utf-8,gbk,utf-16,big5

### 问题二：ssh远程乱码

> 在/etc/ssh_config~orig 文件中有这么一句：

> SendEnv LANG LC_*

> 
> 也就是说ssh命令会发送本地语言环境到目标机器。

> 那么解决办法来了：

> vi ~/.bash_profile

> 在文件中添加

> export LC_ALL="zh_CN.UTF-8"

> export LANG="zh_CN.UTF-8"

> 配置完毕，重启mac终端即可。

