---
date: '2025-08-15T00:10:22+08:00'
draft: false
title: 'Codeforces Mashup 3'
math: true
tags: ["Codeforces"]
---

## CF 2039D
### Description
[Link](https://codeforces.com/problemset/problem/2039/D)

### Solution
當 $i=1,\\; \\forall j \\in [2,n] :$
$$a_{\\gcd(1,j)}=a_1 \\neq \\gcd(a_1,a_j)$$
觀察得到
$$a_1 \\neq \\gcd(a_1,a_j) \\iff a_1 \\nmid a_j$$

先假設 $a_1$ 滿足 $a_1 \\nmid a_j$ ，繼續往下推。

當 $i=2,\\; \\forall j \\in [3,n] :$
\\[
a_{\\gcd(2,j)} = 
\\begin{cases} 
a_1 \\neq \\gcd(a_2, a_j), & j \\text{ is odd} \\\\
a_2 \\neq \\gcd(a_2, a_j), & j \\text{ is even}
\\end{cases}
\\]

- $j$ 是奇數：因為前面已經假設 $a_1$ 不會整除其他數，它自然也不會是其他兩數的最大公因數，所以這條式子成立。
- $j$ 是偶數：同樣可得 $a_2 \\neq \\gcd(a_2,a_j) \\iff a_2 \\nmid a_j$

到這邊可以推出我們要的結論了，$\\forall\\, i \\in [1,n],\\;\\forall\\, j \\in (i,n],\\;\\forall\\, k \\in [2,\\left\\lfloor \\frac{n}{i} \\right\\rfloor]$
$$a_i\\neq \\gcd(a_i,a_j) \\iff a_i \\nmid a_{ki}$$

怎麼滿足不整除的部份？其實很簡單，**一個數不能整除比他小的數**，又題目剛好要求字典序最大：
- $a_1=\\max(S)$
- 對於 $i\\geq 2$ ，令 \\(a_j = \\min \\{ a_k : k \\mid i,\\, k \\neq i \\}\\) ， 則 $a_i$ 等於在集合 $S$ 中比 $a_j$ 次小的數；若找不到則無解。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2039/submission/333991898)

## CF 2030D
### Description
[Link](https://codeforces.com/problemset/problem/2030/D)

## CF 1626C
### Description
[Link](https://codeforces.com/problemset/problem/1626/C)

## CF 2112D
### Description
[Link](https://codeforces.com/problemset/problem/2112/D)

## CF 1798C
### Description
[Link](https://codeforces.com/problemset/problem/1798/C)

