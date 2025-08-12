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
$a_i = b_i \\lor a_i = a_{i+1} \\lor b_i = b_{i+1}$ 是否為真，找到最大的 $i$ 就是答案，沒找到就把 $a_{i+1}$ 和 $b_{i+1}$ 加進集合裡，。

時間複雜度 $O(n)$。

我的 code 有點醜就不放了，看官解就好。

## CF 1917C
### Description
[Link](https://codeforces.com/contest/1917/problem/C)

有 $t$ 筆測資。

給一個長度為 $n$ 的數列 $a$ 和一個數列 $b$ ，在接下來的 $d$ 天中，假設當天為第 $i$ 天，你必須且只能選擇以下其中一個操作：
<ol style="list-style-type: none; counter-reset: item;">
  <li style="counter-increment: item;">(1) 把數列 $a$ 的前 $b_i$ 項加上 $1$ 。
</li>
  <li style="counter-increment: item;">(2) 把分數加上滿足 $a_j = j$ 的個數，$1\leq j \leq n$，之後把數列 $a$ 的所有元素重置為 $0$ 。
</li>
</ol>

分數初始值為 $0$ ，求分數的最大值。

由於 $d$ 可能非常大，數列 $b$ 以壓縮格式給出：

- 給定一個整數數列 \\( v_1, v_2, \dots, v_k \\)。  
數列 $b$ 是將數列 $v$ 無限次重複拼接而成的：  \\(b = [v_1, v_2, \dots, v_k, v_1, v_2, \dots, v_k, \dots]\\)

#### Constraints
- $1\\leq t \\leq 10^3$
- $1\\leq \\sum n \\leq 2000$
- $1\\leq \\sum k \\leq 10^5$
- $k \\leq d \\leq 10^9$
- $0 \\leq a_i \\leq n$
- $1 \\leq v_i \\leq n$

### Solution
先考慮當數列 $a$ 重置為 $0$ 的情況，觀察發現不管選幾次 (1)， $a_j = j$ 的個數只會小於等於 $1$ ，因此只要 (1) (2) (1) (2) 這樣交替下去就會得到最大分數，假設有 $w$ 天則可以得到 $\\left\\lfloor \\frac{w}{2} \\right\\rfloor$ 的分數。

再考慮最初的數列 $a$ ，一個長度為 $n$ 的數列最多也只會貢獻 $n$ 的分數，再利用上面得出的結論，得出最多連續選 (1) $\\min(2n, d)$ 天，否則分數只會更小，$n$ 夠小所以我們可以暴力枚舉和更新數列 $a$ ，假設第 $i$ 天第一次選 (2) ，答案為 $\\max(cnt_i + \\left\\lfloor \\frac{n - i}{2} \\right\\rfloor)$，其中 $cnt_i$ 為第 $i$ 天 $a_j = j$ 的個數，$1\\leq i \\leq \\min(2n+1, d)$ ，$1\\leq j \\leq n$ 。

時間複雜度 $O(n ^ 2)$ 。

[AC Code](https://codeforces.com/contest/1917/submission/333519011)

## CF 1671D
### Description
[Link](https://codeforces.com/problemset/problem/1671/D)

### Solution
觀察到：
- $a^{\\prime}$ 的分數大於等於 $a$ 。
- 一段遞增或遞減的數列會比其他排列方式的分數小，且分數為首項減末項的絕對值。

根據觀察可以發現只需要關注 $1$ 和 $x$ 插在哪就好，因為當 $1$ 和 $x$ 插好後，我們一定可以把剩下的數找到某個遞增或遞減的區間插入。

先計算原數列的分數，再枚舉插入 $1$ 的位置，找到插入後增加的分數為最小的那個，頭尾的位置分別會多出 $\\lvert a_1 - 1 \\rvert$ 和 $\\lvert a_{n} - 1 \\rvert$ ，其他位置會多出 $2 \\cdot \\lvert a_i - 1\\rvert$ ；同樣地，當 $x$ 小於等於數列 $a$ 的最大值時不影響分數，否則就用和插入 $1$ 一樣的方式計算。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1671/submission/333668690)

## CF 1899F
### Solution
