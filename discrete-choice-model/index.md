# 小组会——离散选择模型


***经典消费者离散选择模型介绍***

<!--more-->

## 1 Basic Attraction Model (BAM) 和 Multinomial Logit Models (MNL)

- BAM 的选择概率
  
$$
\pi_j(S)=\frac{v_j}{v_0+V(S)}
$$

- MNL 是 Random Utility Model (RUM) 的一种，拥有确定的选择概率形式，同时选择概率函数的对数似然函数具有凹性。但是 MNL 假设了 RUM 中的随机项是 IID 的，当替代产品之间存在相关关系，MNL 模型就不能够给予一个很好的选择预测结果

## 2 Generalized Attraction Model (GAM)

- 在 BAM 中忽视了顾客对 $\bar{S}$ 中商品的偏好，在 GAM 引入了 shadow attraction value
$$
\pi_j(S)=\frac{v_j}{v_0+W(\bar{S})+V(S)}
$$
- IIA：各产品两两之间选择概率的比值与其他产品的效用无关

{{< admonition tip "red-bus, blue-bus paradox" false>}}

如果某人选择小汽车和巴士（假设所有的巴士都漆成红色）的概率各为0.5，两者的选择概率之比为1:1。现在设原模型中加入一半巴士漆成蓝色的选择枝。蓝巴士和红巴士完全相同，选择他们的概率为1:1。所以加入蓝巴士后，小汽车、红巴士、蓝巴士选择的概率为1:1:1，概率值都为1/3。但通常人们在进行选择时与巴士颜色无关，小汽车、巴士的选择概率仍为0.5，红蓝巴士的选择概率各为0.25，这种模型忽略了红巴士和蓝巴士的紧密相关性

{{< /admonition >}}

## 3 Nested Logit (NL) model

消费者选择 nest $i$ 的概率：
$$
Q_i(S_1,\dots,S_m)=\frac{V_i(S_i)^{\gamma_i}}{v_0+ \sum_{l\in M}V_l(S_l)^{\gamma_l}}
$$

产品分 nests 供给，消费者先选择 nest，然后再选择该 nest 中的产品。
- Products in the same nest are closer substitutes of each other
- If $\gamma_i=1$, the utilities of the products are uncorrelated and the NL model reduces to the MNL model

NL 模型解决了 MNL 关于无法解释各替代品之间相关性的问题，同时其极大似然函数有显式表达式，计算速度更快

前三种模型的研究主要是应用于 Assortment Optimization 和 Revenue Management

## 4 Mixtures of Basic Attraction Models

将消费者分类
$$
\pi_j(S)=\sum_{g\in G}\alpha^g \frac{v_j^g}{v_0^g+\sum_{i\in S}v_i^g}
$$
$\alpha^g$ 是到来的顾客是 type $g$ 的概率

## 5 Markov Chain Choice Model

每个消费者对产品有一个排序，当他进入系统后会优先选择排序第一的产品。如果系统没有提供该产品，则消费者会按照 Markov 转移矩阵选择其他的产品

- 产品的首选概率：$\lambda_i$
- 从 $i$ 产品转移到 $j$ 产品的概率是 $\rho_{ij}$

$$
    \pi_j(S)=\lambda_j+\sum_{i\in \bar{S}}\phi_i(S)\rho_{ij} \quad \forall j\in S
$$
$$
   \phi_j(S)=\lambda_j+\sum_{i\in \bar{S}}\phi_i(S)\rho_{ij} \quad \forall j\in \bar{S}
$$

The MC choice model can be used to approximate any discrete choice model.

Blanchet. *A Markov chain approximation to choice modeling* (2013) 证明了基于 MC 的 DCM 在数据上是任一 RUM 真实选择概率的逼近。

## 6 其他 Discrete Choice Models

- RUM：multinomial probit (MNP)、nested multinomial logit model (NMNL)、exponomial choice model (EC)
- semi-parametric choice model
- Feng. *Analysis of discrete choice models: A welfare-based framework* (2015) 提出了 welfare-based 选择模型。这种离散选择模型完全包含 RUM 模型

## 7 Assortment Optimization

We consider the so-called static assortment optimization problem, where inventories of the products is not a limiting concern.

- 空间限制：提供商品的数量有限
- 优先关系：一个产品被提供的前提是另一间产品被提供

目标：
$$
R(S,z)=\sum_{j\in N}(p_j-z)\pi_j(S)
$$
$$
\mathcal{R}(z)=\max_{S\subset N}R(S,z)
$$
通过 DCM 得到消费者购买产品的概率 $\pi_j(S)$

Problem is formulated as
$$
Q(\rho)=\max \quad \sum_{S\subset N}R(S)t(S)
$$
which subject to
$$
\sum_{S\subset N}\Pi(S)t(S)< \rho \quad \text{and} \quad \sum_{S\subset N}t(S)=1
$$

> An assortment $E\subset N$ is said be to *efficient* if $Q(\Pi(E))=R(E)$

The dual formulation is
$$
Q(\rho)=\min_{z\geq 0}\{\mathcal{R}(z)+\rho z\}
$$
For its solution $z(\rho)$
$$
\mathcal{R}(z(\rho))\geq R(S,z(\rho))
$$

efficient set 可以减少枚举空间 $S\subset N$

Customer choice model:
- BAM
  
$$
\mathcal{R}^*=\max_{S\subset N}R(S)=\max_{S\subset N} \{ \frac{\sum_{j\in S}p_jv_j}{v_0+\sum_{j\in S}v_j} \}
$$
$$
v_0\mathcal{R}^*\geq \sum_{j\in S}(p_j-\mathcal{R}^*)v_j  \rightarrow \max_{S\subset N} \{ \sum_{j\in S}(p_j-\mathcal{R}^*)v_j  \}
$$
The optimal solution is <em>nested-by-revenue</em> assortment: $E_j=\{1,\dots,j\}$

For GAM, regards revenue of product $j$ as $p_jv_j/(v_j-w_j)$, attraction value of $j$ as $(v_j-w_j)$ and no-purchase alternative as $v_0+w(N)$

For mixture of BAMs, the problem is NP-complete

- NL model

<div>
$$
\mathcal{R}^*=\max_{\substack{ (S_1,\dots,S_m): \\ S_i\subset N \ \forall i \in M }}R(S_1,\dots,S_m)=\max_{\substack{ (S_1,\dots,S_m): \\ S_i\subset N \ \forall i \in M }} \{ \frac{\sum_{i\in M}R_i(S_i)V_i(S_i)^{\gamma_i}}{v_0+\sum_{i\in M}V_i(S_i)^{\gamma_i}} \}
$$
</div>
$$
\sum_{i\in M}f_i(x_i)-\mathcal{R}^*\sum_{i\in M}g_i(x_i)\leq \mathcal{R}^*v_0,\quad \forall x_i\in \{0,1\}^n
$$
in which $x_i=\{x_{i1},\dots,x_{in}\}\in \{0,1\}^n$ an incidence vector。Let $V_i(x_i)=\sum_{j\in N}v_{ij}x_{ij}$

The expected value can be solved
$$
\mathcal{R}^*=\min_{z,y}z
$$
which subject to $\sum_{i\in M}y_i\leq v_0z$ and $f_i(x_i)-zg_i(x_i)\leq y_i$, $\forall x_i\in \{0,1\}^n$

Let $u_i^\*=z+(1-\gamma_i)[R_i(x_i^\*)-z]^+$, the optimal solution of problem
$$
\max_{x_i\in \{0,1\}^n}\{V_i(x_i)R_i(x_i)-u_i^*V_i(x_i)\} \rightarrow \max_{x_i\in \{0,1\}^n}\{\sum_{j\in N}v_{ij}(p_{ij}-u_i^*)x_{ij}\}
$$
is the optimal solution of problem $\max_{x_i\in \{0,1\}^n}\{V_i(x_i)^{\gamma_i}R_i(x_i)-zV_i(x_i)^{\gamma_i}\}$

Nested-by-revenue assortment in each nest is optimal

- MC choice model

The expected revenue from customer is
$$
g_j=\max\{p_j,\sum_{i\in N}\rho_{ji}g_i\}
$$
The problem is $\sum_{j\in N}\lambda_jg_j$

The optimal set is not nested-by-revenue

## 8 Constrained Assortment Optimization

- Such constraints may limit the number of products that can be offered.

- Impose precedence relationships on the products such that a product can only be offered if some other products are offered.

对商品供给设置限制 $\sum_{j\in N}a_{ij}x_j\leq b_i$，$x_j\in \{0,1\}$

### 8.1 BAM

The problem is equivalent to $\max \sum_{j\in n}p_jy_j$, which subject to
$$
    \sum_{j\in N}y_j+y_0=1
$$
$$
    \sum_{j\in N}\frac{a_{ij}}{v_j}y_j\leq \frac{b_i}{v_0}y_0 
$$
$$
    0\leq \frac{y_j}{v_j}\leq \frac{y_0}{v_0}
$$

### 8.2 NL model

每个 nest 有限制 $\mathcal{F}_i=\{S)i\subset N : |S_i|\leq C_i\}$

Theorem 2 and Theorem 4

> ***Lemma 3 (Gallego 2014)*** &ensp; Let $(S_1^* , \dots ,S_m^* )$ be an optimal solution to problem (1) with the objective value $Z^*$ and set $u_i^*=\max\{Z^*,\gamma_i Z^*+ (1-\gamma_i)R_i(S_i^*)\}$ for all $i\in M$. If the assortments $\hat{S}_i,i\in M$ satisfy
> 
> <div> $$ \alpha V_i(\hat{S}_i)(R(\hat{S}_i)-u_i^*)\geq \max_{S_i\in \mathcal{F}_i}\{V_i(S_i)(R_i(S_i)-u_i^*)\} $$ </div>
> 
> for some $\alpha\geq 1$, then $\alpha R(\hat{S}_1,\dots,\hat{S}_m)\geq Z^*$

Let $ u_i^* = z + ( 1 - \gamma_i) [ R_i ( x_i^* )-z]^+$, the optimal solution of problem
$$
\max_{x_i\in \mathcal{F}_i}\{V_i(x_i)R_i(x_i)-u_i^*V_i(x_i)\} \rightarrow \max_{x_i\in \mathcal{F}_i}\{\sum_{j\in N}v_{ij}(p_{ij}-u_i^*)x_{ij}\}
$$
is the optimal solution of problem $\max_{x_i\in \mathcal{F}_i}\{V_i(x_i)^{\gamma_i}R_i(x_i)-zV_i(x_i)^{\gamma_i}\}$

- 将 nest 中的商品供给视为 $u_i$ 的函数，则可以将问题转化为背包问题。

$$
\max_{x_i\in \{0,1\}^n} \{ \sum_{j\in N}(p_{ij}-u_i)v_{ij}x_{ij}\quad : \quad \sum_{j\in N}x_{ij}\leq C_i  \}
$$

- 对 $f_{i,j}(u_i)=(p_{ij}-u_i)v_{ij}$，$n+1$ 条线共有 $C_{n+1}^2=(n+1)n/2$ 个交点，即共有 $C_{n+1}^2=(n+1)n/2$ 种排序。

