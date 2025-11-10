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
1. 數列 $a$ 中必須恰好出現一個 $0$ 或 $n$ ，否則不存在 imbalanced array 。
2. $a_i=0 \\implies b_i < 0 \\land |b_i| = \\max\\limits_{1 \\leq j \\leq n} |b_j|$
3. $a_i=n \\implies b_i > 0 \\land |b_i| = \\max\\limits_{1 \\leq j \\leq n} |b_j|$

根據觀察2，可以發現填入這個 $b_i$ 不會影響所有 $b_i + b_j > 0$ 的個數；同理，根據觀察3，填入這個 $b_i$ 會使得所有包含自己的 $b_i + b_j > 0$ 的個數加一。這兩個其中一個填入後剩下的數列和原數列具備同樣的性質，我們只需要保證每次填入的
1. 負數都比前一次填入的負數大，
2. 正數都比前一次填入的正數小，

這樣當前填入的數才不會影響先前填入的數的 $b_i + b_j > 0$ 的個數。

由小到大排序數列 $a$ 後，令當前左端為 $l$ 右端為 $r$ ，從兩端向內開始填，假設當前填入的正數個數為 $cnt$ 。  
若 $a_l-cnt=0$ ，則 $b_l = -(r - l + 1)$ ；若 $a_r-cnt=(r-l+1)$ ，則 $b_r=(r-l+1)$ 。兩端沒有一端可以填的時候無解。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/1852/submission/347913779)

## CF 1805D
### Description
[Link](https://codeforces.com/contest/1805/problem/D)

### Solution
#### 觀察
- 一個點會自成一個 component 若且唯若它與其他點的最遠距離小於 $k$ 。
- 所有與其他點的最遠距離大於等於 $k$ 會在同一個 component 。

我們只需要計算每個點與其他點的距離就好，而一個點距離最遠的點一定在直徑兩端其中一點，因為如果最遠的點不在直徑上，就可以得出一條更長的直徑
。每個點與其他點的最遠距離可以在兩次 DFS 找直徑的時候順便計算，所以我的 Code 裡面 LCA 其實是多餘的。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/1805/submission/348066004)
