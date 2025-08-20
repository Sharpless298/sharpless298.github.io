---
date: '2025-08-09T18:37:41+08:00'
draft: false
title: 'Codeforces Mashup 2'
tags: ["Codeforces"]
math: true
---

## CF 2117E
### Description
[Link](https://codeforces.com/problemset/problem/2117/E)

### Solution
顯然從陣列末端操作回來會最好，接著觀察發現刪除和不刪除的情況合在一起使得 index 為 $i$ 的陣列元素能被換成集合 $\\{a_{i+2},\\, a_{i+3}, \\, \\dots,\\, a_n,\\, b_{i+2},\\, b_{i+3},\\, \\dots ,\\,b_n\\}$ 內的任意元素，因此可以檢查 $a_i$ 或 $b_i$ 有沒有出現在集合裡，若沒有再檢查  
$a_i = b_i \\lor a_i = a_{i+1} \\lor b_i = b_{i+1}$ 是否為真，找到最大的 $i$ 就是答案，沒找到就把 $a_{i+1}$ 和 $b_{i+1}$ 加進集合裡，。

時間複雜度 $O(n)$。

我的 code 有點醜就不放了，看官解就好。

## CF 1917C
### Description
[Link](https://codeforces.com/contest/1917/problem/C)

有 $t$ 筆測資。

給一個長度為 $n$ 的數列 $a$ 和一個數列 $b$ ，在接下來的 $d$ 天中，假設當天為第 $i$ 天，你必須且只能選擇以下其中一個操作：
<ol style="list-style-type: none; counter-reset: item;">
  <li style="counter-increment: item;">(1) 把數列 $a$ 的前 $b_i$ 項加上 $1$ 。
</li>
  <li style="counter-increment: item;">(2) 把分數加上滿足 $a_j = j$ 的個數，$1\leq j \leq n$，之後把數列 $a$ 的所有元素重置為 $0$ 。
</li>
</ol>

分數初始值為 $0$ ，求分數的最大值。

由於 $d$ 可能非常大，數列 $b$ 以壓縮格式給出：

- 給定一個整數數列 \\( v_1, v_2, \dots, v_k \\)。  
數列 $b$ 是將數列 $v$ 無限次重複拼接而成的：  \\(b = [v_1, v_2, \dots, v_k, v_1, v_2, \dots, v_k, \dots]\\)

#### Constraints
- $1\\leq t \\leq 10^3$
- $1\\leq \\sum n \\leq 2000$
- $1\\leq \\sum k \\leq 10^5$
- $k \\leq d \\leq 10^9$
- $0 \\leq a_i \\leq n$
- $1 \\leq v_i \\leq n$

### Solution
先考慮當數列 $a$ 重置為 $0$ 的情況，觀察發現不管選幾次 (1)， $a_j = j$ 的個數只會小於等於 $1$ ，因此只要 (1) (2) (1) (2) 這樣交替下去就會得到最大分數，假設有 $w$ 天則可以得到 $\\left\\lfloor \\frac{w}{2} \\right\\rfloor$ 的分數。

再考慮最初的數列 $a$ ，一個長度為 $n$ 的數列最多也只會貢獻 $n$ 的分數，再利用上面的結論，得出最多連續選 (1) $\\min(2n, d)$ 天，否則分數只會更小，$n$ 夠小所以我們可以暴力枚舉和更新數列 $a$ ，假設第 $i$ 天第一次選 (2) ，答案為 $\\max(cnt_i + \\left\\lfloor \\frac{n - i}{2} \\right\\rfloor)$，其中 $cnt_i$ 為第 $i$ 天 $a_j = j$ 的個數，$1\\leq i \\leq \\min(2n+1, d)$ ，$1\\leq j \\leq n$ 。

時間複雜度 $O(n ^ 2)$ 。

[AC Code](https://codeforces.com/contest/1917/submission/333519011)

## CF 1671D
### Description
[Link](https://codeforces.com/problemset/problem/1671/D)

### Solution
#### 觀察
- $a^{\\prime}$ 的分數大於等於 $a$ 。
- 一段遞增或遞減的數列會比其他排列方式的分數小，且分數為首項減末項的絕對值。

根據觀察可以發現只需要關注 $1$ 和 $x$ 插在哪就好，因為當 $1$ 和 $x$ 插好後，我們一定可以把剩下的數找到某個遞增或遞減的區間插入，上面的第二個觀察告訴你它們不會影響分數。

先計算原數列的分數，再枚舉插入 $1$ 的位置，找到插入後增加的分數為最小的那個，頭尾的位置分別會多出 $\\lvert a_1 - 1 \\rvert$ 和 $\\lvert a_{n} - 1 \\rvert$ ，其他位置會多出 $2 \\cdot \\lvert a_i - 1\\rvert$ ；同樣地，當 $x$ 小於等於數列 $a$ 的最大值時不影響分數，否則就用和插入 $1$ 一樣的方式計算。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1671/submission/333668690)

## CF 1899F
### Description
[Link](https://codeforces.com/problemset/problem/1899/F)

有 $t$ 筆測資。

構造一棵有 \\( n \\) 個節點的樹。

接下來有 \\( q \\) 天，每天有一個整數 \\( d_i \\) ，在第 \\( i \\) 天時，樹中必須存在兩個葉節點，其距離**正好**等於 \\( d_i \\)。  

每天開始前，你最多可以做一次操作：  

1. 選擇三個節點 \\( u, v_1, v_2 \\)，其中 \\( u \\) 與 \\( v_1 \\) 有邊相連，且 \\( u \\) 與 \\( v_2 \\) 沒有邊相連。  
2. 移除邊 \\( (u, v_1) \\)，加入邊 \\( (u, v_2) \\)。  
3. 操作後圖仍必須是一棵樹。  

可以證明總是存在一棵樹與對應的操作序列，能滿足所有 \\( d_i \\) 的條件。  

#### Constraints
- $1\\leq t\\leq 100$
- $3\\leq n \\leq 500$
- $\\sum n \\leq 500$
- $1\\leq \\sum q \\leq 500$
- $2\\leq d_i \\leq n-1$

### Solution
$(x,y)$ 表示節點 $x$ 和節點 $y$ 之間有一個邊，考慮以下構造方式：
$$(1, n-1),\\,(n-1,n-2),\\,(n-2,n-3),\\,\\dots,\\,(3,2),(2,n)$$
當操作為 $u=1,\\,v_1=n-1,\\,v_2=k$ ，節點 $1$ 和節點 $n$ 的距離恰為 $k$ ，且 $2\\leq k = d_i\\leq n-1$ ，因此我們只需要記錄節點 $1$ 前一次連的點 $l$ ，就可以 $O(1)$ 操作 $u=1,\\,v_1=l,\\,v_2=d_i$ 。

時間複雜度 $O(n + q)$ 。

[AC Code](https://codeforces.com/contest/1899/submission/333784568)

## CF 2051E
### Description
[Link](https://codeforces.com/contest/2051/problem/E)

有 $t$ 筆測資。

有 $n$ 位顧客已經來到商店，想要購買聖誕樹，在銷售開始之前，商店需要為每棵樹設定一個統一的價格。

對於第 $i$ 位顧客，已知兩個整數 $a_i$ 和 $b_i$，它們決定了該顧客的行為：

- 若價格不超過 $a_i$ ，顧客會購買一棵樹並留下好評。
- 若價格超過 $a_i$ 且不超過 $b_i$ ，顧客會購買一棵樹但留下負評。
- 若價格超過 $b_i$ ，顧客將不會購買任何樹。

求在負評數量不超過 $k$ 的條件下，商店能夠獲得的最大收益。

#### Constraints
- $1\\leq t \\leq 10^4$
- $1 \\leq \\sum n \\leq 2\\cdot 10^5$
- $0\\leq k \\leq n$
- $1\\leq a_i < b_i \\leq 2\\cdot 10^9$

### Solution
令集合 $S$ 為 $\\{a_1,\\,a_2,\\,\\dots,\\,a_n,\\,b_1,\\,b_2,\\,\\dots,\\,b_n\\}$ ，且 $p \\in S$ 。

#### 觀察
- 最大收益的價格只會在 $S$ 裡。
- 負評數量不超過 $k$ $\\iff$ 滿足 $a_i < p \\leq b_i$ 的個數不超過 $k$ 。
- 最大收益為價格乘上滿足 $b_i\\leq p$ 的個數。

離散化後第二個和第三個觀察可以用差分解決，之後暴力枚舉 $S$ 裡面的元素。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2051/submission/333824127)
