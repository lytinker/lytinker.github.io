---
title: "【《游戏编程算法与技巧》读书笔记】第一章：游戏编程概述"
date: 2021-07-09 01:00:00
tags:
- 《游戏编程算法与技巧》
- 读书笔记
- 游戏编程
categories:
- [《游戏编程算法与技巧》]
- [读书笔记]
---

最近在读[《游戏编程算法与技巧》](https://book.douban.com/subject/26906838/) 这本书。开个新坑，在这里做一个读书笔记，把每一章的重点概念用尽可能简洁的篇幅总结归纳出来。需要提一句的是，这本书的中文版翻译质量相当糟糕，仅第一页就充斥着数不胜数的错译、漏译（参见我在豆瓣写的[这篇书评](https://book.douban.com/review/13662191/)）。所以建议有能力和有条件的读者直接读这本书的原版[《Game Programming Algorithms and Techniques》](https://book.douban.com/subject/25779461/)

本篇是全书第一章“游戏编程概述”的读书笔记，这一章主要关注游戏编程中的几个重要概念：

- 游戏循环
- 增量时间
- 游戏对象

<!-- more -->

## 游戏循环

**游戏循环**（Game Loop）是用于控制整个游戏程序的控制流。游戏循环的每次迭代被称为一**帧**（Frame），每一秒迭代的次数就被称为**帧率**（Frames Per Second，FPS）。

传统的游戏循环可以分为三个阶段：处理输入，更新游戏世界，生成输出。然而，大多数 3A 级主机游戏和 PC 游戏会采用多线程游戏循环。一种基本的多线程游戏循环技术是将图像渲染和游戏世界更新同步执行。为此，我们要让渲染线程比主线程慢一帧，即渲染线程绘制的实际上是主线程上一次更新的结果。这种做法的缺点是会导致**输入延迟**（Input Lag）。

## 游戏中的时间

**游戏时间**（Game Time）和**现实时间**（Real Time）并不总是一致的。在游戏中引入了**增量时间**（Delta Time）这一概念，即游戏从上一帧到这一帧之间所经历的时间，用来表示游戏中的时间流逝。如果一个游戏对象的属性变化需要持续一定时间，那么这种变化应当被处理成作用在增量时间上的函数。

虽然理论上可行，但在实际中以任意帧率运行游戏会导致一些问题。**限制帧率**（Frame Limiting）是解决这个问题最简单的方法，即要求游戏循环在经历一定的增量时间后才能继续。此时，如果某一帧所用的时间超过了给定的增量时间，最常见的解决方法是跳过随后一帧的渲染，以期跟上目标帧率，这种现象被称为**丢帧**（Dropping a Frame）。

## 游戏对象

**游戏对象**（Game Object）是指在游戏中每一帧都需要更新、或者绘制、或者同时需要更新和绘制的对象。游戏对象主要分为三种，第一种是既需要更新也需要绘制的对象，第二种是需要绘制但不需要更新的**静态对象**（Static Object），最后一种是需要更新但不需要被绘制的对象，例如摄像机（Camera）和触发器（Trigger）。

有多种用于表示游戏对象的方法，其中一种是通过面向对象方法中的**接口**（Interface）进行实现。

在实现了上述三种游戏对象之后，就可以很容易地在游戏中将它们组织起来。一种方法是使用两个列表，分别负责维护需要更新的对象和需要绘制的对象。在游戏循环中更新和绘制列表中的每个游戏对象。

## 总结

游戏循环决定了游戏中的对象在每一帧如何更新。游戏时间决定了游戏的运行速度，并保证了在不同机器上游戏体验的一致性。最后，设计良好的游戏对象能够简化游戏世界中所有对象的更新与渲染逻辑。这三者共同构成了实时游戏的核心部分。