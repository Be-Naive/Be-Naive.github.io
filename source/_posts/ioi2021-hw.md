---
title: IOI2021集训队作业乱做
description: 即将鸽掉的东西
mathjax: true
date: 2022-02-22 21:07:07
updated: 2022-02-22 21:07:07
tags: 题解
---

### 大概两个周之后就会鸽了。。。看看鸽之前能做多少吧

## NEERC 17 K

[link](https://codeforces.com/gym/101630/problem/K)

### 题意

有一个序列 $\{a[i]\}$ ，满足 $\sum\limits_{j=1}^{i-1}a_j<a_i$ ， $\sum{a_i}<2^{64}$ ，以及一个奇数 $r$

现在给出序列 $\{b[i]\}$ ，其中 $b[i]=a[i]*r\ mod\ 2^{64}$ 

再给出一个整数 $s$ ，求一些 $b_i$ 使其和 mod $2^{64}$ 为 $s$

保证有解

$1\leq n \leq 64$ ， $1\leq b_i,r\leq 2^{64}$

### 题解

一种方法是 meet in the middle ，复杂度为 $O(2^{\frac{n}{2}})$

另一种方法是枚举 $a_1$ ，解出 $r$

由题意得 $a_i>2a_{i-1}$ ，因此 $a_1\leq2^{64-n}$

又因为 $2\nmid r$ ， $a_1$ 与 $b_1$ 的 lowbit 应当相同，设为 $k$

则只能解出 $mod\ 2^{64-k}$ 意义下的 $r$ ，还需要枚举前 $k$ 位

但 $2^k\mid a_1$ ，$a_1\leq 2^{64-n}$ ，因此枚举 $a_1$ 仅需枚举 $2^{64-n-k}$ 次，总复杂度仍为 $O(2^{64-n})$

解 $r$ 时直接推 $mod\ 2^k$ 意义下的逆元，不要用exgcd

以 $42$ 为阈值分治两种算法，即可通过此题

[code](https://codeforces.com/gym/101630/submission/147269919)

## WF2014 K

[link](https://codeforces.com/gym/101221/problem/K)

### 题意

给定一个大小为 $n$ 的环和 $k$ 条线段，使用最少的线段覆盖环。

$n,k\leq 10^6$

### 题解

直接倍增，令 $f[i][j]$ 为 $i$ 之前有线段覆盖的点能到达的最远点，注意一些 $\pm1$ 的细节

