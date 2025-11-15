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

根據觀察2，可以發現填入這個 $b_i$ 不會影響所有 $b_i + b_j > 0$ 的個數；根據觀察3，填入這個 $b_i$ 會使得所有包含自己的 $b_i + b_j > 0$ 的個數加一。這兩個其中一個填入後剩下的數列和原數列具備同樣的性質，我們只需要保證每次填入的
- 負數都比前一次填入的負數大，
- 正數都比前一次填入的正數小，

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
。每個點與其他點的最遠距離可以在兩次 DFS 找直徑的時候順便計算，我寫的時候沒發現所以多用了一個 LCA 。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/1805/submission/348066004)

## CF 1935D
### Description
[Link](https://codeforces.com/contest/1935/problem/D)

### Solution
正面算不好算，可以嘗試扣掉滿足 $x+y$ 和 $y-x$ 的 pair 再把重複的加回來，難點會是求重複的個數。把集合中所有 $x+y$ 和 $y-x$ 畫在二維平面上，不難發現重複的個數就是所有交點是整數點的個數，且只有當集合中兩點 $t_1,\\ t_2$ 的差值是偶數的時候交點才會是整數點，因此可以把集合分成奇偶兩個部份再用梯形公式把他們兩個加起來。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1935/submission/348635001)

## CF 1922E
### Description
[Link](https://codeforces.com/contest/1922/problem/E)

### Solution
先找到 $c \\in \\mathbb{N}$ 滿足 $2^c \\leq X < 2^{c+1}$ ，一個 $0, 1, 2, \\ldots, c-1$ 的數列會貢獻 $2^c$ 個遞增子序列，在這個數列左端嘗試插入一個數 $t\\in [0, c-1]$ ，它會貢獻 $2^{c-t-1}$ 個遞增子序列，注意到 $$0\\leq X-2^c < 2^c$$ ，我們只需要保證插入的數是遞減數列使得他們不會構成遞增子序列，$X-2^c$ 就可以由若干個 $2^{c-t-1}$ 組合出來，數列長度最長為 $2\\lg X$ ，當 $X=10^{18}$ 大約為 $120$ 。

時間複雜度 $O(t\\log X)$ 。

[AC Code](https://codeforces.com/contest/1922/problem/E)

## CF 1338B
### Description
[Link](https://codeforces.com/contest/1338/problem/B)

### Solution
分開解決最小值和最大值。

#### 最小值
***Claim: 最小值只會是 1 或 3 。***

最小值是 $1$ 應該蠻好想的，如果所有相異兩個葉子的簡單路徑所經過的邊數都是偶數，就可以把所有邊都填上一樣的數字；反之，最小值就是 $3$ ，我的構造方法和官解差不多，它講得也很清楚請自行參閱。

可以隨便挑一個點 DFS ，所有 leaf 深度 parity 都要一樣最小值才會是 $1$ 。

#### 最大值
如果有多個 leaf 連接到同一個點，那些 leaf 和那個點的邊權都要一樣，所以我們需要紀錄有哪些點已經有被 leaf 接過了，每有一個 leaf 接到已經被至少一個 leaf 接過的點答案就會少 $1$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1338/problem/B)
