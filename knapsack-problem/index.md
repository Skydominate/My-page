# 小组会---Knapsack Problem


***近似算法求解复杂背包问题***

<!--more-->

## 1 model

<div>
$$
\begin{aligned}
    \text{maximize} & \sum_{i\in S}v_i \\
    s.t. & \sum_{i\in S} w_i \leq W \\
    & S\subseteq N
\end{aligned}
$$
</div>

> **Exam 1** &ensp; products $v=\{6,3,6,4,5\}$, weight $w=\{2,2,6,5,4\}$, capacity $W=10 (8)$, the optimal choice is $1,2,3 (1,2,5)$, value is $15 (14)$

{{< admonition tip "NPC问题" false >}}

采用传统的 DFS 解法产生的时间复杂度为 $O(2^n)$，DP 方法下有递推关系 
$$
V[i][W']=\max \{V[i-1][W'],V[i-1][W'-w_i]+v_i\}
$$
时间复杂度为 $O(n\cdot W)$，pseudo polynomial time solvable。当 $v_i=w_i$ 时问题等价于 subset sum problem。

{{< /admonition >}}

- 完全背包问题
- 分组背包问题
- Cardinality 约束背包问题

- $k$KP
- E-$k$KP
- $m$-DKP

Both KP and $m$-DKP are NP-hard and pseudopolynomially solvable through DP. **Whether these problems are fixed-parameter tractable.** The existence of such algorithm implies the classes FPT and W$[1]$ are equal.

## 2 Approximation algorithms (Caprara)

<div>
$$
\begin{aligned}
    \text{maximize} & \sum_{i\in S} v_i \\
    s.t. & \sum_{i\in S} w_i \leq W \\
    & |S| \leq K \\
    & S\subseteq N
\end{aligned}\quad
\begin{aligned}
    \text{maximize} & \sum_{i\in N} v_i x_i \\
    s.t. & \sum_{i\in N} w_i x_i \leq W \\
    & \sum_{i\in N} x_i \leq K \\
    & x_i\in \{0,1\}
\end{aligned}
$$
</div>

> **Lemma 1** &ensp; An optimal basic solution $x^\*$ of the LP relaxation, has at most two fractional components. Let $J_1=\{k:x_k^\*=1\}$, if the basic solution has two fractional components $x_i^\*$, $x_j^\*$ and $w_j\leq w_i$, then $\sum_{l\in J_1}v_l + v_i\geq z^\*$ and $J_1 \cup \{j\}$ is feasible

**Algorithm** $H^\frac{1}{2}$
- 计算 LP relaxation 的最优解，其中值为 1 的解的下标集合为 $J_1$，值为分数的解下标集合为 $J_F$
  - 如果 $J_F=\varnothing$，得到最优解 $S=J_1$
  - 如果 $J_F=\{i\}$，则比较 $\max\{\sum_{l\in J_1}v_l, v_i\}$ 得到最优解
  - 如果 $J_F=\{i,j\}$，其中 $w_j\leq w_i$，则比较 $\max\{\sum_{l\in J_1} v_l + v_j,v_i\}$


> $H^\frac{1}{2}$ is a $1/2-$approximation algorithm for $k$KP and runs in $O(n)$ time

**Algorithm** PTAS
- 令 $\varepsilon\leq 1/2$ 表示要求的精确度，及 $l=\min\{\lceil 1 / \varepsilon \rceil - 2, K\}$
- 考虑集合 $L$ 满足 $|L|\leq l-1$。如果有 $\sum_{i\in L}w_i \leq W$ 和 $\sum_{i\in L} v_i > z^H$。则更新 $H=L$, $z^H=\sum_{i\in L}v_i$
- 考虑集合 $L$ 满足 $|L|=l$。如果有 $\sum_{i\in L}w_i \leq W$，定义 $S=\{k\in N\setminus L:v_k \leq \min_{l\in L} v_j\}$ 和 capacity 约束 $W-\sum_{l\in L}w_i$, cardinality 限制 $K-l$，通过算法 $H^\frac{1}{2}$ 得到解 $T$ 和 $z_S^H$。如果 $\sum_{l\in L} v_l + z_S^H> z^H$, 则令 $H=L\cup T$，$z^H=\sum_{i\in L}v_i + z_S^H$
- 返回解 $H$ 和值 $z^H$

> PTAS is a PTAS for $k$KP and runs in $O(n^{\lceil 1/\varepsilon \rceil -1})$ time

### 2.1 Improved PTAS for KP

- 在第一步中，令 $l=\min\{\lceil 1/\varepsilon \rceil -2,n \}$，并将产品按照 v 增序排列
- 在第三步中，将通过算法 $H^\frac{1}{2}$ 替换为相应 KP 下的算法。并且其中的 $L$ 和其他的计算方式替换为
  - 令 $L=\{i_1,\dots, i_l\}$
  - For $i_1\in 1,\dots, n-l+1$，令 $S=\{1,\dots,i_1-1\}$
    - For $i_{l-1}=i_1+l -2,\dots, n-1$
      - For $T\subseteq \{i_1,\dots,i_{l-1}-1\}$, $|T|=l-3$
        - 令 $R=\{i_{l-1}-1,\dots,n\}$
        - 令 $i_l=R[1]$，并且计算在 $S$ 和 $W-\sum_{l\in L}w_l$ 的解
        - For $i_l=R[2],\dots,R[n-i_{l-1}]$，根据前面的解，重新计算
