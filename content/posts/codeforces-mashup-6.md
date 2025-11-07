+++
date = '2025-11-08T01:21:04+08:00'
draft = false
title = 'Codeforces Mashup 6'
katex = true
+++

## CF 1852B
### Description
[Link](https://codeforces.com/contest/1852/problem/B)

### Solution
#### 觀察
- 數列 $a$ 中必須恰好出現一個 $0$ 或 $n$ ，否則不存在 imbalanced array 。
- $a_i=0 \\implies b_i = \\min(b)$
- $a_i=n \\implies b_i = \\max(b)$

根據觀察可以發現填入最小的負數不會影響所有 $b_i + b_j > 0$ 的個數，填入最大的正數會使得所有包含自己的  
$b_i + b_j > 0$ 個數加一，這兩個其中一個填入後剩下的數列和原數列具備同樣的性質，因此可以用同樣的方法再繼續填下去。

由小到大排序數列 $a$ 後，令當前左端為 $l$ 右端為 $r$ ，從兩端向內開始填，假設當前填入的正數個數為 $cnt$ 。  
若 $a_l-cnt=0$ ，則 $b_l = -(r - l + 1)$ ；若 $a_r-cnt=(r-l+1)$ ，則 $b_r=(r-l+1)$ 。兩端沒有一端可以填的時候無解。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/1852/submission/347913779)
