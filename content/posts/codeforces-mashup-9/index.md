+++
date = '2026-03-10T08:04:10+08:00'
draft = false
title = 'Codeforces Mashup 9'
katex = true
+++

## CF 2171E
### Description
[Link](https://codeforces.com/problemset/problem/2171/E)

### Solution
從 $1$ 開始，每六個連續數字一組，$\\operatorname{block}_i$ 表示第 $i$ 組，每一組按照以下方式排
\\[
\\operatorname{block}_i =
\\begin{cases}
[2+6i,\\,1+6i,\\,4+6i,\\,6+6i,\\,5+6i,\\,3+6i], & \\text{if $i$ is odd} \\\\
[3+6i,\\,5+6i,\\,6+6i,\\,4+6i,\\,1+6i,\\,2+6i], & \\text{if $i$ is even}
\\end{cases}
\\]
，這樣保證每一組裡面和每一組的連接處都會是 good ，最後那幾個湊不出一組的數直接放最後面。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2171/submission/366050065)

## CF 2158D
### Description
[Link](https://codeforces.com/problemset/problem/2158/D)

### Solution
在紙上畫一下就可以很快證明所有長度為 $4$ 的字串可以經過操作變成任意字串，由此可以再推得長度 $n\\geq 4$ 的也會滿足，例如 $n=6$ 時可以拆成 $[1,4]$ 和 $[3,6]$ 兩塊長度為 $4$ 的子字串。

用 BFS 計算所有長度為 $5$ 的字串變成任意字串的所需操作，輸出結果後觀察到最大操作次數不會超過 $4$ ，因此可以把整個字串每五個拆成一塊，不足五個的往左延伸補到五個。最差會需要 $4 \\times \\lceil\\frac{n}{5}\\rceil$ 操作。

當 $n=4$ 的時候可以再 BFS 一個長度為 $4$ ，最大操作次數不會超過 $6$ ，或者在 $s,\ t$ 後面都補個 $0$ 當成長度 $5$ 來算也剛好不影響答案。

時間複雜度 $O(n)$ 。

[AC Code](https://codeforces.com/contest/2158/submission/366176984)

如果你想要只想要用 BFS 長度為 $4$ 的結果就計算答案的話, $n=5$ 要多特判幾個 case。

[AC Code](https://codeforces.com/contest/2158/submission/366177506)

## CF 2138C2
### Description
[Link](https://codeforces.com/problemset/problem/2138/C2)

### Solution
令 $d_u$ 表示 $u$ 點的深度，LCS 的最大值會是 $\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ ，並且我們只需要關注那些 $d_v \\leq \\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ 的點就好，因為如果 LCS 的一部分存在於比 $\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ 更深的地方，那跟上面的點交換也必定能滿足，並且需要的 label 個數只會更小或不變。

令 $cnt_i$ 表示 $d_u=i$ 的點有多少個，$x$ 表示 $d_v>\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ 的點有多少個。

因為那些深度超過 $\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ 的點放什麼都可以，所以檢查 $cnt$ 能不能恰好湊出 $[k-x,k]$ 之間至少一個數字，如果可以則答案為 $\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)$ ，否則為 $\\displaystyle\\min_{u\\in \\text{leaf}}(d_u)-1$ 。

subset sum 的部份用 `bitset`， 時間複雜度 $O(\\frac{n ^ 2}{64})$ 。


[AC Code](https://codeforces.com/contest/2138/submission/366443790)
