---
layout: post
title: 命令模式
categories: DesignPattern
description: 学习《Head First 设计模式》第六部分《命令模式》的笔记。
keywords: 设计模式，命令模式
---

**如下内容是学习《Head First 设计模式》第六部分《命令模式》所得，主要就是一些原文的摘抄和少量自己的总结。**

## 命令模式定义
将“请求”封装成对象，从而使你可用不同的请求对客户进行参数化。支持撤销操作。（用途）常用于队列请求或日志请求。

## 模式使用场景
1.系统需要将请求调用者和请求接收者解耦，使调用者和接收者不直接交互。
2.系统需要在不同的时间指定请求，将请求排队和执行请求。
3.系统需要支持命令的撤销（Undo）操作和恢复（Redo）操作。
4.系统需要将一组操作组合在一起，即支持宏命令。

## 类图表示
<img src="/images/posts/designpattern/CommandPattern.png" width="80%" alt="Command  Pattern UML Class Diagram"/>

### 角色说明
* 命令角色（Command）：定义命令接口，声明具体命令类需要执行的方法。是抽象角色，通常为接口。
* 具体命令角色（ConcreteCommand）：命令接口的具体实现对象，通常会持有接收者，并调用接收者的方法来完成命令要执行的操作。
* 调用者角色（Invoker）：负责调用命令对象执行请求，通常会持有命令对象（可以持有多个命令对象）。Invoker是Client真正出发命令并要求命令执行相应操作的地方（使用命令对象的入口）
* 接收者角色（Receiver）：是真正执行命令的对象。任何类都可能成为一个接收者，只要它能实现命令要求实现的相应功能。
* 客户角色（Client）：可以创建具体的命令对象，并设置命令对象的接收者。此处的Client，可以理解为一个装配者，是一个组装命令对象和接收者对象的角色。


### 书中示例的 Java 实现源码
[命令模式实现](https://github.com/qihouying/design-pattern/tree/master/src/main/java/com/design/pattern/command)
