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

## WF2019 B

[link](https://codeforces.com/gym/102511/problem/B)

### 题意

你要修一座拱桥。桥面的高度为 $h$ 。给定 $n$ 个地形坐标 $(x_1,y_1),(x_2,y_2),\dots,(x_n,y_n)$ ，将其相邻连接就是地面。

你需要修若干条柱子，只能在给定的点对应的横坐标处修，在第 $i$ 个点处修的柱子的高度为 $h−x——i$ 。第 $1$ 个和第 $n$ 个点处必须修柱子。

你还需要在修的柱子之间造拱，拱是一个半圆形，直径为两个柱子的距离，恰好和桥面相切。

拱不能和地面相交，可以相切。

假设你修了 $k$ 条柱子，高度为 $h_1,h_2,\dots,h_k$ ，修了 $k-1$ 个拱，直径为 $d_1,d_2,\dots,d_{k−1}$ 。

给定参数 $\alpha,\beta$ ，要求最小化代价： $\alpha*\sum\limits_{i=1}^k{h_i}+\beta*\sum\limits_{i=1}^{k-1}{(h_{i+1}-h_i)^2}$

无合法方案输出 `impossible` 。 $n\leq 10^4$ 。

### 题解

显然可以DP，需要做到 $O(1)$ 的判断一段区间内的点是否都在某个圆内。

设现在我们由 $f_i$ 向后转移，新的拱半径为 $r$ ，则新的拱圆心为 $(x_i+r,h-r)$。

这样一个点 $(x_j,y_j)$ 在圆内的条件为 $(x_j-x_i-r)^2+(y_j-h+r)^2\leq r^2$

整理得 $r^2-2(x_i-x_j+y_j-h)r+(x_i-x_j)^2+(y_j-h)^2\leq 0$

可以解得 $r_1\leq r\leq r_2$ 。

因为拱是一个半圆，所以当 $y_j\leq h-r_1$ 时只需要 $r\leq r2$ 。

枚举 $j$ 时维护 $r$ 的范围即可。

[code](https://codeforces.com/gym/102511/submission/147766018)

