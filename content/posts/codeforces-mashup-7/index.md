+++
date = '2026-01-08T03:09:52+08:00'
draft = false
title = 'Codeforces Mashup 7'
katex = true
+++

## CF 2157E
### Description
[Link](https://codeforces.com/problemset/problem/2157/E)

### Solution

定義 $cnt_x$ 為數列 $a$ 中的 $x$ 的個數。

觀察發現 $i$ 從小到大，如果 $cnt_i > k$ ，則令 $cnt_{i+1} \\leftarrow cnt_{i+1}+cnt_i-1, \\quad cnt_i\\leftarrow 1$ 。  
他們的最終 $cnt$ 會和題目的原操作最終 $cnt$ 會一樣，因此只需要在不斷執行上面操作的時候找到最長連續 $cnt_i > k$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2157/submission/357057728)

## CF 2149F
### Description
[Link](https://codeforces.com/problemset/problem/2149/F)

### Solution
#### 觀察
- 當 $k$ 個回合能走到 $d$ 點時，$k+1$ 也可以；當 $k$ 個回合不能走到 $d$ 點時，$k-1$ 個回合也不能。
- 總共有 $k$ 個回合時，有 $k-d$ 個回合可以休息。

觀察一告訴你這可以對答案二分搜。至於怎麼決定 $k$ 個回合能不能走到 $d$ 點？不難證明最好的方法是分成 $k-d+1$ 個連續步數走完，且盡可能平均分散。

時間複雜度 $O(t\\log d)$ 。

[AC Code](https://codeforces.com/contest/2149/submission/357920353)

## CF 2109D
### Description
[Link](https://codeforces.com/contest/2109/problem/D)

### Solution
用 BFS 計算以奇數和偶數步走到每一個點的最短步數，如果不可能則設為無限大。接著從題目給的集合找到最大可能奇數和偶數，判斷每個點需要的奇或偶步數有沒有小於等於最大可能奇數和偶數。

時間複雜度 $O(n + m + l)$ 。

[AC Code](https://codeforces.com/contest/2109/submission/360805417)

## CF 2064D
### Description
[Link](https://codeforces.com/contest/2064/problem/D)

### Solution
當一個數 $a$ 大於另一個數 $b$ 時，二進位表示下必然存在某個最高的位置，使得在這一位上 $a$ 為 $1$ 而 $b$ 為 $0$，且所有更高位元完全相同。因此我們可以 greedy 地處理每個詢問 $x$ 。

考慮詢問 $x$ 目前 MSB 的位置，所有 $w$ 中這一位為 $0$ 的數，其 MSB 必定更小，因此一定可以被吃掉。我們只需要關注在這一位為 $1$ 的數：設從目前位置開始，第一個在這一位為 $1$ 的數的 index 為 $prev$，那麼 $x$ 會吃掉它，並使得這一位在 XOR 後變為 $0$，也就是 MSB 下降。接著繼續往左找下一個在這一位為 $1$ 的數，這個位置就是第一個可能無法繼續吃的位置之一，可以用來更新答案。當我們處理更低一位元時，只需要從 $prev$ 開始繼續找。

如果目前這一位的前綴 XOR 為 $0$，那麼 $x$ 無法吃掉任何在這一位為 $1$ 的數，因為那些數的 MSB 嚴格大於目前的 $x$。此時只需要找到從目前位置開始第一個在這一位為 $1$ 的 index，並用它來更新答案，不需要移動 $prev$。

預處理每個位元的 XOR 前綴和並記錄每個位元為 $1$ 的所有 index，用 binary search 找到下一個 $1$ 的位置。總時間複雜度 $O(q \\log W \\log n)$ 。

[AC Code](https://codeforces.com/contest/2064/submission/362659445)

## CF 2036F
### Description
[Link](https://codeforces.com/problemset/problem/2036/F)

### Solution
先求出 $[l,r]$ 的區間 XOR 值，再去 XOR 所有區間內的 $x$ 滿足 $x \\not\\equiv k \\pmod{2^i}$ 。

令 $f(x)$ 為 $0 \\oplus 1 \\oplus \\dots \\oplus x$ ，觀察可以得出 
\\[
    f(x) =
    \\begin{cases}
    x & \\text{if } x \\equiv 0 \\pmod{4} \\\\
    1 & \\text{if } x \\equiv 1 \\pmod{4} \\\\
    x + 1 & \\text{if } x \\equiv 2 \\pmod{4} \\\\
    0 & \\text{if } x \\equiv 3 \\pmod{4}
    \\end{cases}
\\]

，$f(l - 1) \\oplus f(r)$ 就是 $[l,r]$ 的區間 XOR 值。

接著計算所有 $x$ 滿足 $x \\not\\equiv k \\pmod{2^i}$ ，發現只要把 $l$ 和 $r$ 往右移 $i$ 個 bit 就可以再套用 $f(x)$ 。而比第 $i$ 位小的那幾個 bit 只有在那個 bit 是 $1$ 且長度為奇數的時候才會是 $1$ ，否則為 $0$ 。

時間複雜度 $O(\\log r)$ 。

[AC Code](https://codeforces.com/contest/2036/submission/365112916)
