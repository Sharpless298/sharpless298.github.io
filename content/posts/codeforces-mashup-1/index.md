+++
date = '2025-08-02T05:18:41+08:00'
draft = false
title = 'Codeforces Mashup 1'
katex = true
+++

## CF 2034D
### Description

[Link](https://codeforces.com/problemset/problem/2034/D)

### Solution

定義 $cnt\_0,\\ cnt\_1,\\ cnt\_2$ 分別為 $0, 1, 2$ 的個數。

一個遞增數列的 $\[0, cnt\_0)$ 區間必定都是 $0$ ， 先考慮把這個區間的數都換成 $0$ ，以下 $\\forall i \\in \[0, cnt\_0)$。

*   $a\_i = 0:$ 不動作。
*   $a\_i = 1:$ 找最右邊 $0$ 交換。
*   $a\_i = 2:$ 先找最右邊的 $1$ 交換， 再找最右邊的 $0$ 交換。

最後再排序 $\[cnt\_0, n)$。

對於以下幾種情況：

1.  整個數列只有 $\\{0, 1\\}$ 或 $\\{1, 2\\}$，會交換 $\\min(cnt\_0, cnt\_1)$ 或 $\\min(cnt\_1, cnt\_2)$ 次。
2.  區間 $\[0, cnt\_0)$ 都是 $1$，會交換 $cnt\_0$ 次，$\[cnt\_0, n)$ 會交換 $\\min(cnt\_1, cnt\_2)$ 次，總共 $cnt\_0 + \\min(cnt\_1, cnt\_2)$ 次。
3.  區間 $\[0, cnt\_0)$ 都是 $2$，會交換 $2cnt\_0$ 次，且除了第一次交換，每次都必定會有一個 $2$ 被交換至 $\[cnt\_0+cnt\_1, n)$ 之間，因此 $\[cnt\_0, n)$ 會交換 $cnt\_2-(cnt\_0-1)$ 次，總共 $cnt\_0 + cnt\_2 + 1$ 次，題目保證  
$cnt\_1 \\geq 1$ ，因此 $cnt\_0 + cnt\_2 + 1 \\leq n$。
4.  顯然其他情況不會比 3. 更糟。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2034/submission/331907445)

## CF 1766D
### Description

[Link](https://codeforces.com/contest/1766/problem/D)

### Solution

觀察一下不難發現：

*   $x=y \\Rightarrow k = 0$
*   $x=y-1 \\Rightarrow k = \\infty$

對於 $x < y - 1$ 的情況，我們先將數對 $(x,y)$ 兩邊減去 $x$ 變成 $(0, y-x)$ ，此時問題變成：

<p style="text-align: center; font-weight: bold;">
找到一個最小的正整數 $\bm{z \geq x}$ 使得 $\bm{\gcd(z, y-x+z) \neq 1}$
</p>

假設 $y-x$ 有 $c$ 個相異質因數 $p\_i,\\;i \\in \[1, c\]$ $$y-x = p\_1 p\_2 \\dots p\_c$$

觀察可發現 $\\gcd(z, y-x+z) \\neq 1 \\Rightarrow$ $(y-x)$ 至少有一個質因數整除 $z$，因此對於每一個 $(y-x)$ 的質因數 ，皆存在一個最小的正整數 $m\_i$ 使得 $p\_i m\_i \\geq x$ ，找到最小的 $p\_i m\_i - x$ 就是答案。

令 $N$ 為 $(y - x)$ 的最大值，利用線性篩可以紀錄最小質因數達到 $O(\\log N)$ 分解質因數。

時間複雜度 $O(n \\log N)$ 。

[AC Code](https://codeforces.com/contest/1766/submission/332299877)

## CF 1857F
### Description

[Link](https://codeforces.com/problemset/problem/1857/F)

### Solution

$$ \\begin{align} a\_i + a\_j = x \\\\ a\_i \\cdot a\_j = y \\end{align} $$ 由 $(1)$ 得 $a\_j = x - a\_i$ 代入 $(2)$ $$ \\begin{aligned} &{a\_j}^2-xa\_i+y=0 \\\\\[0.6em\] \\Rightarrow\\;&a\_j = \\frac{x \\pm \\sqrt{x^2-4y}}{2} \\\\ \\Rightarrow\\;&a\_i = x - a\_j \\end{aligned} $$

$a\_i$, $a\_j$有解的話要符合：

*   $x^2-4y \\geq 0$ 且為完全平方數
*   $x \\pm \\sqrt{x^2-4y}$ 是偶數

當 $a\_i \\neq a\_j$ ，答案為 $a\_i$ 和 $a\_j$ 個數相乘；當 $a\_i = a\_j$ ，假設個數為 $k$ ，答案為 $\\binom{k}{2}$ 。

時間複雜度 $O(q \\log n)$。

[AC Code](https://codeforces.com/contest/1857/submission/332627790)

## CF 1680C

### Description

[Link](https://codeforces.com/problemset/problem/1680/C)

### Solution

定義 $p\_0$ 和 $p\_1$ 為 $0$ 和 $1$ 的個數前綴和，以下都是左閉右開區間。

使用雙指標，$\[l, r)$ 表示沒被刪除的區間，對於每一個 $l$ 只要滿足 $p\_0(r)-p\_0(l) < p\_1(l)+p\_1(n)-p\_1(r)$ ，就不斷右移 $r$ ，答案為 $\\max(p\_0(r)-p\_0(l),\\, p\_1(l)+p\_1(n)-p\_1(r))$ 的最小值。

時間複雜度 $O(n)$。

[AC Code](https://codeforces.com/contest/1680/submission/332749464)

## CF 1843E
### Description

[Link](https://codeforces.com/problemset/problem/1843/E)

### Solution

定義 $cnt\_0$ 和 $cnt\_1$ 為 $0$ 和 $1$ 的個數。

觀察到若前 $k$ 項滿足 $cnt\_1 > cnt\_0$ 時，前 $k + 1$ 項也會滿足；相反地，若前 $k$ 項不滿足 $cnt\_1 > cnt\_0$ 時，前 $k - 1$ 項也會不滿足。因此我們可以對 $k$ 二分搜，每次 $O(n)$ 修改並計算 $1$ 的前綴和，接著 $O(m)$ 檢查每個區間有沒有滿足。

時間複雜度 $O((n+m)\\log q)$ 。

[AC Code](https://codeforces.com/contest/1843/submission/332966958)
