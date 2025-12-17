+++
date = '2025-12-03T20:30:54+08:00'
draft = false
title = 'Advent of Code 2025'
katex = true
+++

記錄一下今年 AOC 的解題過程，即便今年縮減到只有 12 天，題目品質不知道為什麼不如去年。

## Day 03 - Part 2
### Description
給一個 $n$ 個 digit 的正整數，求去掉當中 3 個 digit 後的最大值。

### Solution
動態規劃，定義 $f(i,j)$ 為選第 $i$ 個整數當作第 $j$ 位數的最大值。

轉移 $f(i,j)=\\max(f(i,j), f(i-1,j)\\cdot 10+s_i)$ 。

時間複雜度 $O(n^2)$。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2003/part2.cpp)

## Day 04 - Part 2
### Description
有一張 $n \times m$ 的網格，裡面用 @ 表示紙卷。
你能移除一個紙卷，當它周圍 $8$ 格中，紙卷的數量小於 $4$。
移除後，它周圍的其他紙卷可能變得「可存取」，於是也能再被移除。
重複這個過程，直到沒有紙卷可以再被存取為止，求總共移除紙卷的數量。

### Solution
記錄每個紙卷周圍 $8$ 格內有幾個紙卷，如果數量小於 $4$ 就把他丟進 queue 裡面。每次從 queue 裡面拿出一個點表示這個紙卷要被移除，把他周圍 $8$ 格紙卷的周圍 $8$ 格有多少紙卷的數量減一，如果減一後數量小於 $4$ 就把他丟進 queue 裡面，不斷重複直到 queue 為空。可以令不是紙卷的位置和已經被移除的紙卷周圍 $8$ 格的數量為無限大避免重複計算。

最糟每個點都被丟進 queue 裡面一次，時間複雜度 $O(nm)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2004/part2.cpp)

## Day 05 - Part 1
### Description
有 $n$ 個區間，$q$ 筆詢問，求有多少詢問至少被一個區間包含。

### Solution
離散化後差分。

時間複雜度 $O((n+q)\\log (n+q))$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2005/part1.cpp)

## Day 05 - Part 2
### Description
有 $n$ 個區間，求總共有多少數字至少被一個區間包含。

### Solution
掃描線。

時間複雜度 $O(n \\log n)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2005/part2.cpp)

## Day 07 - Part 2
### Description
有一個 $n\\times m$ 的圖，`^` 記作 splitter 。最開始有一個粒子只會往下走，每遇到一次 splitter，粒子會同時往左、往右展開，形成兩條時間線，求有多少條不同的 timeline 。

### Solution
定義 $cnt_i$ 為粒子在第 $i$ 列的時間線個數，當第 $j$ 列有 splitter 時，把 $cnt_{j-1}$ 和 $cnt_{j+1}$ 的個數加上 $cnt_j$ ，再把 $cnt_j$ 設為 $0$ ，答案為 $\sum cnt_i$ 。

時間複雜度 $O(nm\\log m)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2007/part2.cpp)

## Day 08 - Part 1
### Description
有 $n$ 個三維座標，在連接前 $1000$ 個最近點對後，求最大三個連通分量的大小相乘。

### Solution
把所有點對的距離丟進 min heap 裡面，再用 DSU 把前 $1000$ 個點對合併。

時間複雜度 $O(n^2\\log n)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2008/part1.cpp)

## Day 08 - Part 2
### Description
要你連接所有最近點對，求最後成功合併兩個不同集合時的兩個點的 $x$ 座標相乘。

### Solution
一樣用 DSU ，不斷記錄最後成功合併的兩點 $x$ 座標相乘就好。

時間複雜度 $O(n^2\\log n)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2008/part2.cpp)

## Day 09 - Part 2
### Description
有一個 $n \\times m$ 的網格圖，給 $V$ 個紅色磁磚，所有在同一行或同一列的紅色磁磚之間都有綠色磁磚把他們連起來，被包起來的點也會變成綠色磁磚。

可以選兩個點當作長方形的對角兩點，且此長方形每個點必須都是紅色或綠色的磁磚，求所有可能長方形的最大面積。

### Solution
可以把所有點離散化，因為這不影響能不能構成一個合法的長方形。

先填上外圍綠色磁磚再填內部的點，而一個點是被包起來的若且唯若他的上下左右都能找到至少一個紅色或綠色的磁磚，用前綴和預處理就可以 $O(1)$ 解決。

接著枚舉所有紅色點對，一個長方形合法若且唯若長方形的面積等於他包含紅色或綠色磁磚個數，同樣用二維前綴和預處理後可以 $O(1)$ 。

時間複雜度 $O(V^2)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2009/part2.cpp)

## Day 10 - Part 1
### Description
給一個最初皆為 $0$ 的 binary string 和 $n$ 個按鈕，每個按鈕可以使得當前字串某幾個位元反轉，且每個按鈕都可以按無數次，求最少按幾次可以達到目標字串。

### Solution
位元枚舉。

時間複雜度 $O(n^2)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2010/part1.cpp)

## Day 11 - Part 2
### Description
給一張 DAG ，求從點 $u$ 到 $v$ 的路徑中，必須不限順序經過 $x$ 和 $y$ 兩點的走法有幾種。

### Solution
經典拓撲排序 + DP，多開一個維度表示當前狀態是否有走過 $x, y$ 兩點，$0$ 表示都沒走過，$1$ 表示走過 $x$ 點，$2$ 表示走過 $y$ 點，$3$ 表示兩點都走過。
假設 $u$ 指向 $v$ ，轉移：

- 當 $v$ 是 $x$ ，$f_v(1)\\leftarrow f_v(1) + f_u(0), \\ f_v(3)\\leftarrow f_v(3) + f_u(2)$ 
- 當 $v$ 是 $y$ ，$f_v(2)\\leftarrow f_v(2) + f_u(0), \\ f_v(3)\\leftarrow f_v(3) + f_u(0)$ 
- 當 $v$ 不是 $x$ 或 $y$ ，$\\forall\\, i \\in [0,4)\\quad f_v(i) \\leftarrow f_v(i) + f_u(i)$

時間複雜度 $O(V + E)$ 。

[Code](https://github.com/Sharpless298/adventofcode/blob/main/2025/Day%2011/part2.cpp)
