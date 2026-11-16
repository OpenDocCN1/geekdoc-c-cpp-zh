

```matlab
load fisheriris;
% extract two attributes
pl = meas(:,3); % petal length
pw = meas(:,4); % petal width
figure;
h1 = gscatter(pl, pw, species,'rgb','os');
legend('Setosa','Versicolor','Virginica','Location','best')
hold on
X = [pl,pw];
cls = ClassificationDiscriminant.fit(X,species,...
    'DiscrimType','quadratic');
% plot the classification boundaries
% retrieve the coefficients for the quadratic boundary between
% the first and second class (setosa and versicolor).
c = cls.Coeffs(1,2).Const;
l = cls.Coeffs(1,2).Linear;
q = cls.Coeffs(1,2).Quadratic;
% plot the curve c + [x1,x2]'*l + [x1,x2]*q*[x1,x2]' = 0;
F = @(x1,x2) c + l(1,1).*x1 + l(1,2).*x2 + q(1,1).*x1.^2 + ...
    (q(1,2)+q(2,1)).*x1.*x2 + q(2,2).*x2.^2;
h2 = ezplot(F,[.9 7.1 0 1]);
set(h2, 'Color', 'k');
% retrieve the coefficients for the quadratic boundary between
% the first and third class (versicolor and virginica).
c = cls.Coeffs(2,3).Const;
l = cls.Coeffs(2,3).Linear;
q = cls.Coeffs(2,3).Quadratic;
% plot the curve c + [x1,x2]'*l + [x1,x2]*q*[x1,x2]' = 0;
F = @(x1,x2) c + l(1,1).*x1 + l(1,2).*x2 + q(1,1).*x1.^2 + ...
    (q(1,2)+q(2,1)).*x1.*x2 + q(2,2).*x2.^2;
h3 = ezplot(F,[.5 7.0 0 2.5]);
set(h3, 'Color', 'k');
xlabel('Petal length');
ylabel('Petal width');
axis([0 8 0 3]);
title('');
```

清单 5.1: 二次判别分析.

![](img/d3c00252180686426c9e63ab889b535b_132_0.png)

图 5.1: 二次判别分析.

这正是线性判别分析中直线的方程。在下一节中，我们将通过引入人工特征并以这种方式扩展特征空间，从另一个角度来探讨二次判别分析.

## 5.2 核技巧

在二次

$$v^T A v + v^T b + c = 0$$

矩阵 A 是对称的，因为 A 是协方差矩阵的差，而协方差矩阵是对称的。假设 M = 2 并写成

$$A = \begin{pmatrix} A_{11} & A_{12} \\ A_{12} & A_{22} \end{pmatrix}, \quad b = \begin{pmatrix} b_1 \\ b_2 \end{pmatrix},$$

边界方程可以写成

$$A_{11} v_1^2 + 2 A_{12} v_1 v_2 + A_{22} v_2^2 + b_1 v_1 + b_2 v_2 + c = 0.$$

现在我们可以将其重排为

$$( A_{11} \quad 2A_{12} \quad A_{22} \quad b_1 \quad b_2 ) \begin{pmatrix} v_1^2 \\ v_1 v_2 \\ v_2^2 \\ v_1 \\ v_2 \end{pmatrix} + c = 0.$$

![](img/d3c00252180686426c9e63ab889b535b_133_0.png)

![](img/d3c00252180686426c9e63ab889b535b_133_1.png)

图 5.2: 线性不可分数据及其向更高维空间的变换.

令 $\mathbf{w}^T = ( A_{11} \quad 2A_{12} \quad A_{22} \quad b_1 \quad b_2 )$ 和 $\tilde{\mathbf{v}} = \begin{pmatrix} v_1^2 \\ v_1 v_2 \\ v_2^2 \\ v_1 \\ v_2 \end{pmatrix}$，这描述了五维特征空间中的线性边界

$$\mathbf{w}^T \tilde{\mathbf{v}} + c = 0.$$

换句话说，我们通过三个人工特征扩充了特征空间

- $v_1^2$
- $v_1 v_2$
- $v_2^2$

这被称为 *核技巧*。特征被转换到更高维的特征空间，其中类别是线性可分的。我们将在下面看到，在实践中从不执行此变换。

图 5.2 显示了人工数据，这些数据无法被一条直线分开，以及它们向更高维空间的变换，在该空间中它们可以被一个平面分开。我们设置 $v_3 = \sqrt{v_1^2 + v_2^2}$，平面位于 $v_3 = 1$。回到二维，$v_3^2 = v_1^2 + v_2^2 = 1$ 是 $v_1, v_2$ 平面上的单位圆。

为了形式化这种方法，回顾一下，支持向量机根据

$-b + \sum_{n=1}^N \alpha_n c_n \mathbf{v}_n^T \mathbf{v}_i$

的符号进行分类，其中偏置 $b$ 由 $- \sum_{n=1}^N \alpha_n c_n$ 给出，且 $c_i = \pm 1$ 是样本 $\mathbf{v}_i$ 的类标签。对于 $i = 1, \dots, N$ 的 $\alpha_i \ge 0$ 最大化函数

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n (1 + \mathbf{v}_i^T \mathbf{v}_n).$

令 $\phi : \mathbb{R}^M \to \mathbb{R}^{\hat{M}}$ 为从原始 $M$ 维特征空间到更高 $\hat{M}$ 维特征空间的映射。我们现在将支持向量机应用于此更高维空间中的数据；即我们需要最大化

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n \left( 1 + \phi(\mathbf{v}_i)^T \phi(\mathbf{v}_n) \right).$

令 $k : \mathbb{R}^M \times \mathbb{R}^M \to \mathbb{R}$ 定义为

$k(\mathbf{x}, \mathbf{y}) = \phi(\mathbf{x})^T \phi(\mathbf{y}).$

这被称为 *核函数* 或简称 *核*。使用此记号，要最大化的目标函数变为

$L(\boldsymbol{\alpha}) = \sum_{n=1}^N \alpha_n - \frac{1}{2} \sum_{i=1}^N \sum_{n=1}^N \alpha_i \alpha_n c_i c_n \left( 1 + k(\mathbf{v}_i, \mathbf{v}_n) \right),$

受限于 $\alpha_i \ge 0, i = 1, \dots, N$。分类根据

$-b + \sum_{n=1}^N \alpha_n c_n \phi(\mathbf{v}_n)^T \phi(\mathbf{v}) = -b + \sum_{n=1}^N \alpha_n c_n k(\mathbf{v}_n, \mathbf{v}).$

的符号进行。

我们看到映射 $\phi$ 从不需要被评估，在最大化和分类中只需要核函数 $k$。

核技巧可以应用于所有线性分类方法，以分离线性不可分的数据。所有方法都归结为核函数 $k$ 的评估。

核函数源自更高维的内积。在前一章中，我们将内积视为不同样本之间关系的度量。一个新样本根据它是否更相关于某一类的支持向量而非另一类来分类。核函数给出一个描述两个样本之间关系的数值。

可以构造此类描述样本之间关系的函数。此类函数适合我们目的的必要且充分条件是：$N \times N$ 矩阵 $\mathbf{K}$（其 $(m, n)$ 项等于 $k(\mathbf{x}_m, \mathbf{x}_n)$）对于任何 $N$ 和任何集合 $\{\mathbf{x}_1, \dots, \mathbf{x}_N\}$ 都是半正定的。它被称为 *Gram* 或 *Gramian 矩阵*。对于正数 $c$，常数函数 $k(\mathbf{x}, \mathbf{y}) = c$ 是一个有效的核，因为对于任何向量 $\mathbf{v} = (v_1, \dots, v_n)^T$

$$\mathbf{v}^T \mathbf{K} \mathbf{v} = c \left( \sum_{n=1}^N v_n \right)^2 \ge 0.$$

如果核函数是通过更高维空间中的内积定义的，那么 K 也具有半正定性，因为

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m \phi(\mathbf{x}_m)^T \phi(\mathbf{x}_n) v_n = \left( \sum_{m=1}^N v_m \phi(\mathbf{x}_m) \right)^T \left( \sum_{n=1}^N v_n \phi(\mathbf{x}_n) \right) = \| \sum_{n=1}^N v_n \phi(\mathbf{x}_n) \|^2 \ge 0.$$

因此内积本身是一个有效的核。

如果 A 是一个对称、半正定的 \(M \times M\) 矩阵，那么由

$$k(\mathbf{x}, \mathbf{y}) = \mathbf{x}^T \mathbf{Ay}$$

定义的函数是一个有效的核函数，因为在这种情况下

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m \mathbf{x}_m^T \mathbf{A} \mathbf{x}_n v_n = \left( \sum_{m=1}^N v_m \mathbf{x}_m \right)^T \mathbf{A} \left( \sum_{n=1}^N v_n \mathbf{x}_n \right) \ge 0.$$

类似地，如果 \(f : \mathbb{R}^M \to \mathbb{R}$ 是任意函数且 \(k : \mathbb{R}^M \times \mathbb{R}^M \to \mathbb{R}$ 是一个有效的核，那么

$$\sum_{m,n=1}^N v_m f(\mathbf{x}_m) k(\mathbf{x}_m, \mathbf{x}_n) f(\mathbf{x}_n) v_n = \mathbf{w}^T K \mathbf{w} \ge 0, \quad (5.1)$$

其中 \(\mathbf{w} = ((f(\mathbf{x}_1)v_1, \dots, f(\mathbf{x}_N)v_N)^T$。因此，由 \(f(\mathbf{x})k(\mathbf{x}, \mathbf{y})f(\mathbf{y})\) 定义的函数是一个核函数。

将有效核乘以正常数显然是一个核，两个有效核的和也是如此。另外，两个有效核的乘积也是一个核。令 \(\{\mathbf{x}_1, \dots, \mathbf{x}_N\}$ 为任意集合。令 \(\mathbf{K}$ 表示核乘积的 Gram 矩阵。由于两个核（作为因子）的 Gram 矩阵是对称且半正定的，它们可以分别写成乘积 \(\mathbf{A}^T \mathbf{A}$ 和 \(\mathbf{B}^T \mathbf{B}$。因此，它们的 \((m, n)$ 项分别由

$$\sum_{i=1}^N A_{mi} A_{ni} \quad \text{and} \quad \sum_{j=1}^N B_{mj} B_{nj}$$

分别给出。现在，对于任意向量 \(\mathbf{v} = (v_1, \dots, v_n)^T$，

$$\mathbf{v}^T \mathbf{Kv} = \sum_{m,n=1}^N v_m K_{mn} v_n = \sum_{m,n=1}^N v_m \left( \sum_{i=1}^N A_{mi} A_{ni} \right) \left( \sum_{j=1}^N B_{mj} B_{nj} \right) v_n = \sum_{i,j=1}^N \left( \sum_{m=1}^N v_m A_{mi} B_{mj} \right) \left( \sum_{n=1}^N v_n A_{ni} B_{nj} \right) = \sum_{i,j=1}^N \left( \sum_{m=1}^N v_m A_{mi} B_{mj} \right)^2 \ge 0.$$

