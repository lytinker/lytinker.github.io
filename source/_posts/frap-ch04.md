---
title: "[FRAP 小结] Chapter 04.Semantics via Interpreters"
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

## 4.1 代数表达式的语义

代数表达式 $e$ 的语义 $\left[\!\!\left[e\right]\!\!\right]$ 是一个作用在 **有限映射**(finite map) $v$ 上的递归函数. $\left[\!\!\left[e\right]\!\!\right]v$ 将 $v$ 映射到一个具体的值, 其中有限映射 $v$ 将表达式 $e$ 中的每个变量映射到该变量的值.

**变量置换函数** $[e'/x]$ 是一个作用在表达式 $e$ 上的函数. $[e'/x]e$ 将 $e$ 中所有的变量 $x$ 替换为 $e'$. 可以证明, 对任意的 $e, e', x, v$, 有

$$
\left[\!\!\left[ [e'/x]e \right]\!\!\right]v 
= \left[\!\!\left[ e \right]\!\!\right](v[x \mapsto \left[\!\!\left[ e' \right]\!\!\right]v])
\tag{定理 4.1}
\label{th_1}
$$

它表示翻译和置换是可以互换的. 等式左边表示对 $x$ 进行置换后进行翻译, 等式右边表示将 $x$ 的值直接映射至 $e'$ 的语义作用在 $v$ 上的结果后再进行翻译, 这两者最后会得到同样的结果.