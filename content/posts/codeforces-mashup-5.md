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
$n$ 個點最小字典序的 cycle 為 $1, 2, 1, 3, \\dots, 1, n, 2, 3, 2, 4,\\dots, 2, n, \\dots, n-1, n,1$ ，剩下實作應該不難。

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
最短路徑的變形，需要多開一個維度表示當前騎哪一台腳踏車，且當有一台腳踏車的 slow factor 比當前的低時，需要馬上換掉。

參考這個[comment](https://codeforces.com/blog/entry/123952?#comment-1116011) ，時間複雜度 $O((n^2+2nm)\\log{n^2})$ 。

[AC Code](https://codeforces.com/contest/1915/submission/347047425)
