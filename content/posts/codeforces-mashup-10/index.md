+++
date = '2026-03-19T17:33:13+08:00'
draft = false
title = 'Codeforces Mashup 10'
katex = true
+++

## CF 2051F
### Description
[Link](https://codeforces.com/contest/2051/problem/F)

### Solution
假設鬼牌可能會出現在位置 $k$ ，第 $i$ 個操作為 $a_i$ ，可以分成三種情況：

1. &nbsp;$k < a_i$ ， $k$ 可能變成 $k$ 或 $k+1$ 。
2. &nbsp;$k > a_i$ ， $k$ 可能變成 $k$ 或 $k-1$ 。
3. &nbsp;$k = a_i$ ， $k$ 會變成 $1$ 和 $n$ 。

觀察 1 和 2 可以得知可能的位置經過操作後會是連續的，可以用兩個變數 $[ml,mr]$ 表示。同理，當遇到第三種情況後，後續的操作最左端和最右端那兩塊也會是連續的
，用 $[1, l], [r, n]$ 表示。每次操作可以 $O(1)$ 更新 $l, ml, mr, r$ 這四個端點。

當第一個操作 $a_1$ 等於鬼牌的初始位置 $m$ 時需要特判，因為這樣會導致 $[ml,mr]$ 永遠為空。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2051/submission/367336214)
