# 优化问题经典算法(一)——Simplex Algorithm


***经典单纯形算法***

<!--more-->

单纯形法是求解线性规划问题最常用、最有效的算法之一。单纯形法最早由 George Dantzig 于1947年提出。如果线性规划问题的最优解存在，则一定可以在其可行区域的顶点中找到。基于此，单纯形法的基本思路是：先找出可行域的一个顶点，据一定规则判断其是否最优；若否，则转换到与之相邻的另一顶点，并使目标函数值更优；如此下去，直到找到某最优解为止。

## 1 线性规划的标准形式


\begin{align*}
    \min \quad& c^Tx \\
    s.t. \quad & Ax\leq b \\
    & x\geq 0
\end{align*}


对于非标准的线性规划
- 如果是 max，则乘 $-1$ 后求 min
- 如果存在 $=$ 约束，则转为 $\geq$ 和 $\leq$
- 对于 $\leq$ 约束，乘 $-1$ 后转为 $\leq$
- 如果存在负变量，则用 $x'-x''$ 替代，其中 $x',x''\geq 0$

在迭代时，需要注意可能在几次迭代中函数的值并没有产生变化。这种情况被称为退化 (Degeneracy)，退化有可能会导致单纯形法无法终止，而产生循环 (cycling)。

在《算法导论》中对退化和循环提到
> Degeneracy can prevent the simplex algorithm from terminating, because it can lead to a phenomenon known as cycling: the slack forms at two different iterations of SIMPLEX are identical. Because of degeneracy, SIMPLEX could choose a sequence of pivot operations that leave the objective value unchanged but repeat a slack form within the sequence. Since SIMPLEX is a deterministic algorithm, if it cycles, then it will cycle through the same series of slack forms forever, never terminating.

对此，有两个避免退化的方法：
- 在选择换入变量和换出变量时，总选择满足条件的下表最小的
- 加入随机扰动

## 2 无界(unbounded) 情况

对于无界的线性规划，目标函数可以无限制的减小，体现在单纯形法中则是某个换出变量可以无限制增大而不违反任何约束，即不存在换入变量。

## 3 单纯形法实现

对于初始问题，将其松弛为

\begin{align*}
    \min \quad& -x_1-14x_2-6x_3  & \\
    s.t. \quad & x_1+x_2+x_3+x_4 & =4 \\
    & x_1 \hspace{7em} +x_5 & =2 \\
    & \hspace{4.5em} x_3 \hspace{5em} +x_6 & =3 \\
    & \hspace{1.8em} 3x_2 + x_3 \hspace{7.5em} +x_7 & =6 \\
    & x_1,\hspace{0.9em} x_2, \hspace{0.8em} x_3, \hspace{0.6em} x_4, \hspace{1.2em} x_5, \hspace{1.1em} x_6, \hspace{1em} x_7 & \geq 0
\end{align*}


可以得到下面的矩阵

$$
C=
\left(\begin{matrix}
    -1 & -14 & -6 & 0 & 0 & 0 & 0
\end{matrix}\right)
$$

$$
B=
\left(\begin{matrix}
    4 \\ 2 \\ 3 \\ 6
\end{matrix}\right)
\quad A=
\left(\begin{matrix}
    1 & 1 & 1 & 1 & 0 & 0 & 0 \\
    1 & 0 & 0 & 0 & 1 & 0 & 0 \\
    0 & 0 & 1 & 0 & 0 & 1 & 0 \\
    0 & 3 & 1 & 0 & 0 & 0 & 1 \\
\end{matrix}\right)
$$

将其合并成矩阵

$$
S_1=
\left(\begin{matrix}
     C \\
    B \quad A
\end{matrix}\right)
$$


其中，$S_1[0][0]$ 为目标值 $z=0$。

接下来寻找换入换出变量，将矩阵 $S_1$ 写为基变量 $=$ 非基变量的形式


\begin{align*}
    z &= -x_1-14x_2-6x_3 \\
    x_4 & = 4-x_1-x_2-x_3 \\
    x_5 &= 2-x_1 \\
    x_6 & =3-x_3 \\
    x_7 & =6-3x_2-x_3
\end{align*}


目标值 $z$ 等于所有非基变量为 $0$ 时的最小值。找到换入变量 $x_2$，因为令 $x_2$ 增大能更大程度的使目标值 $z$ 减小。对于四个基变量约束条件，可以得到约束最紧的为 $x_7$。将所有的换入变量 $x_2$ 替换为 $2-x_7/3-x_3/3$，可以得到


\begin{align*}
    z &= -28-x_1+\frac{14}{3}x_7-\frac{4}{3}x_3 \\
    x_4 & = 2-x_1+\frac{1}{3}x_7-\frac{2}{3}x_3 \\
    x_5 &= 2-x_1 \\
    x_6 & =3-x_3 \\
    x_2 & =2-\frac{1}{3}x_7-\frac{1}{3}x_3
\end{align*}


此时的矩阵表示为

$$
S_2=
\left(\begin{matrix}
    -28 & -1 & 0 & -4/3 & 0 & 0 & 0 & 14/3 \\
    2 & 1 & 0 & 2/3 & 1 & 0 & 0 & -1/3 \\
    2 & 1 & 0 & 0 & 0 & 1 & 0 & 0 \\
    3 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\
    2 & 0 & 1 & 1/3 & 0 & 0 & 0 & 1/3 \\
\end{matrix}\right)
$$

$S_1$ 变为 $S_2$ 的过程可以表示为：对第五行，有 $S_2[4][j]=S_1[4][j]/S_1[4][2]$；对其他行，有
$$
S_2[i][j]=S_1[i][j]-S_1[i][2]\cdot S_2[4][j]
$$

接下来寻找下一对换入换出变量，直到在目标函数中，即第一行中没有负数，迭代停止。注意，如果存在 $S_1[4][2]<0$，则说明是无界解。

## 4 初始解 $\neq$ 可行解

但是上述的步骤会出现问题，如果有某一分量 $b_j<0$，则初始解为非可行解。例如

\begin{align*}
    \min \quad & x_1+2x_2 & \\
    s.t. \quad & x_1+x_2 &\leq 2 \\
    & x_1+x_2 &\geq 1 \\
    & x_1,x_2 &\geq 0
\end{align*}

此时初始解为 $X=\{0,0,2,-1\}$ 不是可行解。在本例中，由于目标函数中不存在负分量，迭代直接停止。所以需要找到初始基可行解。

## 5 初始化

在上述的例子中，构造一个辅助线性规划 (auxiliary linear program)，如下

\begin{align*}
    \min \quad & x_0 && \\
    s.t.\quad & x_1+x_2 - x_0 && \leq 2 \\
    & -x_1 - x_2 - x_0 && \leq -1 \\
    & x_1,x_2,x_0 && \geq 0
\end{align*}

如果这个辅助线性规划 $L_{aux}$ 最优解为 $0$，则证明原线性规划问题 $L$ 有解。否则，原问题也不存在最优解。

{{< admonition tip "证明" false >}}

Suppose that $L$ has a feasible solution $\bar{x}$. Then the solution $x_0=0$ combined with $\bar{x}$ is a feasible solution to $L_{aux}$ with objective value $0$. Since $x_0\geq 0$ is a constraint of $L_{aux}$ and the objective function is to minimize $x_0$, this solution must be optimal for $L_{aux}$.

Conversely, suppose that the optimal objective value of $L_{aux}=0$. Then $x_0=0$, and the remaining solution values of $\bar{x}$ satisfy the constraints of $L$.

{{< /admonition >}}

将 $L_{aux}$ 松弛之后，将 $x_0$ 作为换入变量，并且选择 $\min\{b_i\}$ 的一行作为换出变量。因为在 $L_{aux}$ 中 $x_0$ 的系数为 $-1$，这表示在换入 $x_0$ 时，矩阵的每一行都会减去 $\min \{b_i\}$。因为最小的 $b_i$ 为负，所以能够保证在将 $x_0$ 换入之后的解为可行解。

如果能够得到 $L_{aux}$ 的最优值为 $0$，则可以用最终 $L_{aux}$ 的基变量替换原问题的基变量，即直接将矩阵中含有 $x_0$ 的列去掉 (**如果 $x_0$ 是基变量，则将其与任意非基变量进行换出**)，并修改目标函数行

$$
S=
\left(\begin{array}{c|r|rrrr}
    0 & 1 & 0 & 0 & 0 & 0 \\
    1 & -2 & 0 & 0 & 1 & 1 \\
    1 & 1 & 1 & 1 & 0 & -1 \\
\end{array}\right)\Rightarrow
\left(\begin{matrix}
    1 &  1 & 2 & 0 & 0 \\
    1 &  0 & 0 & 1 & 1 \\
    1 &  1 & 1 & 0 & -1 \\
\end{matrix}\right)
$$

## 6 代码实现

```python
import numpy as np

class Simplex(object):
    def __init__(self, obj, max_mode=False):  # default is solve min LP, if want to solve max lp,should * -1
        self.mat, self.max_mode = np.array([[0] + obj]) * (-1 if max_mode else 1), max_mode

    def add_constraint(self, a, b):
        self.mat = np.vstack([self.mat, [b] + a])

    def _simplex(self, mat, B, m, n):
        while mat[0, 1:].min() < 0:
            col = np.where(mat[0, 1:] < 0)[0][0] + 1  # use Bland's method to avoid degeneracy. use mat[0].argmin() ok?
            row = np.array([mat[i][0] / mat[i][col] if mat[i][col] > 0 else 0x7fffffff for i in
                            range(1, mat.shape[0])]).argmin() + 1  # find the theta index
            if mat[row][col] <= 0: return None  # the theta is ∞, the problem is unbounded
            self._pivot(mat, B, row, col)
        return mat[0][0] * (1 if self.max_mode else -1), {B[i]: mat[i, 0] for i in range(1, m) if B[i] < n}

    def _pivot(self, mat, B, row, col):
        mat[row] /= mat[row][col]
        ids = np.arange(mat.shape[0]) != row
        mat[ids] -= mat[row] * mat[ids, col:col + 1]  # for each i!= row do: mat[i]= mat[i] - mat[row] * mat[i][col]
        B[row] = col

    def solve(self):
        m, n = self.mat.shape  # m - 1 is the number slack variables we should add
        temp, B = np.vstack([np.zeros((1, m - 1)), np.eye(m - 1)]), list(range(n - 1, n + m - 1))  # add diagonal array
        mat = self.mat = np.hstack([self.mat, temp])  # combine them!
        if mat[1:, 0].min() < 0:  # is the initial basic solution feasible?
            row = mat[1:, 0].argmin() + 1  # find the index of min b
            temp, mat[0] = np.copy(mat[0]), 0  # set first row value to zero, and store the previous value
            mat = np.hstack([mat, np.array([1] + [-1] * (m - 1)).reshape((-1, 1))])
            self._pivot(mat, B, row, mat.shape[1] - 1)
            if self._simplex(mat, B, m, n)[0] != 0: return None  # the problem has no answer

            if mat.shape[1] - 1 in B:  # if the x0 in B, we should pivot it.
                self._pivot(mat, B, B.index(mat.shape[1] - 1), np.where(mat[0, 1:] != 0)[0][0] + 1)
            self.mat = np.vstack([temp, mat[1:, :-1]])  # recover the first line
            for i, x in enumerate(B[1:]):
                self.mat[0] -= self.mat[0, x] * self.mat[i + 1]
        return self._simplex(self.mat, B, m, n)
```

## 7 从几何的角度

线性规划问题的最优解在 polyhedron 的各个**顶点**上，而不需要考虑可行域内部点。在单纯形运算中，基变量即为顶点。所以需要做的就是按照一定的规则沿着边遍历顶点，直到无法继续更新了为止。

设当前的顶点为 $x$，下一个顶点为按照方向为 $\lambda$ 的边走长度 $\theta$，然后可以找到新的顶点 $x'=x+\theta\lambda$。体现在约束矩阵 $A$ 中即为用基变量的列约束的线性组合得到换入变量的列约束的权重向量。还是用最初的例子，

$$
A=(A_1;\dots;A_7)=
\left(\begin{matrix}
    1 & 1 & 1 & 1 & 0 & 0 & 0 \\
    1 & 0 & 0 & 0 & 1 & 0 & 0 \\
    0 & 0 & 1 & 0 & 0 & 1 & 0 \\
    0 & 3 & 1 & 0 & 0 & 0 & 1 \\
\end{matrix}\right)
$$

用图表示为：
![单纯形](https://cdn.jsdelivr.net/gh/Skydominate/image_bed@main/image115.jpg)

初始的顶点为 $(0,0,0,4,2,3,6)$， 此时换入变量为 $x_2$，基变量为 $x_4,x_5,x_6,x_7$。用基变量的列约束表示换入变量的列约束，即为 $A_2=A_4+3A_7$，得到 $\lambda=(0,1,0,-1,0,0,-3)$。长度 $\theta$ 即为约束最紧的值 $\theta=\min\{S_1[i][0]/S_1[i][2]:i\in [1,7]\}=2$。因此，下一个遍历的顶点为 $(0,2,0,2,2,3,0)$，即沿着换入变量 $x_2$ 的方向到了下一个顶点。

为什么可以用列的线性组合表示边的方向，可以这么理解：在确定换入变量之后，需要将换入变量的约束列变为单位矩阵的列。而 $x_i'=x_i+\theta\lambda$ 可以理解为将每个约束中的 $x_2$ 替换为相应的非基变量的组合。

___

如果可行域并不是凸紧集，则可以用其 convex hull 来代替原可行域，同样可以得出最优解。

{{< admonition tip >}}

Let $s\in D$ is the optimal solution of $\min_{y\in D}c^Ty$, in which $D=conv(V)$, $V$ is the feasible region of LP. Then there is $s=\sum_{i=1}^k\alpha_i v_i$, means that $s$ is the weighted average of some finite set of "vertices" $v_1,\dots,v_k\in V$, with $\alpha_i\geq 0,\sum_i \alpha_i=1$. By linearity of the inner product
$$
c^T s=c^T \sum_{i=1}^k\alpha_i v_i=\sum_{i=1}^k\alpha_i c^Tv_i
$$
Therefore, we must have that $c^Tv_i\leq c^Ts$ for at least one indices $i$, means that
$$
\min_{y\in D}c^Ty = c^T s \leq \min_{y\in V}c^Ty \leq c^Tv_i\leq c^Ts
$$
 $v_i$ is also the optimal solution.

 {{< /admonition >}}

## 8 单纯形的时间复杂度

在算法中，每次查找一个换出变量需要 $O(m+n)$ (即需要遍历所有松弛后的基变量与非基变量)。而对矩阵变换则需要 $O(m\cdot(m+n))$。因此在大多数情况下，单纯形为多项式时间复杂度 (polynomial time complexity)。

但是 V. Klee and G. L. Minty[1972] 构造了一个例子：

\begin{align*}
    \max \quad & x_n & & \\
    s.t.\quad & \delta & \leq x_i & \leq 1 \\
    & \delta x_{i-1} & \leq x_i & \leq 1-\delta x_{i-1} \\
    & & x_i &\geq 0
\end{align*}

在这个例子中，单纯形算法要遍历 $2^n$ 个顶点。根据这个例子，可以得到单纯形算法不是一个多项式时间复杂度的算法。2001年 Daniel A. Spielman 和 Shang-Hua Teng 提出了平滑型复杂度理论 (smoothed complexity)，解决了单纯形算法在实际运行时是多项式时间平滑复杂度的。

- Average-case analysis was first introduced to overcome the limitations of worst-case analysis, however the difficulty is saying what an average case is. The actual inputs and distribution of inputs may be different in practice from the assumptions made during the analysis.
- Smoothed analysis is a hybrid of worst-case and average-case analyses that inherits advantages of both, by measuring the expected performance of algorithms under slight random perturbations of worst-case inputs.
- The performance of an algorithm is measured in terms of both the input size, and the magnitude of the perturbations.
- If the smoothed complexity of an algorithm is low, then it is unlikely that the algorithm will take long time to solve practical instances whose data are subject to slight noises and imprecisions.

