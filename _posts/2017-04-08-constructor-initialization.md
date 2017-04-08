---
layout: post
title: 构造器初始化
categories: thinking in java
description: 学习《Java编程思想》第五部分《初始化与清理》的笔记。
keywords: 构造器初始化
---

**如下内容是学习《Java编程思想》第五部分《初始化与清理》所得，主要就是一些原文的摘抄和少量自己的总结。**

## 构造器初始化
### 初始化顺序
> 类的内部，变量定义的先后顺序决定了初始化的顺序。
> 变量在任何方法（包括构造器）被调用之前得到初始化。


### 书中示例的 Java 实现源码
[单例模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/singleton)
