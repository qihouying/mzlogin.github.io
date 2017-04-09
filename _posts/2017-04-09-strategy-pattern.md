---
layout: post
title: 策略模式
categories: DesignPattern
description: 学习《Head First 设计模式》第一部分《策略模式》的笔记。
keywords: 设计模式，策略模式
---

**如下内容是学习《Head First 设计模式》第一部分《策略模式》所得，主要就是一些原文的摘抄和少量自己的总结。**

## 策略模式定义
定义了算法族，将每个算法分别封装起来，让它们之间可以互相替换，此模式让算法的变化独立于使用算法的客户端。属于对象的行为模式。

## 00原则
* 封装变化。
* 多用组合，少用继承。
* 针对接口编程，不针对实现编程。

## 模式使用场景
 
1.如果在一个系统中有许多类，它们之间的区别仅在于它们的行为，则使用策略模式可以动态地让一个对象在许多行为中选择一种行为。

2.一个系统需要动态地在几种算法中选择一种。

3.如果一个对象有很多行为，若使用不当，则这些行只能使用多重条件选择语句来实现。

4.不希望客户端知道复杂的，与算法相关的数据结构，在具体策略类中封装算法和相关的数据结构，来提高算法的保密性与安全性。

## 类图表示
<img src="/images/posts/designpattern/StrategyPattern.png" width="80%" alt="Strategy Pattern UML Class Diagram"/>

### 角色说明
* 环境角色（Context）：持有一个Strategy的引用。
* 抽象策略角色（Strategy）：给出所有的具体策略类所需的接口。是抽象角色，通常为接口。
* 具体策略角色（ConcreteStrategy）：包装了相关的算法或行为。

### 书中示例
#### 示例类图表示如下
<img src="/images/posts/designpattern/StrategyPatternDuck.png" width="80%" alt="Strategy Pattern Duck UML Class Diagram"/>

#### java源代码实现
[策略模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/strategy)
