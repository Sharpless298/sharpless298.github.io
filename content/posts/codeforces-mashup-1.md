---
date: '2025-08-02T05:18:41+08:00'
draft: false
title: 'Codeforces Mashup 1'
tags: ["Codeforces"]
math: true
---

## CF 2034D
### Description
[Link](https://codeforces.com/problemset/problem/2034/D)

有 $t$ 筆測資。

給一個長度 $n$ 的數列 $a$ 且 $a_i \in \\{0, 1, 2\\}$ ，你可以交換兩個差值為 $1$ 的數，求不超過 $n$ 次的交換方法使得它為遞增數列，題目保證至少出現一個 $1$ 。

#### Constraints
- $1\\leq t \\leq 3000$
- $1 \\leq \\sum n \\leq 2 \cdot 10^5$

### Solution
定義 $cnt_0,\ cnt_1,\ cnt_2$ 分別為 $0, 1, 2$ 的個數。

一個遞增數列的 $[0, cnt_0)$ 區間必定都是 $0$ ，先考慮把這個區間的數都換成 $0$ ，以下 $\\forall i \in [0, cnt_0)$。
- $a_i = 0$ : 不動作。
- $a_i = 1$ : 找最右邊 $0$ 交換。
- $a_i = 2$ : 先找最右邊的 $1$ 交換， 再找最右邊的 $0$ 交換。

最後再排序 $[cnt_0, n)$。

對於以下幾種情況：

1. 整個數列只有 $\\{0, 1\\}$ 或 $\\{1, 2\\}$，會交換 $\min(cnt_0, cnt_1)$ 或 $\min(cnt_1, cnt_2)$ 次。
2. 區間 $[0, cnt_0)$ 都是 $1$，會交換 $cnt_0$ 次，$[cnt_0, n)$ 會交換 $\min(cnt_1, cnt_2)$ 次，總共 $cnt_0 + \min(cnt_1, cnt_2)$ 次。
3. 區間 $[0, cnt_0)$ 都是 $2$，會交換 $2cnt_0$ 次，且除了第一次交換，每次都必定會有一個 $2$ 被交換至 $[cnt_0+cnt_1, n)$ 之間，因此 $[cnt_0, n)$ 會交換 $cnt_2-(cnt_0-1)$ 次，總共 $cnt_0 + cnt_2 + 1$ 次，題目保證 $cnt_1 \geq 1$，  
因此 $cnt_0 + cnt_2 + 1 \leq n$。
4. 顯然其他情況不會比 3. 更糟。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2034/submission/331907445)

## CF 1766D

### Description
[Link](https://codeforces.com/contest/1766/problem/D)

有 $n$ 筆詢問。

給定 $x, y \in \mathbb{N}$ ，找到最大的 $k$ 使得 $(x,y),\\,(x+1,y+1),\\,\\dots ,\\,(x+k-1, y+k-1)$ 皆為互質，  
若 $k$ 為 $\infty$ 則輸出 $-1$ 。

#### Constraints
- $1\\leq n \\leq 10^6$
- $1\\leq x < y \\leq 10^7$

### Solution
觀察一下不難發現：
- $x=y \\Rightarrow k = 0$
- $x=y-1 \\Rightarrow k = \infty$

對於 $x < y - 1$ 的情況，我們先將數對 $(x,y)$ 兩邊減去 $x$ 變成 $(0, y-x)$ ，此時問題變成：<div style="text-align: center; font-size: 15px;"><strong>找到一個最小的正整數 $\bm{z \geq x}$ 使得 $\bm{\gcd(z, y-x+z) \neq 1}$</strong></div>

假設 $y-x$ 有 $c$ 個相異質因數 $p_i$ ，$i \in [1, c]$
$$y-x = p_1 p_2 \dots p_c$$

觀察可發現 $\\gcd(z, y-x+z) \neq 1 \\Rightarrow$ $(y-x)$ 至少有一個質因數整除 $z$，因此對於每一個 $(y-x)$ 的質因數 ，皆存在一個最小的正整數 $m_i$ 使得 $p_i m_i \geq x$ ，找到最小的 $p_i m_i - x$ 就是答案。

令 $N$ 為 $(y - x)$ 的最大值，利用線性篩可以紀錄最小質因數達到 $O(\log N)$ 分解質因數，時間複雜度 $O(n \log N)$ 。

[AC Code](https://codeforces.com/contest/1766/submission/332299877)

## CF 1857F
### Description
[Link](https://codeforces.com/problemset/problem/1857/F)

### Solution
$$
\\begin{align}
a_i + a_j = x \\\\
a_i \\cdot a_j = y
\\end{align}
$$
由 $(1)$ 得 $a_j = x - a_i$ 代入 $(2)$
$$
\\begin{aligned}
&{a_j}^2-xa_i+y=0 \\\\[0.6em]
\\Rightarrow\\,&a_j = \\frac{x \\pm \\sqrt{x^2-4y}}{2} \\\\
\\Rightarrow\\,&a_i = x - a_j
\\end{aligned}
$$

$a_i$, $a_j$有解的話要符合：
- $x^2-4y \\geq 0$ 且為完全平方數
- $x \\pm \\sqrt{x^2-4y}$ 是偶數

當 $a_i \neq a_j$ ，答案為 $a_i$ 和 $a_j$ 個數相乘；當 $a_i = a_j$ ，假設個數為 $k$ ，答案為 $\\binom{k}{2}$ 。

時間複雜度 $O(q \\log n)$。

[AC Code](https://codeforces.com/contest/1857/submission/332627790)

## CF 1680C
### Description
[Link](https://codeforces.com/problemset/problem/1680/C)

### Solution
定義 $p_0$ 和 $p_1$ 為 $0$ 和 $1$ 的個數前綴和，以下都是左閉右開區間。

使用雙指標，$[l, r)$ 表示沒被刪除的區間，對於每一個 $l$ 只要滿足 $p_0(r)-p_0(l) < p_1(l)+p_1(n)-p_1(r)$ ，就不斷右移 $r$ ，答案為 $\\max(p_0(r)-p_0(l),\\, p_1(l)+p_1(n)-p_1(r))$ 的最小值。

時間複雜度 $O(n)$。

[AC Code](https://codeforces.com/contest/1680/submission/332749464)

## CF 1843E
### Description
[Link](https://codeforces.com/problemset/problem/1843/E)

有 $t$ 筆測資。

有一個長度 $n$ 且全為 $0$ 的數列 $a$，給你 $m$ 個區間 $(l_i, r_i)$， $1 \\leq i \\leq m$ ， $1 \\leq l_i \\leq r_i \\leq n$ ，有 $q$ 筆有序修改 $x_j$，  
修改 $a_{x_j}$ 為 $1$ ， $1\\leq j \\leq q$ ， $1 \\leq x_j \\leq n$，求至少要前幾項修改才能滿足至少有一個區間的 $1$ 的個數嚴格大於 $0$ 的個數，無解輸出 $-1$ 。

#### Constraints
- $1 \\leq t \\leq 10^4$
- $1 \\leq \\sum n \\leq 10^5$
- $1 \\leq m \\leq n \\leq 10^5$
- $1 \\leq q \\leq n$

### Solution
定義 $cnt_0$ 和 $cnt_1$ 為 $0$ 和 $1$ 的個數。

觀察到若前 $k$ 項滿足 $cnt_1 > cnt_0$ 時， 前 $k + 1$ 項也會滿足；相反地，若前 $k$ 項不滿足 $cnt_1 > cnt_0$ 時，前 $k - 1$ 項也會不滿足。  
因此我們可以對 $k$ 二分搜，每次 $O(n)$ 修改並計算 $1$ 的前綴和，接著 $O(m)$ 檢查每個區間有沒有滿足。

時間複雜度 $O((n+m)\\log q)$ 。

[AC Code](https://codeforces.com/contest/1843/submission/332966958)
