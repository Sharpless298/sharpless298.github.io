+++
date = '2025-08-09T18:37:41+08:00'
draft = false
title = 'Codeforces Mashup 2'
katex = true
+++

CF 2117E
--------

### Description

[Link](https://codeforces.com/problemset/problem/2117/E)

### Solution

顯然從陣列末端操作回來會最好，接著觀察發現刪除和不刪除的情況合在一起使得 index 為 $i$ 的陣列元素能被換成集合 $\\{a\_{i+2},\\, a\_{i+3}, \\, \\dots,\\, a\_n,\\, b\_{i+2},\\, b\_{i+3},\\, \\dots ,\\,b\_n\\}$ 內的任意元素，因此可以檢查 $a\_i$ 或 $b\_i$ 有沒有出現在集合裡，若沒有再檢查 $a\_i = b\_i \\lor a\_i = a\_{i+1} \\lor b\_i = b\_{i+1}$ 是否為真，找到最大的 $i$ 就是答案，沒找到就把 $a\_{i+1}$ 和 $b\_{i+1}$ 加進集合裡。

時間複雜度 $O(n)$。

我的 code 有點醜就不放了，看官解就好。

CF 1917C
--------

### Description

[Link](https://codeforces.com/contest/1917/problem/C)

### Solution

先考慮當數列 $a$ 重置為 $0$ 的情況，觀察發現不管選幾次 (1)， $a\_j = j$ 的個數只會小於等於 $1$ ，因此只要 (1) (2) (1) (2) 這樣交替下去就會得到最大分數，假設有 $w$ 天則可以得到 $\\left\\lfloor \\frac{w}{2} \\right\\rfloor$ 的分數。

再考慮最初的數列 $a$ ，一個長度為 $n$ 的數列最多也只會貢獻 $n$ 的分數，再利用上面的結論，得出最多連續選 (1) $\\min(2n, d)$ 天，否則分數只會更小，$n$ 夠小所以我們可以暴力枚舉和更新數列 $a$ ，假設第 $i$ 天第一次選 (2) ，答案為 $\\max(cnt\_i + \\left\\lfloor \\frac{n - i}{2} \\right\\rfloor)$，其中 $cnt\_i$ 為第 $i$ 天 $a\_j = j$ 的個數，$1\\leq i \\leq \\min(2n+1, d)$ ，$1\\leq j \\leq n$ 。

時間複雜度 $O(n ^ 2)$ 。

[AC Code](https://codeforces.com/contest/1917/submission/333519011)

CF 1671D
--------

### Description

[Link](https://codeforces.com/problemset/problem/1671/D)

### Solution

#### 觀察

*   $a^{\\prime}$ 的分數大於等於 $a$ 。
*   一段遞增或遞減的數列會比其他排列方式的分數小，且分數為首項減末項的絕對值。

根據觀察可以發現只需要關注 $1$ 和 $x$ 插在哪就好，因為當 $1$ 和 $x$ 插好後，我們一定可以把剩下的數找到某個遞增或遞減的區間插入，上面的第二個觀察告訴你它們不會影響分數。

先計算原數列的分數，再枚舉插入 $1$ 的位置，找到插入後增加的分數為最小的那個，頭尾的位置分別會多出 $\\lvert a\_1 - 1 \\rvert$ 和 $\\lvert a\_{n} - 1 \\rvert$ ，其他位置會多出 $2 \\cdot \\lvert a\_i - 1\\rvert$ ； 同樣地，當 $x$ 小於等於數列 $a$ 的最大值時不影響分數，否則就用和插入 $1$ 一樣的方式計算。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1671/submission/333668690)

CF 1899F
--------

### Description

[Link](https://codeforces.com/problemset/problem/1899/F)

### Solution

$(x,y)$ 表示節點 $x$ 和節點 $y$ 之間有一個邊，考慮以下構造方式： $$(1, n-1),\\,(n-1,n-2),\\,(n-2,n-3),\\,\\dots,\\,(3,2),(2,n)$$ 當操作為 $u=1,\\,v\_1=n-1,\\,v\_2=k$ ，節點 $1$ 和節點 $n$ 的距離恰為 $k$ ，且 $2\\leq k = d\_i\\leq n-1$ ，因此我們只需要記錄節點 $1$ 前一次連的點 $l$ ，就可以 $O(1)$ 操作 $u=1,\\,v\_1=l,\\,v\_2=d\_i$ 。

時間複雜度 $O(n + q)$ 。

[AC Code](https://codeforces.com/contest/1899/submission/333784568)

CF 2051E
--------

### Description

[Link](https://codeforces.com/contest/2051/problem/E)

### Solution

令集合 $S$ 為 $\\{a\_1,\\,a\_2,\\,\\dots,\\,a\_n,\\,b\_1,\\,b\_2,\\,\\dots,\\,b\_n\\}$ ，且 $p \\in S$ 。

#### 觀察

*   最大收益的價格只會在 $S$ 裡。
*   負評數量不超過 $k$ $\\iff$ 滿足 $a\_i < p \\leq b\_i$ 的個數不超過 $k$ 。
*   最大收益為價格乘上滿足 $b\_i\\leq p$ 的個數。

離散化後第二個和第三個觀察可以用差分解決，之後暴力枚舉 $S$ 裡面的元素。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2051/submission/333824127)
