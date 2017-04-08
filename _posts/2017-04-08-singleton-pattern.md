---
layout: post
title: 单例模式
categories: DesignPattern
description: 学习《Head First 设计模式》第五部分《单例模式》的笔记。
keywords: 设计模式，单例模式
---

**如下内容是学习《Head First 设计模式》第五部分《单例模式》所得，主要就是一些原文的摘抄和少量自己的总结。**

## 单例模式
确保一个类只有一个实例，并提供一个全局访问点。

## 几点说明
1. 单例模式中getInstance()方法是静态的，这意味着它是一个类方法，所以可以在代码的任何地方使用Singleton.getInstance()访问它，与全局变量一样简单，只多了一个优点：单例可以延迟实例化。

2. static方法内部不能调用非静态方法，反过来是可以的。

### 书中示例的 Java 实现源码
[单例模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/singleton)
