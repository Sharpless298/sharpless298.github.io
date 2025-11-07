+++
date = '2025-09-18T11:37:17+08:00'
draft = false
title = 'Codeforces Mashup 5'
katex = true
+++

## CF 1793D
### Description
[Link](https://codeforces.com/contest/1793/problem/D)

### Solution
主動尋找 $\\mathrm{MEX} = i$ 的最大左界和最小右界，若存在就把答案加上
$($ 最大左界 $-$ 最小左界 $+1)$ $\\times$ $($ 最大右界 $-$ 最小右界 $+1)$ ， 接著 $\\mathrm{MEX} = i + 1$ 的最大左界和最小右界可以從 $\\mathrm{MEX} = i$ 的 $O(1)$ 更新。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1793/submission/339199649)

## CF 1334D
### Description
[Link](https://codeforces.com/contest/1334/problem/D)

### Solution
$n$ 個點最小字典序的 cycle 為 $1, 2, 1, 3, \\dots, 1, n, 2, 3, 2, 4,\\dots, 2, n, \\dots, n-1, n,1$ ，檢查一下題目所求落在哪個部份就好。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1334/submission/343292234)

## CF 1326D2
### Description
[Link](https://codeforces.com/contest/1326/problem/D2)

### Solution
令 $l=0, r=n-1$ ，當 $s_l=s_r$ 時，不斷右移 $l$ 和左移 $r$ ，接著在子字串 $s_l, s_{l+1}, s_{l+2},\\dots,s_{r}$ 中找到最長前綴或後綴的回文字串，可以用 hash 或 Manacher 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1326/submission/346785509)

## CF 1915G
### Description
[Link](https://codeforces.com/contest/1915/problem/G)

### Solution
Dijkstra 的變形，需要多開一個維度表示當前騎哪一台腳踏車，且當有一台腳踏車的 slow factor 比當前的低時，需要馬上換掉。

參考這個[comment](https://codeforces.com/blog/entry/123952?#comment-1116011) ，時間複雜度 $O((n^2+2nm)\\log{n^2})$ 。

[AC Code](https://codeforces.com/contest/1915/submission/347047425)

## CF 1409E
### Description
[Link](https://codeforces.com/contest/1409/problem/E)

### Solution
$y$ 座標顯然不影響，可以忽略，再把 $x$ 座標全部排序一下，以下用 $x_i$ 表示第 $i$ 個 $x$ 座標。

兩個平台重疊的部份不好處理，先解決不重疊的情況。用雙指標把所有滿足 $x_r - x_l \\leq k$ 的 $[l, r]$ ，再加上 $[l,r]$ 包含點的個數包成 tuple 丟進 priority queue，接著同樣用雙指標由左往右枚舉每一個點當作第一個平台的開頭，從 priority queue 中取出包含最多點的 tuple
。若取出 tuple 的 $[l, r]$ 和第一個平台重疊，就 pop 掉繼續取，直到不重疊然後更新答案。

重疊的部份觀察可以發現可以直接把兩個平台相接頭尾相接，變成一個長度 $2k$ 的平台，再用雙指標計算一次就好。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/1409/submission/347847505)
