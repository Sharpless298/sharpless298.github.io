+++
date = '2026-03-04T21:19:41+08:00'
draft = false
title = 'Codeforces Mashup 8'
katex = true
+++

## CF 2022D1
### Description
[Link](https://codeforces.com/problemset/problem/2022/D1)

### Solution
只有當兩個玩家 $a, b$ 其中一人是 Imposter 時，$f(a,b)+f(b,a)$ 才會是 $1$ ，否則為 $0$ 或 $2$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2022/submission/365351008)

## CF 2009G1
### Description
[Link](https://codeforces.com/contest/2009/problem/G1)

### Solution
首先令 $a_i \\coloneqq a_i - i \\quad \\text{for } 1 \\le i \\le n$ ，此時詢問 $f(l,r) = k-\\displaystyle \\max_{l\\leq x \\leq r}(cnt_{a_x})$ ，其中 $cnt_x$ 為 $x$ 在 $[l,r]$ 出現的個數。

雙指標 + `set` 可以在 $O(n \\log n)$ 求出所有可能的詢問 $f(l,r)$ 。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2009/submission/365509161)
