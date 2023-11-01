# 小组会---近似算法介绍


***2023-10-13 小组会***

<!--more-->

## Introduction to Approximation Algorithms

*The difficulty of sifting through large amounts of data in order to make an informed choice is ubiquitous in todays's society*


P=NP $\Rightarrow$ efficient algorithm: polynomial in input size

- find optimal solutions (***relaxation***)
- in polynomial time
- for any instance

---
> ***Definition:*** An $\alpha$-approximation algorithm for an optimization problem is a polynomial-time algorithm that for all instances of the problem produces a solution whose value is with a factor of $\alpha$ of the value  of an optimal solution.

> ***Definition:*** A polynomial-time approximation scheme (PTAS) is a family of algorithms $\{A_\epsilon\}$, where there is an algorithm for each $\epsilon>0$, such that $A_\epsilon$ is a $(1+\epsilon)$-approximation algorithm (for minimization problems).

> ***Theorem:*** For any MAX SNP-hard problem, there does not exist a PTAS, unless P=NP.

---

{{< admonition tip >}}

The aims is mathematical rigor in the analysis of our algorithms, content with notion of worst-case analysis. The worst-case bounds are often due to pathological cases that do not arise in practice, so that approximation algorithms often give rise to heuristics that return solutions much closer to optimal than indicated.

{{< /admonition >}}

### The Set Cover Problem

***Set Cover Problem:*** Given a ground set of elements $E=\{e_1,e_2,...,e_n\}$, some subsets of those elements $S_1,...,S_m$ where each $S_j\subseteq E$, and a nonnegative weight $w_j\geq 0$ for each subset $S_j$. The goal is to find a minimum-weight collection of subset that covers all of $E$

\begin{align*}
    \text{minimize} \quad & \sum_{j\in I} w_j \\
    \text{subject to}\quad & \bigcup_{j\in I} S_j=E \\
    & I\subseteq \{1,...,m\}
\end{align*}

- the development of an antivirus product;
- the vertex cover problem


$$
Z_{IP}^*=OPT
$$

> **NP-hard** : non-polynomial time solvable

LP-relaxation: $Z_{LP}^*< Z_{IP}^*$

#### Deterministic Rounding Algorithm

Obtain the LP solution $x^*$, include subset $S_j$ if $x_j\geq 1/f$, where $f$ is the maximum number of sets in which any emelemt appers.
$$f=\max_{i=1,\dots,n} |\{j:e_i\in S_j\}|$$

> ***Lemma:*** The collection of subsets $S_j$, $j\in I$, $I=\{j: x_j^*\geq 1/f\}$, is a set cover.

> ***Theorem:*** The rouding algorithm is an $f$-approximation algorithm for the set cover problem.

#### Rounding a Dual Solution

Each element $e_i$ is charged a price $y_i\geq 0$

\begin{align*}
    \text{maximize}\quad & \sum_{i=1}^n y_i\\
    \text{subject to}\quad & \sum_{i:e_i\in S_j} y_i \leq w_j, \quad j=1,\dots,m \\
    & y_i\geq 0
\end{align*}

- *weak duality:* $\sum_{i=1}^n y_i \leq Z_{LP}^* \leq OPT$
- *strong duality:* $\sum_{j=1}^m w_j x_j^* = \sum_{j=1}^n y_j^*$

Obtain the dual LP solution $y^*$, choose all subsets for which the corresponding dual inequality is tight.

> ***Lemma:*** The collection of subsets $S_j$, $j\in I'$, $I'=\{j:\sum_{i:e_i\in S_j} y_i^* = w_j\}$, is a set cover.

> ***Theorem:*** The dual rouding algorithm is an $f$-approximation algorithm for the set cover problem.

- *complementary slackness*: 
$$
\sum_{i=1}^n y_i \leq \sum_{i=1}^n y_i \sum_{j:e_i\in S_j} x_j = \sum_{j=1}^m x_j \sum_{i:e_i\in S_j} y_i \leq \sum_{j=1}^m x_j w_j
$$

#### The Primal-dual Method

Primal-dual algorithm
- $y\leftarrow 0$
- $I\leftarrow \varnothing$
- **While** there exists $e_i\notin \bigcup_{j\in I} S_j$ **do**
  - Increase the dual variable $y_i$ until there is some $l$ with $e_i\in S_l$ such that 
  - $$ \sum_{j:e_j\in S_l} y_j=w_l $$
  - $I\leftarrow I\cup \{l\}$

Increase  $y_i$ by $\min_{j:e_i\in S_j} \left(w_j- \sum_{k:e_k\in S_j} y_k \right)$

> ***Theorem:*** The Primal-dual algorithm is an $f$-approximation algorithm for the set cover problem.

#### The Greedy Algorithm

Greedy algorithm (*most bang for the buck*)

- $I\leftarrow \varnothing$
- $\hat{S}_j \leftarrow S_j, \quad \forall j$
- **While** $I$ is not a set cover **do**
  - $l\leftarrow \arg\min_{j:\hat{S}_j\neq \varnothing} w_j/|\hat{S}_j|$
  - $I\leftarrow I\cup \{l\}$
  - $\hat{S}_j\leftarrow \hat{S}_j - S_l$

at $k^{th}$ iteration
$$
\min_{j:\hat{S}_j} \frac{w_j}{|\hat{S}_j|} \leq \frac{\sum_{j\in O}w_j}{\sum_{j\in O}|\hat{S}_j|} = \frac{OPT}{\sum_{j\in O}|\hat{S}_j|}\leq \frac{OPT}{n_k}
$$

$$\Downarrow$$

$$
w_j\leq \frac{n_k-n_{k+1}}{n_k} OPT
$$

$$\Downarrow$$

$$
\sum_{j\in I}w_j\leq \sum_{k=1}^l \frac{n_k-n_{k+1}}{n_k} OPT \leq OPT \sum_{k=1}^l \left( \frac{1}{n_k} + \frac{1}{n_k-1}+\cdots+\frac{1}{n_{k+1}+1} \right)
$$

> ***Theorem:*** The greedy algorithm is an $H_n$-approximation algorithm for the set cover problem.

> ***Theorem:*** The greedy algorithm returns a solution indexed by $I$ such that $\sum_{j\in I}w_j \leq H_g Z_{LP}^*$, where $g=\max_j |S_j|$.

> ***Theorem:*** If there exists a $c\ln n$-approximation algorithm for the unweighted set cover problem for some constant $c<1$, then there is an $O(n^{O(\log\log n)})$-time deterministic algorithm for each NP-complete problem.

> ***Theorem:*** There exists some constant $c>0$ such that if there exists a $c\ln n$-approximation algorithm for the unweighted set cover problem, then P=NP.

> ***Theorem:*** If there exists an $\alpha$-approximation algorithm for the vertex cover problem with $\alpha< 10\sqrt{5}-21 \approx 1.36$, then P=NP.

> ***Theorem:*** Assuming the unique games conjecture, if there exists an $\alpha$-approximation algorithm for the vertex cover problem with constant $\alpha<2$, then P=NP.

#### A Randomized Rounding Algorithm

$$
E\left[ \sum_{j=1}^m w_j X_j \right] = \sum_{j=1}^m w_j \Pr[X_j=1] = \sum_{j=1}^m w_j x_j^* = Z_{LP}^* \leq OPT
$$

- the probability that $e_i$ is not covered: 
$$
\prod_{j:e_i\in S_j} (1-x_j^*) \leq  \prod_{j:e_i\in S_j} e^{-x_j^*} \leq e^{-1}
$$

An algorithm works with *high probability*: chance of failure is at most $n^{-c}$ for any constant $c$

For each subset $S_j$, consider a coin that comes up heads with probability $x_j^*$, and flip the coin $c\ln n$ times. If it comes up heads in any of the $c\ln n$ trials, then include $S_j$ in the solution.

$$
\prod_{j:e_i\in S_j} (1-x_j^*)^{c\ln n} \leq  \frac{1}{n^c}
$$

> ***Theorem:*** The algorithm is a randomized $O(\ln n)$-approximation algorithm that produces a set cover with high probability.

$$
E\left[ \sum_{j=1}^m w_j X_j \right] = \sum_{j=1}^m w_j \left(1- (1-x_j^*)^{c\ln n} \right) \leq \sum_{j=1}^m w_j (c\ln n) x_j^*
$$
