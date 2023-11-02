# 小组会——离散选择模型(二)


***经典消费者离散选择模型介绍(第二期)***

<!--more-->

## 1 Gumble 分布：
广义极值分布：
$$
P(X< x)=\exp(-[1+k(\frac{x-\mu}{\sigma})]^{-\frac{1}{k}})
$$
当 $k\rightarrow 0$ 时，分布成为gumbel分布，也叫做第一类极值分布，此时分布函数趋于双指数形式
$$
P(X< x)=\exp(-\exp[-\frac{x-\mu}{\sigma}])
$$

- mode is $\mu$
- affine transformation $\alpha x+\beta \sim gumble(\alpha \mu +\beta,\sigma/\alpha)$
- $\varepsilon_1 \sim gumble(\mu_1,\sigma)$ and $\varepsilon_2 \sim gumble(\mu_2,\sigma)$, then 

$$
\varepsilon_1-\varepsilon_2 \sim logistics(\mu_1-\mu_2,\sigma)\quad \max\{\varepsilon_1,\varepsilon_2\} \sim gumble(\frac{1}{\sigma}log(e^{\sigma \mu_1}+e^{\sigma \mu_2}),\sigma)
$$
____

1. assortment problem under MNL
2. pricing problem under MNL
3. assortment problem with display location effects
4. assortment problems with product precedence constraints
5. quality consistent pricing problems

这五种情况下的 constraint matrix 都是全单模的，即都可以将整数规划松弛为相应的线性规划
___

## 2 MNL的优点
- The parameters of MNL has a concave log likelihood function

Its prototype is Luce model.
$$
P(i|z,\theta)=v(z_i,\theta)/\sum_{j=1}^Jv(z_j,\theta)
$$

### 2.1 Assortment Problem under MNL

Maximiza the expected revenue obtained from each customer. Yielding the problem

<div>
$$
\begin{aligned}
  z^*=& \max_{x\in \{0,1\}^{|N|}}\frac{\sum_{j\in N}r_jv_jx_j}{1+\sum_{j\in N}v_jx_j} \\
  s.t.\quad & \sum_{j\in N}a_{ij}x_j\leq b_i \quad \forall i\in M
\end{aligned}
$$
</div>

The problem is equivalent to

<div>
$$
\begin{aligned}
  & \max \quad  \sum_{j\in N}r_jw_j \\
   s.t. \quad &  \sum_{j\in N}w_j+w_0=1 \\
   & \sum_{j\in N}a_{ij}\frac{w_j}{v_j}\leq b_iw_0 \quad \forall i\in M \\
   & 0\leq \frac{w_j}{v_j}\leq w_0 \quad \forall j\in N
\end{aligned}
$$
</div>

### 2.2 Quality Consistent Pricing
The problem
$$
\max \frac{\sum_{j\in N}\sum_{k\in K}r_kv_{jk}x_{jk}}{1+\sum_{j\in N}\sum_{k\in K}v_{jk}x_{jk}}
$$

subject to constraints 
<div>
$$
\begin{aligned}
  x_{j1}+z_{j1} & =x_{j-1,1} \\
  x_{jk}+z_{jk} & =x_{j-1,k} + z_{j,k-1} \\
  x_{jm} & =x_{j-1,m}+z_{j,m-1} 
\end{aligned}
$$
</div>


### 2.3 Iterative constraint generation

<div>
$$
\begin{aligned}
  \min \quad & t  \\
  s.t. \quad &  f(x)-tg(x)\leq 0 \quad \forall x\in \mathcal{F}
\end{aligned}
$$
</div>

- At iteration $k$, consider a subset $\mathcal{F}^k$ of the constraints
- Solving problem $\min\{t: f(x)-tg(x)\leq 0\ \forall x\in \mathcal{F}^k\}$ and get the solution $t^k$
- Solving the constaint generation subproblem $\max_{x\in \mathcal{F}}f(x)-t^kg(x)$ to get the solution $x^k$
  - if $f(x^k)-t^kg(x^k)> 0$, then the solution $t^k$ is violated to the problem. Need to consider $\mathcal{F}^{k+1}=\mathcal{F}^k \cup x^k$ and proceed the next iteration $k+1$
  - if $f(x^k)-t^kg(x^k)\leq 0$, then $t^k$ is the optimal solution.

If $f(\cdot)$ and $g(\cdot)$ are linear function and constraints matrix in $\mathcal{F}$ is total unimodular, the optimal value can be obtained by linear problem.

<div>
$$
\begin{aligned}
  \min \quad & t \\
  s.t. \quad & \sum_{i\in M}b_i\mu_i +\sum_{j\in N}\eta_j +f_0-tg_0 \leq 0  \\
  & \sum_{i\in M}a_{ij}\mu_i+\eta_j\geq f_j-tg_i  \quad  \forall j\in N  \\
  & \mu_i,\eta_j \geq 0 \quad \forall i\in M,j\in N
\end{aligned}
$$
</div>

## 3 Other Choice Model

### 3.1 Multinomial-Probit (MP) Model

From the random-utility model, and assume the utilities of alternatives to have a multivariate normal distribution.

### 3.2 Elimination-by-Aspects Model

Each alternative can be viewed as owning a set of aspects. Consumer selects an aspect at random, eliminates available alternatives which fail to own this aspect.

![decision tree](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image101.jpg)

$$
P(1|1,2,3)=\frac{v_1}{v_1+v_2+v_3+v_4}+\frac{v_4}{v_1+v_2+v_3+v_4}\frac{v_1}{v_1+v_2}
$$

### 3.3 Generalized Extreme-Value Model

Different from Luce model, GEV model considers nonindependent extreme value distributions.
$$
P(1|1,2,3)=\frac{(v_1^{1/\rho}+v_2^{1/\rho})^\rho}{(v_1^{1/\rho}+v_2^{1/\rho})^\rho+v_3}\frac{v_1^{1/\rho}}{v_1^{1/\rho}+v_2^{1/\rho}}
$$

All parameters of GEV model can be estimated by the empirically practical  method of multinomial-logit estimation at each of the two nested levels of the decision tree.

## 4 Dynamic optimization problem

The parameters of the logit model are unknown and must be estimated from data.

### 4.1 Multi-armed Bandit Problem (MBP)

MBP问题的难点是Exploitation-Exploration(E&E)两难的问题：对已知的吐钱概率比较高的老虎机，应该更多的去尝试(exploitation)，以便获得一定的累计收益；对未知的或尝试次数较少的老虎机，还要分配一定的尝试机会（exploration），以免错失收益更高的选择，但同时较多的探索也意味着较高的风险（机会成本）。

### 4.2 STATIC MNL algorithm

The profit optimization problem
$$
Z=\max\{\frac{\sum_{i\in S}w_iv_i}{1+\sum_{i\in S}v_i}: S\subseteq N \ \text{and}\ |S|\leq C\}
$$

is equivalent to

<div>
$$
\begin{aligned}
  Z = & \max\{\lambda\in R:\exists X\subseteq N,|X|\leq C, f(X)\geq \lambda\}  \\
  & = \max\{\lambda\in R:\max_{X:|X|\leq C} \sum_{i\in X}v_i(w_i-\lambda)\geq \lambda\}
\end{aligned}
$$
</div>

Define a class of linear functions:

<div>
$$
\begin{aligned}
  h_0(\lambda) & =0 \\
  h_i(\lambda) & =v_i(w_i-\lambda)
\end{aligned}
$$
</div>

there is at most $C_{N+1}^2$ intersection points among them. For any $\lambda$ between two consecutive intersection points, the ordering of the $h_j(\lambda)=v_j(w_j-\lambda)$ is constant. Therefore, to enumerate $\mathop{\arg\max}_{X:|X|\leq C}\sum_{i\in X}v_i(w_i-\lambda)$ for all $\lambda \in R$, it suffices to enumerate all intersection points. And the time complexity of STATIC MNL algorithm is $O(N^2)$.

> As long as the estimated orderings coincide with the true orderings, then the output of the STATIC MNL will be exactly the same as if the true $\pmb{v}$ is known

- If the capacity $C$ is fixed, finding the optimal assortment only need to search through $O(N)$ assortments, which is on the same order as the uncapacitated optimization problem.

## 5 Single-leg reserve management problem

Customer choice behavior, such as buy-up and but-down, is an important phenomenon in a wide range of revenue management contexts.

A basic and simple assumption: customer demand for each of the fare products is completely indenpendent of the controls being applied by the seller.

### 5.1 Optimization
The value function $V_t(x)$ as the maximum expected revenue obtainable from periods $t,t-1,...,1$ with $x$ inventory units remaining.

<div>
$$
\begin{aligned}
  V_t(x)  = & \max_{S\subseteq N}\{\sum_{j\in S}\lambda P_j(S)(r_j+V_{j-1}(x-1) )+ (\lambda P_0(S)+1-\lambda)V_{t-1}(x)\}  \\
  = & \max_{S\subseteq N}\{\sum_{j\in S}\lambda P_j(S)(r_j-(V_{t-1}(x)-V_{t-1}(x-1)))\} + V_{t-1}(x) \\
  = & \max_{S\subseteq N}\{\lambda (R(S)-Q(S))\Delta V_{t-1}(x)\} + V_{t-1}(x)
\end{aligned}
$$
</div>

the optimal set $S$ is an efficient set, and can be search in problem

<div>
$$
\begin{aligned}
  \max \quad & \sum_{S\subset N}\alpha(S)R(S) \\
  s.t. \quad & \sum_{S\subseteq N} \alpha(S)Q(S)\leq Q(T) \\
  & \sum_{S\subseteq N}\alpha(S) =1 \quad \alpha(S) \geq 0
\end{aligned}
$$
</div>

### 5.2 Nested-by-fare property

Complete set: $S=\{1,\dots,k\}$.

Under independent demand model (IDM)、multinomial logit model (MNL) and a model where a customer purchases the lowest open fare, the optimal policy is nested by fare order.

### 5.3 Estimation

The choice probabilities: $P_j(S)=P_j(z,\beta,S)$.

For MNL model, the mean utility $u_i=\beta^T z_i$. 根据历史数据估计 $\beta$ 和顾客到达率 $\lambda$.

The log-likelihood function for the MNL model has closed-form first and second partial derivatives and is jointly concave.

The problem is that a period without an arrival and a period in which there was an arrival but without purchase is impossible to distinguish. Thus, EM method can overcome this problem.

## 6 Multiproduct Price Optimization Under NL Model

The monopolist's problem under the NL model is to maximize the expected total profit
$$
R(\pmb{P})=\sum_{i=1}^n \sum_{j=1}^{m_i}(p_{ij}-c_{ij})\pi_{ij}(\pmb{P})
$$

$$
Q_i(\pmb{P})=\frac{(\sum_{s=1}^{m_i}e^{\alpha_{is}-\beta_{is}p_{is}})^{\gamma_i}}{1+ \sum_{l=1}^n (\sum_{s=1}^{m_l}e^{\alpha_{ls}-\beta_{ls}p_{ls}})^{\gamma_l}} \quad q_{j|i}(\pmb{p_i})=\frac{e^{\alpha_{ij}-\beta_{ij}p_{ij}}}{\sum_{s=1}^{m_i}e^{\alpha_{is}-\beta_{is}p_{is}}}
$$

$$
\pi_{ij}(\pmb{P})=Q_i(\pmb{P})\cdot q_{j|i}(\pmb{p_i})
$$

### 6.1 Constant Adjusted Markup

Suppose there are product-differentiated price sensitivities, then let the adjusted markup $\theta_{i}=p_{ij}-c_{ij}-1/\beta_{ij}$, and the average profit of nest $i$ is $\sum_j^{m_i}(\theta_i+1/\beta_{ij})q_{j|i}(\theta_i)=\theta_i+w_i(\theta_i)$. Consider arbitrary nest coefficients, let $\phi= \theta_i+(1-1/\gamma_i)w_i(\theta_i)$. Then the problem is 
$$
R(\phi)=\sum_{i=1}^n Q_i(\theta)\phi
$$

{{< admonition >}}

If for each nest $i$, $\gamma_i \geq 0$ or $\max_s \beta_{is}/\max_s \beta_{is}\leq 1/(1-\gamma_i)$

Then this problem is unimodal in $\phi$, and the optimal prices can be easily found by serveral well-known algorithms, such as 二分查找法、黄金分割搜索.etc.

{{< /admonition >}}

### 6.2 Oligopolistic Competition

Consider each firm controls a nest of multiple products. 

The price competition game as
$$
R_i(\pmb{P_i},\pmb{P_{-i}})=\sum_{j=1}^{m_i}(p_{ij}-c_{ij})\cdot \pi_{ij}(\pmb{P})
$$

The log-supermodular game as
$$
R_i(\theta_i,\theta_{-i})=Q_i(\pmb{\theta})(\theta_i + w_i(\theta_i))
$$

在 condition 1 下，$R_i(\theta_i,\theta_{-i})$ is quasi-concave in $\theta_i$，博弈存在纳什均衡.

