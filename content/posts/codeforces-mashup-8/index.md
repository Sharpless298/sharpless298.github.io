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
首先令 $a_i \\coloneqq a_i - i \\quad \\text{for all } 1 \\le i \\le n$ ，此時詢問 $f(l,r) = k-\\displaystyle \\max_{l\\leq x \\leq r}(cnt_{a_x})$ ，其中 $cnt_x$ 為 $x$ 在 $[l,r]$ 出現的個數。

雙指標 + `set` 可以在 $O(n \\log n)$ 求出所有可能的詢問 $f(l,r)$ 。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2009/submission/365509161)

## CF 2002D1
### Description
[Link](https://codeforces.com/problemset/problem/2002/D1)

### Solution
以 $1$ 為根，按前序把點存下來，接著開一個陣列 $pos_i$ 記錄點 $i$ 出現在前序的位置。令 $up(i)$ 表示位置 $i$ 的父節點應該在 $p$ 的哪個位置上，且
\\(
    up(pos_i)=pos_{\\left\\lfloor \\frac{i}{2}\\right\\rfloor} \\quad \\text{for all } 1\\leq i\\leq n
\\)
。

一個點 $p_i$ 在 $p$ 中會接上正確的父節點若且唯若 $p(up_i)=\\left\\lfloor\\frac{p_i}{2}\\right\\rfloor$，並且一個排列 $p$ 會是合法的 DFS 順序若且唯若所有的點都滿足 $p(up_i)=\\left\\lfloor\\frac{p_i}{2}\\right\\rfloor$ 。 $cnt$ 記錄目前有多少個點接上正確的父節點，每次詢問可以 $O(1)$ 更新，當 $cnt=n-1$ 表示合法。

時間複雜度 $O(n+q)$ 。

[AC Code](https://codeforces.com/contest/2002/submission/365624405)

## CF 2000F
### Description
[Link](https://codeforces.com/contest/2000/problem/F)

### Solution
令 $cost(i,j)$ 表示在第 $i$ 長方形上得到 $j$ 個 point 最少需要花費多少操作。

觀察發現每次先填滿長方形最短邊會最佳，因此可以在 $O(a_i b_i)$ 計算出 $cost(i,j)$ 。令 $dp(i)$ 表示得到 $i$ 點最少需要幾次操作，此時問題就變成經典的背包問題。

時間複雜度 $O(nk^2)$ 。

[AC Code](https://codeforces.com/contest/2000/submission/365657403)

## CF 1998C
### Description
[Link](https://codeforces.com/problemset/problem/1998/C)

### Solution
首先考慮 $k=0$ 情況，假設 $a$ 已經排序，此時 
$$\\displaystyle \\max_{i=1}^{n} \\left( a_i + \\operatorname{median}(c_i) \\right) = a_n+a_{\\lfloor\\frac{n}{2}\\rfloor}\\tag{1}$$


再考慮 $k\\neq0$ ，題目所求 $\\displaystyle \\max_{i=1}^{n} \\left( a_i + \\operatorname{median}(c_i) \\right)$ ，這給了我們兩種可能

1. 增加 $a_i$ ，
2. 增加 $\\operatorname{median}(c_i)$ 。

不難證明同時增加這兩項必定比只增加一項糟糕，因此可以分成兩種情況，答案取較大者。

#### Case 1
找到最大的 $i$ 滿足 $b_i=0$ ，令 $a_i\\coloneqq a_i+k$ ，排序 $a$ 後套用 $(1)$ 式計算。

#### Case 2
令 $f(x)$ 表示最少需要多少次操作使得 $a$ 中至少有$\\lfloor\\frac{n+1}{2}\\rfloor$ 個元素大於等於 $x$，$f(x)$ 是單調函數因此可以二分搜找到最大的 $x$ ，同樣排序 $a$ 後套用 $(1)$ 計算。

時間複雜度 $O(n\\log(n+A))$ 。

[AC Code](https://codeforces.com/contest/1998/submission/365739668)
