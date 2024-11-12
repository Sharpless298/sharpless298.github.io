+++
title = 'DP 練習'
date = 2024-09-18T00:53:31+08:00
draft = false
math = true
tags = ["DP"]
+++

記錄一下練習DP的過程，~~沒偷懶的話~~打算一天至少一題，難度慢慢遞增。

## Luogu P1077

[Link](https://www.luogu.com.cn/problem/P1077)

定義 $dp[i][j]$ 為第 $i$ 種花放第 $j$ 個花盆的方法數。

轉移： $dp[i][j] = dp[i][j] + dp[i-1][j-k], \quad 1\leq k\leq \min(a_i, j)$

時間複雜度 $\mathcal{O}(nma_i)$，空間複雜度 $\mathcal{O}(nm)$。

### 改進1
觀察一下發現可以滾動，空間壓至 $\mathcal{O}(m)$。

### 改進2
觀察一下發現可以像背包一樣倒著跑
```cpp
for(int i=0; i<n; i++)
    for(int j=m; j>=1; j--)
        for(int k=1; k<=min(a[i], j); k++)
            dp[j] = dp[j] + dp[j-k];
```
空間一樣 $\mathcal{O}(m)$。

### 改進3
```cpp
for(int k=1; k<=min(a[i], j); k++)
    dp[j] = dp[j] + dp[j-k];
```
上面相當於 $dp[j]$ 加上 $dp[j-k]$ 到 $dp[j-1]$ 這個區間，因此我們可以使用前綴和優化。

時間複雜度 $\mathcal{O}(nm)$。

## Luogu P1541

[Link](https://www.luogu.com.cn/problem/P1541)

定義 $dp[a][b][c][d]$ 為選了a張爬行卡1，b張爬行卡2，c張爬行卡3，d張爬行卡4時的得分最大值。

轉移：
    $$\begin{align*}
    dp[a][b][c][d] = & \max \left( dp[a-1][b][c][d], \right. \\\\
                     & \quad \quad \ \ dp[a][b-1][c][d], \\\\
                     & \quad \quad \ \ dp[a][b][c-1][d], \\\\
                     & \quad \quad \ \ dp[a][b][c][d-1] \left. \right) + A[a + 2b + 3c + 4d]\\\\
    \end{align*}$$

時間複雜度$\mathcal{O}((\frac{M}{4})^4)$。

## UVa 10036

[Link](http://domen111.github.io/UVa-Easy-Viewer/?10036)

定義 $dp[i][j]$ 前 $i$ 個數字是否可以湊出餘數 $j$ 。

轉移： $dp[i][j] = dp[i-1][(j-a[i]+K) \\% K]\ \ or \ \ dp[i-1][(j+a[i]+K) \\% K]$

時間複雜度$\mathcal{O}(nk)$。

## UVa 437

[Link](http://domen111.github.io/UVa-Easy-Viewer/?437)

### 觀察
每塊積木可以重複使用，所以一塊積木可以分成六塊不同長寬高，並且不難發現同一塊不可能使用兩次。

### 做法
當一塊小的積木能連到另一塊大的積木時，建一條有向邊從小的指向大的，建完圖後會發現這是一張DAG，因此問題變成在DAG上面DP。

時間複雜度$\mathcal{O}(n^2)$。

[AC code](https://github.com/Sharpless298/CompetitiveProgramming/blob/main/UVa/437.cpp)

## UVa 10739

[Link](http://domen111.github.io/UVa-Easy-Viewer/?10739)

定義 $dp[i][j]$ 為區間 $i$ 到 $j$ 所需花費的最小值。

轉移：

$$dp[i][j] = \begin{cases} 
            dp[i+1][j-1], & \text{if }s_i = s_j \\\\
            \min(dp[i+1][j], dp[i][j-1], dp[i+1][j-1])+1, & \text{else}
            \end{cases}$$

時間複雜度$\mathcal{O}({\lvert s \rvert}^2)$。

[AC code](https://github.com/Sharpless298/CompetitiveProgramming/blob/main/UVa/10739.cpp)

## AtCoder 369D

[Link](https://atcoder.jp/contests/abc369/tasks/abc369_d)

定義 $dp0,\ dp1$ 為當前偶數、奇數擊殺的經驗最大值。

轉移：
    $$dp0 = \max(dp0,\ dp1 + 2a_i)$$
    $$dp1 = \max(dp1,\ dp0 + a_i)$$

時間複雜度$\mathcal{O}(n)$。

[AC code](https://atcoder.jp/contests/abc369/submissions/59461888)

## UVa 11351

經典約瑟夫問題

定義 $dp[n] = m$ 為 $n$ 個人的時候倖存者為第 $m$ 個人。

轉移： $dp[n] = (dp[n-1]+k) \\% n$

時間複雜度$\mathcal{O}(n)$。

[AC code](https://github.com/Sharpless298/CompetitiveProgramming/blob/main/UVa/11351.cpp)
