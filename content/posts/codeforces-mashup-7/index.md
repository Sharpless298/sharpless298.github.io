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

觀察一告訴你這可以對答案二分搜。至於怎麼決定 $k$ 個回合能不能走到 $d$ 點？不難證明最好的方法是分成 $k-d+1$ 個連續步數走完，且盡可能平均分散。

時間複雜度 $O(t\\log d)$ 。

[AC Code](https://codeforces.com/contest/2149/submission/357920353)

## CF 2109D
### Description
[Link](https://codeforces.com/contest/2109/problem/D)

### Solution
用 BFS 計算以奇數和偶數步走到每一個點的最短步數，如果不可能則設為無限大。接著從題目給的集合找到最大可能奇數和偶數，判斷每個點需要的奇或偶步數有沒有小於等於最大可能奇數和偶數。

時間複雜度 $O(n + m + l)$ 。

[AC Code](https://codeforces.com/contest/2109/submission/360805417)
