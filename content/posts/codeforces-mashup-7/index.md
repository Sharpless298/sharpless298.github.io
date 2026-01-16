+++
date = '2026-01-08T03:09:52+08:00'
draft = false
title = 'Codeforces Mashup 7'
katex = true
+++

## CF 2157E
### Description
[Link](https://codeforces.com/problemset/problem/2157/E)

### Solution

定義 $cnt_x$ 為數列 $a$ 中的 $x$ 的個數。

觀察發現 $i$ 從小到大，如果 $cnt_i > k$ ，則令 $cnt_{i+1} \\leftarrow cnt_{i+1}+cnt_i-1, \\quad cnt_i\\leftarrow 1$ 。  
他們的最終 $cnt$ 會和題目的原操作最終 $cnt$ 會一樣，因此只需要在不斷執行上面操作的時候找到最長連續 $cnt_i > k$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2157/submission/357057728)

## CF 2149F
### Description
[Link](https://codeforces.com/problemset/problem/2149/F)

### Solution
#### 觀察
- 當 $k$ 個回合能走到 $d$ 點時，$k+1$ 也可以；當 $k$ 個回合不能走到 $d$ 點時，$k-1$ 個回合也不能。
- 總共有 $k$ 個回合時，有 $k-d$ 個回合可以休息。

觀察一告訴你這可以對答案二分搜。怎麼決定 $k$ 個回合能不能走到 $d$ 點？不難證明最好的方法是分成 $k-d+1$ 個連續步數走完，且盡可能平均分散。

時間複雜度 $O(t\\log d)$ 。

[AC Code](https://codeforces.com/contest/2149/submission/357920353)

## CF 2148G
### Description
[Link](https://codeforces.com/contest/2148/problem/G)

### Solution
定義 $cnt_x$ 為前綴 $a$ 能被 $x$ 整除的個數。

令 $g=\\gcd(a_1, a_2, \\dots, a_k)$ ，要找到最大的 $k$ 滿足 $g>\\gcd(g, a_k+1)$，i.e.， 對於長度為 $k$ 的前綴 $a$ ，找到 $\\max\\{cnt_x | 1\\leq x\\leq n \\land cnt_x \\neq k\\}$ 。

時間複雜度 $O(n \\log n + n\\sqrt[3]{n})$ 。

[AC Code](https://codeforces.com/contest/2148/submission/358087403)
