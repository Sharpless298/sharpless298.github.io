+++
date = '2025-09-11T14:26:33+08:00'
draft = false
title = 'Codeforces Mashup 4'
katex = true
+++

## CF 1422C
### Description
[Link](https://codeforces.com/contest/1422/problem/C)

### Solution
考慮每個 digit 的貢獻，從右邊數過來，第 $i$ 個 digit 會貢獻 $10^{i-1}\\cdot (i * \\sum_{i+1}^n d_i + \\frac{1}{2}(1+n-i)\\cdot (n-i)\\cdot d_i)$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1422/submission/338028448)

## CF 1550C
### Description
[Link](https://codeforces.com/contest/1550/problem/C)

### Solution
#### 觀察
- 假設 $i<j<k$ ，他們構成 bad triple 若且唯若 $a_i\\leq a_j \\leq a_k \\lor a_k \\leq a_j \\leq a_i$ 。
- good subarray 的長度不會超過 $4$ 。

只需要檢查所有長度為 $3$ 和 $4$ 的 subarray 就好，所有被夾在中間的點都不能和其他點構成 bad triple ，長度 $3$ 檢查 $1$ 次，長度 $4$ 檢查 $4$ 次，答案別忘了再加上長度 $1$ 和 長度 $2$ 。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/1550/submission/338143767)

## CF 1695C
### Description
[Link](https://codeforces.com/contest/1695/problem/C)

### Solution
`bitset` 練習題。

[AC Code](https://codeforces.com/contest/1695/submission/338256083)
