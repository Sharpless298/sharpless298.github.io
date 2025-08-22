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
a_1 \\neq \\gcd(a_2, a_j), & j \\text{ is odd.} \\\\
a_2 \\neq \\gcd(a_2, a_j), & j \\text{ is even.}
\\end{cases}
\\]

- 當 $j$ 是奇數：因為前面已經假設 $a_1$ 不會整除其他數，它自然也不會是其他兩數的最大公因數，所以這條式子成立。
- 當 $j$ 是偶數：同樣可得 $a_2 \\neq \\gcd(a_2,a_j) \\iff a_2 \\nmid a_j$

接著再假設 $a_2 \\nmid a_j$ ，推 $i=3,\\;\\forall j \\in [4,n]$ 的情況，這樣不斷推下去可以得到一個結論：
$$\\forall\\, i \\in [1,n],\\;\\forall\\, j \\in (i,n],\\;\\forall\\, k \\in [2,\\left\\lfloor \\frac{n}{i} \\right\\rfloor] \\quad
a_i\\neq \\gcd(a_i,a_j) \\iff a_i \\nmid a_{ki}$$

令題目給定的集合 $S = \\{ s_1, s_2, \\dots, s_m \\}, \\quad s_1 < s_2 < \\cdots < s_m$

結論有了，怎麼構造？其實很簡單，**一個數不能整除比他小的數**，題目又剛好要求字典序最大，因此考慮以下構造方式：
- $a_1=s_m$
- 對於 $i \\geq 2$ ，設 \\(a_j = \\min \\{ a_k : k \\mid i,\\, k \\neq i \\}\\) ，若 $a_j$ 為 $s_t$， 則令 $a_i$ 為 $s_{t-1}$；若 $t=1$ 則無解。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2039/submission/333991898)

## CF 2112D
### Description
[Link](https://codeforces.com/problemset/problem/2112/D)

### Solution
#### 觀察
- $n = 2$ 無解
- $u \\rightarrow v \\rightarrow w$ 有 $3$ 個 good pair
- $v_1\\rightarrow v_2 \\leftarrow v_3 \\rightarrow \\dots \\leftarrow v_k$ 有 $k-1$ 個 good pair


找到一個度數為 $2$ 的節點 $v$ ，假設 $v$ 相鄰的節點為 $v, w$ ，就像觀察二一樣構造 $u \\rightarrow v \\rightarrow w$ ，剩下的點就像觀察三一樣接上去就好，參考下圖
{{< figure align=center src="graph.png" width="300">}}  

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2112/submission/334600976)

## CF 1975D
### Description
[Link](https://codeforces.com/contest/1975/problem/D)

### Solution
先找到最先被染色成藍色的點，假設為 $v$ 且所有的點中與 $v$ 的最遠距離為 $d$ ，答案為 $dis(b, v) + 2(n-1) - d$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1975/problem/D)
