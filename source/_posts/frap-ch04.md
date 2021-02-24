---
title: "【FRAP 小结】Chapter 04.Semantics via Interpreters"
date: 2021-02-23 01:00:00
tags:
- FRAP
- 读书笔记
- Formal Verification
categories:
- [FRAP]
- [读书笔记]
---

这是 [*Formal Reasoning About Programs*](http://adam.chlipala.net/frap/) 第四章 *Semantics via Interpreters* 的章后小结。这一章主要关注程序的 **语义**(semantic)。

<!-- more -->

## 4.0 重要概念

* 什么是语义, 怎样定义语言的语义.
* 怎样证明作用在语言上的函数的正确性.
* 什么是编译, 怎样证明编译过程的正确性.
* 什么是优化, 怎样证明优化过程的正确性.

这一章通过代数表达式, 堆栈机和一个简单的高阶命令式语言三个例子来说明这几个概念.

## 4.1 代数表达式

代数表达式 $e$ 的语义 $\left[\!\!\left[ e \right]\!\!\right]$ 是一个作用在 **有限映射**(finite map) $v$ 上的递归函数. $\left[\!\!\left[ e \right]\!\!\right]v$ 将 $v$ 映射到一个具体的值, 其中有限映射 $v$ 将表达式 $e$ 中的每个变量映射到该变量的值.

**变量置换**(variable substitution) $[e'/x]$ 是一个作用在表达式 $e$ 上的函数. $[e'/x]e$ 将 $e$ 中所有的变量 $x$ 替换为 $e'$. 我们可以通过 **定理 4.1** 来证明变量置换函数的正确性. 这里的正确性指的是, 对 $x$ 进行置换和将 $x$ 的值直接映射至 $\left[\!\!\left[ e' \right]\!\!\right]v$, 两者是等价的.

## 4.2 堆栈机

**堆栈机**(stack machine)是由一组指令 $i$ 构成的序列 $\overline{i}$. $\left[\!\!\left[ \overline{i} \right]\!\!\right]$ 是作用在有限映射 $v$ 和堆栈 $s$ 上的函数, $\left[\!\!\left[ \overline{i} \right]\!\!\right] (v, s)$ 返回指令执行结束后的堆栈.

编译(compilation)是指将一种语言翻译成另一种语言的过程, 记做 $\lfloor \ldots \rfloor$. 我们用 $\lfloor e \rfloor$ 将代数表达式 $e$ 编译为堆栈机 $\overline{i}$. 可以通过 **定理 4.2** 和 **引理 4.3** 证明编译过程的正确性, 其中 **定理 4.2** 是 **引理 4.3** 的特殊情况. 这里的正确性指的是, 编译前后的两种语言在语义上是等价的.

## 4.3 一个简单的高级命令式语言

我们定义一个简单的命令式语言 $c$, $\left[\!\!\left[ c \right]\!\!\right]$ 作用在有限映射 $v$ 上并对 $v$ 进行操作.

**优化**(optimization)是指对一门语言进行变换, 且变换前后是同一种语言的过程, 记做 $\vert \ldots \vert$. 我们用 $\vert c \vert$ 对命令式语言 $c$ 进行 **循环展开**(loop unrolling) 的优化. 可以通过 **定理 4.4** 和 **引理 4.5** 证明优化过程的正确性. 这里的正确性指的是, 优化前后语言的语义保持不变.