---
layout: post
title: 观察者模式
categories: DesignPattern
description: 学习《Head First 设计模式》第二部分《观察者模式》的笔记。
keywords: 设计模式，观察者模式
---

**如下内容是学习《Head First 设计模式》第二部分《观察者模式》所得，主要就是一些原文的摘抄和少量自己的总结。**

### 观察者模式定义

> 定义了对象之间的一对多依赖，这样一来，当一个对象改变状态时，它的所有依赖者都会收到通知并自动更新。

### OO 原则

1. 为交互对象之间的松耦合设计而努力。

### 吐槽

作者直接使用 Java 标准库里的 Observer 和 Observable 等东东来讲，虽然阅读起来无障碍……但是。好吧，也没啥好但是的。

### 书中示例的 Java 实现源码

[观察者模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/observe)

### 书中示例的类图

