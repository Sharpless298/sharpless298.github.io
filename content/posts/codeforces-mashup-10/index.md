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

## CF 1978E
### Description
[Link](https://codeforces.com/problemset/problem/1978/E)

### Solution
注意到先對整個 $s$ 執行操作一，再對整個 $t$ 執行操作二總是最好。假設 $s^{\\prime}$ 和 $t^{\\prime}$ 是經過操作後的數列，用前綴和預處理 $s^{\\prime}$ 前 $i$ 個 $s_{i}^{\\prime}=1$ 的個數。觀察到當把完整字串切成 $[l,r]$ 的子字串時，受到影響地方只有 $s_l,s_{l+1},s_{r-1},s_r$ 四個地方，用 $s,\\ s^{\\prime},\\ t$ 就可以推出每個位置會不會受影響。

時間複雜度 $O(n+q)$ 。

[AC Code](https://codeforces.com/contest/1978/submission/367557220)

## CF 1956D
### Description
#### 觀察
- 把任意長度子陣列的元素全都變成 $0$ 的操作不會超過 $2$ 。
- 元素全為 $0$ 的長度 $k$ 陣列可以在 $2^k$ 次操作把全部元素換成 $k$ 。
- $2^{18}=262144<5\\times10^5$

使用動態規劃，令 $f(i)$ 表示前 $i$ 個數的總和最大值，轉移
\\[
    f(i) = \\max \\left(
    a_i + f(i-1),\\;
    \\max_{1 \\le k \\le i} \\left( f(i-k) + k^2 \\right)
    \\right)
\\]

時間複雜度 $O(2^n)$ 。

[AC Code](https://codeforces.com/contest/1956/submission/367758470)

## CF 1931G
### Description
[Link](https://codeforces.com/problemset/problem/1931/G)

### Solution
一個合法的擺放方式會是第一塊和第二塊拼圖交替，並且在它們之中或兩側穿插第三塊和第四塊拼圖，並且這兩塊的穿插方式是獨立的，因此分別對第三塊和第四塊做 stars and bars 相乘就是答案，特別地當第一塊和第二塊個數相同的時候會有兩種可能。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1931/submission/368421235)

## CF 1867E1
### Description
[Link](https://codeforces.com/problemset/problem/1867/E1)

### Solution
先用 $k \\lfloor\\frac{n}{k}\\rfloor$ 次詢問求出前 $k \\lfloor\\frac{n}{k}\\rfloor$ 項的 XOR 值。最後 $n \\bmod k$ 項每兩項來看，假設為 $a_i,a_{i+1}$ ，利用 $$\\operatorname{query}(i-k+1) \\oplus \\operatorname{query}(i-k+2)=a_i \\oplus a_{i+1}$$ ，操作完後也不會動到大於 $i+1$ 的位置，這樣最糟只會需要 $97$ 次操作。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1867/submission/368786696)
