+++
date = '2025-08-15T00:10:22+08:00'
draft = false
title = 'Codeforces Mashup 3'
katex = true
+++

## CF 2039D
### Description

[Link](https://codeforces.com/problemset/problem/2039/D)

### Solution

當 $i=1,\\; \\forall j \\in \[2,n\] :$ $$a\_{\\gcd(1,j)}=a\_1 \\neq \\gcd(a\_1,a\_j)$$ 觀察得到 $$a\_1 \\neq \\gcd(a\_1,a\_j) \\iff a\_1 \\nmid a\_j$$

先假設 $a\_1$ 滿足 $a\_1 \\nmid a\_j$ ，繼續往下推。

當 $i=2,\\; \\forall j \\in \[3,n\] :$ \\\[ a\_{\\gcd(2,j)} = \\begin{cases} a\_1 \\neq \\gcd(a\_2, a\_j), & j \\text{ is odd.} \\\\ a\_2 \\neq \\gcd(a\_2, a\_j), & j \\text{ is even.} \\end{cases} \\\]

*   當 $j$ 是奇數： 因為前面已經假設 $a\_1$ 不會整除其他數，它自然也不會是其他兩數的最大公因數，所以這條式子成立。
*   當 $j$ 是偶數： 同樣可得 $a\_2 \\neq \\gcd(a\_2,a\_j) \\iff a\_2 \\nmid a\_j$ 。

接著再假設 $a\_2 \\nmid a\_j$ ，推 $i=3,\\;\\forall j \\in \[4,n\]$ 的情況，這樣不斷推下去可以得到一個結論： $$\\forall\\, i \\in \[1,n\],\\;\\forall\\, j \\in (i,n\],\\;\\forall\\, k \\in \[2,\\left\\lfloor \\frac{n}{i} \\right\\rfloor\] \\quad a\_i\\neq \\gcd(a\_i,a\_j) \\iff a\_i \\nmid a\_{ki}$$

結論有了，怎麼構造？ 其實很簡單，**一個數不能整除比他小的數**，題目又剛好要求字典序最大，因此考慮以下構造方式：

*   令題目給定的集合 $S = \\{ s\_1, s\_2, \\dots, s\_m \\}, \\quad s\_1 < s\_2 < \\cdots < s\_m$
*   $a\_1=s\_m$
*   對於 $i \\geq 2$ ，設 \\(a\_j = \\min \\{ a\_k : k \\mid i,\\, k \\neq i \\}\\) ，若 $a\_j$ 為 $s\_t$， 則令 $a\_i$ 為 $s\_{t-1}$ ； 若 $t=1$ 則無解。

時間複雜度 $O(n \\log n)$ 。

[AC Code](https://codeforces.com/contest/2039/submission/333991898)

## CF 2112D
### Description

[Link](https://codeforces.com/problemset/problem/2112/D)

### Solution

#### 觀察

*   $n = 2$ 無解
*   $u \\rightarrow v \\rightarrow w$ 有 $3$ 個 good pair
*   $v\_1\\rightarrow v\_2 \\leftarrow v\_3 \\rightarrow \\dots \\leftarrow v\_k$ 有 $k-1$ 個 good pair

找到一個度數為 $2$ 的節點 $v$ ，假設 $v$ 相鄰的節點為 $v, w$ ，就像觀察二一樣構造 $u \\rightarrow v \\rightarrow w$ ，剩下的點就像觀察三一樣接上去就好，參考下圖

![](/posts/codeforces-mashup-3/graph.png)

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2112/submission/334600976)

## CF 1975D
### Description

[Link](https://codeforces.com/contest/1975/problem/D)

### Solution

#### 觀察

*   $P\_A,\\,P\_B$ 亂逛是沒有用的，應該先找到最先被染色成藍色的點，假設為 $v$ 。
*   假設所有的點中與 $v$ 的最遠距離為 $d$ ，答案為 $dis(b, v) + 2(n-1) - d$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1975/problem/D)

## CF 1430D
可能因為這題太老了，感覺不到這題 rating 有 1700 。
### Description
[Link](https://codeforces.com/problemset/problem/1430/D)

### Solution
對於操作一，先從由單一字元構成且長度 $\\geq 2$ 的子字串開始刪，且由左往右，如果找不到這種子字串則從最左邊開始刪。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1430/submission/337133361)

## CF 1777C
### Description
[Link](https://codeforces.com/contest/1777/problem/C)

### Solution
#### 觀察
- 因為 $\\{1,\\,2,\\,\\cdots,\\, \\frac{m}{2}\\}$ 中的每一個數必定至少是 $\\{\\frac{m}{2}+1,\\,\\frac{m}{2}+2,\\,\\cdots ,\\,m\\}$ 其中的一個因數，因此只需要檢查 $\\left[\\frac{m}{2}+1, m\\right]$ 。
- 重複的元素沒有用。

 根據觀察可以把數列 $a$ 中所有小於 $(\\frac{m}{2}+1)$ 的數和重複的數刪掉後再排序，接著使用雙指標，暴力檢查當前的數是不是 $\\left[\\frac{m}{2}+1, m\\right]$ 的倍數，若小於就跳出迴圈。不斷右移右指標直到能湊齊 $\\left[\\frac{m}{2}+1, m\\right]$ 。

最糟的情況是 $m = n$ ，根據觀察可以把數列的長度縮減成最多 $\\frac{n}{2}$ 且裡面元素不重複，  
且總操作次數 $1 + 2 + \\dots + \\frac{n}{2} \\approx \\frac{n^2}{8}$ 。

[AC Code](https://codeforces.com/contest/1777/submission/337883398)
