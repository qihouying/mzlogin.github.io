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

> 参考文章：https://www.vat58.com/mac%E4%B8%8Bvim%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81%E5%8F%8Assh%E8%BF%9C%E7%A8%8B%E4%B8%AD%E6%96%87%E4%B9%B1%E7%A0%81%E7%9A%84%E8%A7%A3%E5%86%B3%E6%96%B9%E6%B3%95/
