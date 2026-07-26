# 半正规划的一种新型投影收缩算法











毕红*, 赵学军, 任锦神

*中国空军工程大学基础学部，西安 710038，中国

# 摘要

本文研究了一种用于半定规划问题的投影收缩算法。内点法是求解半定规划问题的经典算法。根据初始点是否可行，它可以被分为可行算法和不可行算法。可行内点法需要使用自对策略来寻找严格可行点。虽然不可行内点法不要求初始点严格可行，但该算法的理论分析非常复杂。与内点法相比，投影收缩算法对初始点没有要求，且算法简单得多。半定规划问题的最优条件可以重写为投影方程，然后通过投影收缩算法进行求解。我们提出了一种基于下降方向的新型投影收缩算法，通过求解线性方程来改进算法，从而避免高维求逆，使算法能够解决大规模半定规划问题。数值实验表明，该算法是行的，且改进算法与内点法一致。




关键词：半定规划；最优条件；投影方程；投影收缩算法

# 1. 引言

*通讯作者。电话：+86-1791789397。邮箱：bihongmei2021@163.com






考虑半定规划问题：

(P) min $C\cdot X$ s.t. $A\cdot X=b\cdot i, i=1,2,...,m, X\geq 0$。(1)

以及其对偶问题

(D) max $b^T y$ s.t. $\sum_{i=1}^m y_i A_i+S=C, S\geq 0$。(2)

为了简单起见，我们将实数对称 $n\times n$ 矩阵空间记为 $S^n$，，$S^n$ 中所有半定矩阵记为 $S^n_+$。在系统 (1) 和 (2) 中，矩阵 $C, A_i \in S^n, i=1,...,m$，向量 $b, y \in R^m$。$A\cdot B$ 表示 $A, B \in S^n$ 的内积，定义为 $A\cdot B=\text{trace}(AB)$。$X, S\geq 0$ 表示 $X, S \in S^n$。

在适当的约束限定下，原问题和对偶问题半定规划问题的解满足最优条件：

$$\begin{cases} A\cdot X=b\cdot i, i=1,2,...,m, X\geq 0 \\ \sum_{i=1}^m y_i A_i+S=C, S\geq 0 \\ XS=0 \end{cases}$$ (3)

内点法求解半定规划问题的基本思想是将互补条件 $XS=0$ 替换为互补松弛 $XS=\mu I$，其中 $I$ 是单位矩阵，参数 $\mu > 0$，从而得到中心系统：

$$\begin{cases} A\cdot X=b\cdot i, i=1,2,...,m, X\geq 0 \\ \sum_{i=1}^m y_i A_i+S=C, S\geq 0 \\ XS=\mu I \end{cases}$$ (4)

然后使用牛顿法来获取搜索方向，然而矩阵乘积通常不是可交换的，得到的搜索方向是非对称的。为了获得对称的搜索方向，需要互补松弛是对称的 [1]。近年来，求解半定规划问题的内点法侧重于新核函数的构造、宽邻域的设计以及新的搜索策略——[2–4]。这些算法要求起始点必须是严格可行的，但严格可行起始点并不容易找到。常用方法是使用 SDMM [6], SDP3 [7]，另一种方法是设计不可行算法，例如 [8]，它们不要求初始点可行，但理论分析更为复杂。

投影算法源于早期对求解变分不等式的研究。基于何兵求解变分不等式的投影收缩算法 [9] 和求解变分不等式的投影收缩算法 [10]，韩其将求解变分不等式的投影收缩扩展到半定规划 [11]。该方法将 (3) 中的相容条件转换为投影方程，然后使用投影算法求解变分不等式 [12]。郑正采用求解变分不等式的投影收缩算法 [13] 来解决某些投影问题 [14]。对于二阶规划，Mu和张 [15] 结合欧几里得几何来求解二阶规划。此外，Mu和张给半定规划的投影收缩算法。二阶规划可以看作半定规划的特例，投影收缩算法的理论分析简单，且对初始点没有要求。基于 [14]，本文提出了一种新的投影收缩算法来求解半定规划问题。与内点法相比，投影收缩算法对初始点没有要求，且算法简单得多。半定规划问题的最优条件可以重写为投影方程，然后通过投影收缩算法进行求解。我们提出了一种基于下降方向的新型投影收缩算法，通过求解线性方程来改进算法，从而避免高维求逆，使算法能够解决大规模半定规划问题。数值实验表明，该算法是行的，且改进算法与内点法一致。

# 2. 预备知识

$\Omega \subset R^n$ 为凸集，$F$ 是从 $R^n$ 到 $R^n$ 的单调算子，变分不等式是寻找 $u^* \in \Omega$ 使得：

$$(u-u^*)^T F(u^*) \geq 0, \quad \forall u \in \Omega.$$

显然，将变分不等式 (5) 中的算子 $F$ 乘以因子 $\beta > 0$ 不改变问题的解。众所周知，上述变分不等式等价于求解投影方程：

$$u = P_{\Omega}[u - \beta F(u)], \quad \beta > 0.$$

令 $e(u, \beta) := u - P_{\Omega}[u - \beta F(u)]$。特别当 $F(u) = Mu + q, q \in R^n, M \in R^{n \times n}$ 满足 $u^T Mu \geq 0$ 时，称为线性变分不等式。

以下引理表明 (3) 中的相容条件可以转换为投影的投影形式。

**定理 1[11]** 对于 $X, S \in S_+^s，$XS=0 \Rightarrow X = P_{S^s}(X-S)$。对于半定规划问题，令 $u = \begin{pmatrix} X \\ y \end{pmatrix}, M = \begin{pmatrix} 0 & -A^T \\ A & 0 \end{pmatrix}, q = \begin{pmatrix} c \\ b \end{pmatrix}, \text{其中 } A = \begin{pmatrix} A_1 \\ \vdots \\ A_m \end{pmatrix}, \text{则}$

$$[X-P_{(X,\beta)}[X-C-\sum^m y_i A_i)], \beta[A_1 \cdot X-b_1], \beta[A_m \cdot X-b_m]]begin{pmatrix} e(X, \beta) \\ e(y, \beta) \end{pmatrix}$$

$\Omega = S_+^s \times R^n$。因此，从定理1可知，半定规划的最优条件 (3) 等价于 $u = P_{\Omega}[u - \beta(Mu+q)]$。注意 $M^T = -M$，即矩阵是反对称的，在实际计算中，矩阵的



按列提取为向量以便操作。

# 3. 基于新方向的投影收缩算法

基于求解线性投影方程的一些新方法 [10]，文献 [14] 提出了一种用于二阶锥规划的快速投影收缩算法。同样，根据线性投影方程 (7) 与半正定规划问题最优条件的等价性，本文提出并改进了一种用于求解半正定规划问题的投影收缩算法。

假设方程 (7) 有解，解集记为 $\Omega^u$。

**定理 2** 令 $u' \in \Omega^u, \beta \in \{0,1\}$，则

$$(u-u')^T d(u, \beta) \geq \|e(u, \beta)\|^2, \forall u \in \mathbf{R}^{mn} \times \mathbf{R}^m$$

其中 $d(u, \beta) = (I - \beta M)e(u, \beta)$。

证明：根据闭凸集上的投影性质，我们得到

$$[P_{\Omega}(v)]^T[P_{\Omega}(v)-u^*] \geq 0, \forall v \in \mathbf{R}^{mn} \times \mathbf{R}^m. (8)$$

在 (8) 中令 $v = u-\beta(Mu+q)$，有

$$[e(u,\beta)-\beta(Mu+q)]^T[P_{\Omega}(u-\beta(Mu+q))-u^*] \geq 0. (9)$$

然后令 $v=P_{\Omega}(u-\beta(Mu+q))$，从 (5) 得到

$$[\beta(Mu+q)]^T[P_{\Omega}(u-\beta(Mu+q))-u^*] \geq 0. (10)$$

将 (9) 和 (10) 相加得

$$[e(u,\beta)-\beta M(u-u^*)]^T[P_{\Omega}(u-\beta(Mu+q))-u^*] \geq 0. (11)$$

上述不等式给出
$$(u-u^*)^T(I+\beta M)e(u,\beta) \geq \|e(u,\beta)\|^2+(u-u^*)^T\beta M(u-u^*).$$

最后，由于 $M$ 是反对对称的，证明结束。

定义 $F(u,\beta)=\frac{1}{2}\|u-u^*\|^2$，根据定理 2，可知 $d(u,\beta)$ 是 $F(u,\beta)$ 在 $G=(I+\beta M)^T(I+\beta M)$ 处的下降方向。由于 $M$ 是反对对称的，有 $G=(I-\beta M)(I+\beta M)$。显然 $G$ 是正的，则 $-G^{-1}d(u,\beta)=-(I+\beta M)^{-1}e(u,\beta)$ 也可以是一个下降方向 [9]。

## 算法 1 投影收缩算法如下。

给定 $u_0 \in \mathbf{R}^{mn} \times \mathbf{R}^m, r \in (0,2), \beta \in \{0,1\}$。

对于 $k=0,1,\dots,$，若 $u_k^* \notin \Omega^u$：

步骤 1：计算 $d(u_k,\beta)=(I+\beta M)^{-1}e(u_k,\beta)$，

步骤 2：更新 $u_{k+1} = u_k - r\beta d(u_k, \beta)$。

根据定理 2，可以给出求解半正定规划问题的投影收缩算法的全局收敛性证明。

**定理 3** $G = (I + \beta M^T)$，$r \in (0,2), \beta \in [0,1]$，算法 1 产生的序列 $\{u_k\}$ 满足

$$\|u_{k+1}-u_k\|_G^2 \leq \|u_k-u_k^*\|_G^2 - r\beta(2-\beta)\|e(u_k, \beta)\|$$

证明：$\|u_{k+1}-u_k\|_G^2 = \|(I + \beta M^T)(u_k - u_k^*) - r\beta I(I + \beta M^T)^{-1}e(u_k, \beta)\|_G^2$

$= \|(I + \beta M^T)(u_k - u_k^*)\|_G^2 \neq \|u_k-u_k^*\|_G^2 - 2r\beta(u_k-u_k^*)(I + \beta M^T)e(u_k, \beta) + r^2\beta^2 \|e(u_k, \beta)\|_G^2$

$\leq \|u_k-u_k^*\|_G^2 - 2r\beta\|e(u_k, \beta)\|$

**定理 4** [9] 算法1 产生的序列 $\{u_k\}$ 收敛于 $u_k^* \in \Omega^*$。

在算法 1 中，当计算下降方向 $d(u_k, \beta) = (I + \beta M)^{-1}e(u_k, \beta)$ 时，如果问题规模很大，$(I + \beta M)^{-1}$ 的计算成本过高，会导致算法运行缓慢。以下是等价形式：

$$d(u_k, \beta) = (I + \beta M)^{-1}e(u_k, \beta) \Leftrightarrow (I + \beta M)d(u_k, \beta) = e(u_k, \beta). (12)$$

右侧方程的特定形式为线性方程组

$$\begin{bmatrix} I_{n \times n} & -\beta A^T \\ \beta A & I_{m \times m} \end{bmatrix} \begin{bmatrix} d(X_k, \beta) \\ d(y_k, \beta) \end{bmatrix} = \begin{bmatrix} e(X_k, \beta) \\ e(y_k, \beta) \end{bmatrix}. (13)$$

求解方程得到：

$$d(y_k, \beta) = (I_{m \times m} + \beta^2 A^T)^{-1}[e(y_k, \beta) - \beta e(X_k, \beta)]. (14)$$

$$d(X_k, \beta) = \beta A^T d(y_k, \beta) + e(X_k, \beta). (15)$$

从 (12) 到 (15) 可以看出，通过逆运算 $(I+\beta M)^{-1}$ 和 $(I + \beta^2 A^T)^{-1}$，维度从 $(n^2+m)$ 降低到 $m \times m$，当 $n$ 大于 $m$ 时，计算量可以显著减少。因此存在投影收缩算法：

## 算法 2 改进的投影收缩算法

步骤 1：给定 $u_k \in \mathbb{R}^n \times \mathbb{R}^m, r \in (0,2), \beta \in [0,1]$。

步骤 2：对于 $k=0, 1, \dots$，若 $u_k \notin \Omega^*$：

步骤 3：从方程 (14) 和 (15) 计算 $d(y_k, \beta), d(X_k, \beta)$ 以得到 $d(u_k, \beta)$，

步骤 4：更新 $u_{k+1} = u_k - r\beta d(u_k, \beta)$。

## 4. 数值实验

测试平台和软件：Intel Xeon2 CPU (3.3GHz)，8GB内存 PC，Win 10 系统，Matlab 2010b 编程。

**示例 1** 考虑以下半正定规划问题：

$$A_1 = \begin{pmatrix} 0 & 1 & 0 & 0 \\ 1 & 2 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & -2 & -1 \\ 0 & -1 & -1 & -2 \end{pmatrix}, A_2 = \begin{pmatrix} 0 & -2 & 2 & 0 \\ 0 & 2 & 1 & 2 \\ -1 & -2 & 0 & 1 \\ 2 & 0 & 0 & 0 \\ 0 & 2 & 1 & 2 \end{pmatrix}$$

$$A_3 = \begin{pmatrix} 2 & -1 & -1 & 0 \\ 2 & 0 & 2 & 1 \\ -1 & -1 & 2 & -1 \\ 1 & 1 & 0 & -2 \end{pmatrix}, C = \begin{pmatrix} 3 & -3 & 3 & 1 \\ 3 & 5 & 3 & 2 \\ -3 & 3 & 1 & -1 \\ 1 & 2 & -1 & -1 \end{pmatrix}, b = \begin{pmatrix} -2 \end{pmatrix}$$

当 $\beta = 0.7$ 时，满足 $\|e(u,\beta)\| \le 10^{-4}$，算法终止。算法 1 在 71 次迭代后获得原始最优解，对偶间隙为 $9.305 \times 10^{-5}$。

**示例 2** 考虑随机半正定规划：整数 $m,n$ 生成 $m$ 个矩阵 $R_i \in \mathbb{R}^{n \times n}, i=1,\dots,m$。令 $A_i = (R_i + R_i^T)/2, b_i = \text{trace}(A_i)$。问题具有一个严格可行点 $(\mathbf{1})$，其中 $e$ 是元素全为1的列向量。算法 1 和 2 采用参数 $r = \beta = 1$。

| 迭代次数 | 算法 1 间隙 | 算法 1 时间 | 算法 2 间隙 | 算法 2 时间 | Yu 算法 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 10 | 0.0028 | 51.1 | 0.0044 | 58.2 | 0.0026 |
| 20 | 0.0129 | 51.1 | 0.0065 | 56.3 | 0.0042 |
| 30 | 0.0729 | 64.7 | 0.0103 | 62.7 | 0.0178 |
| 40 | 0.4385 | 70.2 | 0.0187 | 74.1 | 0.0221 |
| 50 | 1.0871 | 79.4 | 0.0291 | 80.4 | 0.0390 |
| 60 | 4.0640 | 77.8 | 0.0364 | 80.0 | 0.0512 |
| 70 | 9.1441 | 82.5 | 0.0583 | 83.1 | 0.0862 |
| 80 | 26.4063 | 78.0 | 0.0665 | 86.7 | 0.1012 |
| 90 | 411.4213 | 87.0 | 0.1098 | 83.1 | 0.2373 |





[9] He B. 一类线性变分不等式的新方法[J]. Mathematical Programming, 1994, 66(1): 137-144.

[10] He B. 求解一类线性投影方程[J]. Numerische Mathematik, 1994, 68(1): 71-80.

[12] Yu Z. 通过交替方向法求解半正定规划问题[J]. Journal of Computational and Applied Mathematics, 2006, 1932(2): 437-445.

[13] Liang F., He, G., Li, S. 适用于二阶锥规划的具有全牛顿步长的全局非线性内点算法[J]. Applications of Mathematics, 2009, 54(5): 447-464.

[14] Mu X, Zhang Y. 用于二阶锥规划的快速投影与收缩法[J]. Acta Mathematicae Applicatae Sinica. 2015, 38(1): 256. https://doi.org/10.12387/C2015003

[15] Mu X, Zhang Y. 使用投影与收缩法多指机器人手的抓持力优化[J]. Journal of Optimization Theory and Applications, 2019, 183(2): 592-608.

