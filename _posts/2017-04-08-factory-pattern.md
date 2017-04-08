---
layout: post
title: 工厂模式
categories: DesignPattern
description: 学习《Head First 设计模式》第四部分《工厂模式》的笔记。
keywords: 设计模式，工厂模式
---

**如下内容是学习《Head First 设计模式》第二部分《工厂模式》所得，主要就是一些原文的摘抄和少量自己的总结。**

## OO原则
依赖抽象，不要依赖具体类

## 工厂模式
定义了一个创建对象的接口，但由子类决定要实例化的类是哪一个。工厂方法让类把实例化推迟到子类。

## 抽象工厂方法
用于创建相关或依赖对象的家族，而不需要明确指定具体类。

## 工厂模式和抽象模式的区别
> 工厂模式：使用继承，把对象的创建委托给子类，子类实现工厂方法来创建对象。
> 抽象工厂模式：使用对象组合，对象的创建被是现在工厂接口所暴露出来的方法中。

## 工厂类图表示

<img src="/images/posts/designpattern/FacotryPattern.png" width="80%" alt="Factory  Pattern UML Class Diagram"/>

## 抽象工厂类图表示
<img src="/images/posts/designpattern/AbstractFacotryPattern.png" width="80%" alt="Abstract Factory  Pattern UML Class Diagram"/>

### 书中示例的 Java 实现源码
[工厂模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/facotry)

[抽象工厂模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/abstractFacotry)

