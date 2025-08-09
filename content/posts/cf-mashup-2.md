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

## CF 1861C
### Description
[Link](https://codeforces.com/problemset/problem/1861/C)

## CF 1980E
## CF 1671D
## CF 1899F
