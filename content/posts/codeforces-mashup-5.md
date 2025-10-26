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
基本上和官解差不多，主動尋找 $\\mathrm{MEX} = i$ 的最大左界和最小右界，若存在就把答案加上  
$($ 最大左界 $-$ 最小左界 $+1)$ $\\times$ $($ 最大右界 $-$ 最小右界 $+1)$ ， 接著 $\\mathrm{MEX} = i + 1$ 的最大左界和最小右界可以從 $\\mathrm{MEX} = i$ 的 $O(1)$ 更新，細節請參考 code 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1793/submission/339199649)

## CF 1334D
### Description
[Link](https://codeforces.com/contest/1334/problem/D)

### Solution
$n$ 個點最小字典序的 cycle 為 $1, 2, 1, 3, \\dots, 1, n, 2, 3, 2, 4,\\dots, 2, n, \\dots, n-1, n,1$ ，剩下實作應該不難。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1334/submission/343292234)
