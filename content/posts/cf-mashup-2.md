---
date: '2025-08-09T18:37:41+08:00'
draft: false
title: 'Codeforces Mashup 2'
math: true
---

## CF 2117E
### Description
[Link](https://codeforces.com/problemset/problem/2117/E)

### Solution
顯然先從陣列末端操作回來會最好，接著觀察發現刪除和不刪除的情況合在一起使得 index 為 $i$ 的陣列元素能被換成集合 $\\{a_{i+2},\\, a_{i+3}, \\, \\dots,\\, a_n,\\, b_{i+2},\\, b_{i+3},\\, \\dots ,\\,b_n\\}$ 內的任意元素，因此可以檢查 $a_i$ 或 $b_i$ 有沒有出現在集合裡，若沒有再檢查  
$a_i = b_i \\lor a_i = a_{i+1} \\lor b_i = b_{i+1}$ 是否為真，最後把 $a_{i+1}$ 和 $b_{i+1}$ 加進集合裡，找到最大的 $i$ 就是答案。

時間複雜度 $O(n)$。

我的 code 有點醜，看官解就好。

## CF 1917C
### Description
[Link](https://codeforces.com/contest/1917/problem/C)

有 $t$ 筆測資。

給一個長度為 $n$ 的數列 $a$ 和一個數列 $b$ ，在接下來的 $d$ 天中，假設當天為第 $i$ 天，你必須且只能選擇以下其中一個操作：
1. 把數列 $a$ 的前 $b_i$ 項加上 $1$ 。
2. 把分數加上滿足 $a_j = j$ 的個數，$1\\leq j \\leq n$，之後把數列 $a$ 的所有元素重置為 $0$ 。

分數初始值為 $0$ ，求分數的最大值。

由於 $d$ 可能非常大，數列 $b$ 以壓縮格式給出：

- 給定一個整數數列 \\( v_1, v_2, \dots, v_k \\)。
數列 $b$ 是將數列 $v$ 無限次重複拼接而成的：  
\\(b = [v_1, v_2, \dots, v_k, v_1, v_2, \dots, v_k, \dots]\\)

#### Constraints
- $1\\leq t \\leq 10^3$
- $1\\leq \\sum n \\leq 2000$
- $1\\leq \\sum k \\leq 10^5$
- $k \\leq d \\leq 10^9$
- $0 \\leq a_i \\leq n$
- $1 \\leq v_i \\leq n$

### Solution
先考慮當數列 $a$ 重置為 $0$ 的情況，觀察發現不管執行幾次操作一， $a_j = j$ 的個數只會 $\\leq 1$ ，因此只要操作一二一二這樣交替下去就會得到最大分數，假設有 $w$ 天則可以得到 $\\left\\lfloor \\frac{w}{2} \\right\\rfloor$ 的分數。

再考慮最初的數列 $a$ ，利用剛剛得出的結論，一個長度為 $n$ 的數列最多也只會貢獻 $n$ 的分數，因此最多連續執行操作一 $\\min(2n, d)$ 天，$n$ 夠小所以我們可以暴力枚舉。假設第 $i$ 第一次執行操作二 ，答案為 $\\max(cnt_i + \\left\\lfloor \\frac{n - i}{2} \\right\\rfloor)$，  
其中 $cnt_i$ 為 $a_j = j$ 的個數，$1\\leq i \\leq \\min(2n+1, d)$ 。

時間複雜度 $O(n ^ 2)$ 。

[AC Code](https://codeforces.com/contest/1917/submission/333519011)

## CF 1980E
### Description
[Link](https://codeforces.com/contest/1980/problem/E)

## CF 1671D
## CF 1899F
