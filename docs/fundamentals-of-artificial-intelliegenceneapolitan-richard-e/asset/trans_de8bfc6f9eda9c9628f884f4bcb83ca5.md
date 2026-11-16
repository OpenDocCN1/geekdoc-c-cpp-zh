
那么结果矩阵 P 满足等式 13.12。为确定这样的值，令 Q 为任意马尔可夫链的转移矩阵，其状态为给定有限状态集 \(\{e_1, e_2, \dots e_s\}\) 的成员，并令

\[
\alpha_{ij} = \left\{ \begin{array}{ll} \frac{s_{ij}}{1 + \frac{r_i q_{ij}}{r_j q_{ji}}} & q_{ij} \neq 0, q_{ji} \neq 0 \\ 0 & q_{ij} = 0 \text{ or } q_{ji} = 0 \end{array} \right. \tag{13.14}
\]

其中 \(s_{ij}\) 是 \(i\) 和 \(j\) 的对称函数，选取使得对所有 \(i\) 和 \(j\) 都有 \(0 \le \alpha_{ij} \le 1\)。然后取

\[
p_{ij} = \alpha_{ij} q_{ij} \quad i \neq j \tag{13.15}
\]
\[
p_{ii} = 1 - \sum_{j \neq i} p_{ij}.
\]

可以直接验证，得到的 \(p_{ij}\) 值满足等式 13.13。P 的不可减性必须在每个应用中进行检查。

Hastings [1970] 建议选择 s 的以下方法：如果 \(q_{ij}\) 和 \(q_{ji}\) 都非零，则设

\[
s_{ij} = \left\{ \begin{array}{ll} 1 + \frac{r_i q_{ij}}{r_j q_{ji}} & \frac{r_j q_{ji}}{r_i q_{ij}} \ge 1 \\ 1 + \frac{r_j q_{ji}}{r_i q_{ij}} & \frac{r_j q_{ji}}{r_i q_{ij}} \le 1 \end{array} \right. \tag{13.16}
\]

根据此选择，我们有

\[
\alpha_{ij} = \left\{ \begin{array}{ll} 1 & q_{ij} \neq 0, q_{ji} \neq 0, \frac{r_j q_{ji}}{r_i q_{ij}} \ge 1 \\ \frac{r_j q_{ji}}{r_i q_{ij}} & q_{ij} \neq 0, q_{ji} \neq 0, \frac{r_j q_{ji}}{r_i q_{ij}} \le 1 \\ 0 & q_{ij} = 0 \text{ or } q_{ji} = 0 \end{array} \right. \tag{13.17}
\]

如果使 Q 对称（即，对所有 \(i\) 和 \(j\) 都有 \(q_{ij} = q_{ji}\)），则得到 Metropolis 等人 (1953) 提出的方法。在此情况下

\[
\alpha_{ij} = \left\{ \begin{array}{ll} 1 & q_{ij} \neq 0, r_j \ge r_i \\ r_j / r_i & q_{ij} \neq 0, r_j \le r_i \\ 0 & q_{ij} = 0 \end{array} \right. \tag{13.18}
\]

注意，在此选择下，如果 Q 是不可减的，那么 P 也是不可减的。

**示例 13.13** 假设 \(r^T = (1/8\ 3/8\ 1/2)\)。按如下方式选择对称的 Q：

Q =

| 1/3 | 1/3 | 1/3 |
| --- | --- | --- |
| 1/3 | 1/3 | 1/3 |
| 1/3 | 1/3 | 1/3 |

根据等式 13.16 选择 s，使 \(\alpha\) 具有等式 13.18 中的值。我们有

\(\alpha =\)

| 1 | 1 | 1 |
| --- | --- | --- |
| 1/3 | 1 | 1 |
| 1/4 | 3/4 | 1 |

使用等式 13.15，我们有

P =

| 1/3 | 1/3 | 1/3 |
| --- | --- | --- |
| 1/9 | 5/9 | 1/3 |
| 1/12 | 1/4 | 2/3 |

注意

\(r^T P = (1/8\ 3/8\ 1/2) \begin{pmatrix} 1/3 & 1/3 & 1/3 \\ 1/9 & 5/9 & 1/3 \\ 1/12 & 1/4 & 2/3 \end{pmatrix} = (1/8\ 3/8\ 1/2) = r^T\),

正如所期望的那样。

一旦按上述方法构建了矩阵 Q 和 \(\alpha\)，我们就可以按如下方式进行模拟：

- 1. 给定第 k 次试验所占状态为 e_i，使用 Q 的第 i 行给出的概率分布选择一个状态。假设该状态为 e_j。
- 2. 将第 (k + 1) 次试验所占状态选择为 e_j，概率为 \(\alpha_{ij}\)，选择为 e_i，概率为 \(1 - \alpha_{ij}\)。

这样一来，当状态 e_i 为当前状态时，在第 (1) 步中 e_j 将以 q_{ij} 的比例被选择，而在这些次数中，在第 (2) 步中 e_j 将以 \(\alpha_{ij}\) 的比例被选择。因此，总体上 e_j 将以 \(\alpha_{ij} q_{ij} = p_{ij}\) 的比例被选择（参见等式 13.15），这正是我们想要的。

## 吉布斯采样方法

接下来，我们展示另一种创建马尔可夫链的方法，其平稳分布是特定的联合概率分布。该方法称为吉布斯采样，适用于我们有 n 个随机变量 X_1, X_2, ... X_n 及其联合概率分布 P（如贝叶斯网络中）的情况。如果令 X = {X_1, X_2, ... X_n}，我们希望近似

\(\sum_x f(x)P(x)\)。

要使用 MCMC 近似此和，我们需要创建一个马尔可夫链，其状态集为 X 的所有可能取值，且其平稳分布为 P(x)。我们通过在第 h 次试验中按如下方式选择 X 的值来实现这一点：

- 使用分布 \(P(x_1|x_2^{(h-1)}, x_3^{(h-1)}, \dots, x_n^{(h-1)})\) 选取 \(x_1^{(h)}\)。
- 使用分布 \(P(x_2|x_1^{(h)}, x_3^{(h-1)}, \dots, x_n^{(h-1)})\) 选取 \(x_2^{(h)}\)。
- \(\vdots\)
- 使用分布 \(P(x_k|x_1^{(h)}, \dots, x_{k-1}^{(h)}, x_{k+1}^{(h-1)} \dots, x_n^{(h-1)})\) 选取 \(x_k^{(h)}\)。
- \(\vdots\)
- 使用分布 \(P(x_n|x_1^{(h)}, \dots, x_{n-1}^{(h)})\) 选取 \(x_n^{(h)}\)。

注意，在第 k 步中，除了 \(x_k^{(h)}\) 之外的所有变量均保持不变，且 \(x_k^{(h)}\) 的新值是从其条件于所有其他变量当前值的分布中抽取的。

只要所有条件概率都非零，该链就是不可减的。接下来，我们验证 P(x) 是该链的平稳分布。如果令 \(p(x;\hat{x})\) 表示每次试验中从 x 到 \(\hat{x}\) 的转移概率，我们需要证明

\(P(\hat{x}) = \sum_x P(x)p(x;\hat{x})\)。 (13.19)

不难看出，只需证明每次试验的每个步骤中等式 13.19 成立即可。为此，对于第 k 步，我们有

\(\sum_x P(x)p_k(x;\hat{x})\)
\(= \sum_{x_1, \dots, x_n} P(x_1, \dots, x_n)p_k(x_1, \dots, x_n; \hat{x}_1, \dots, \hat{x}_n)\)
\(= \sum_{x_k} P(\hat{x}_1, \dots, \hat{x}_{k-1}, x_k, \hat{x}_{k+1}, \dots, \hat{x}_n)P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n) \sum_{x_k} P(\hat{x}_1, \dots, \hat{x}_{k-1}, x_k, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x}_k|\hat{x}_1, \dots, \hat{x}_{k-1}, \hat{x}_{k+1}, \dots, \hat{x}_n)P(\hat{x}_1, \dots \hat{x}_{k-1}, \hat{x}_{k+1}, \dots \hat{x}_n)\)
\(= P(\hat{x}_1, \dots \hat{x}_{k-1}, \hat{x}_k, \hat{x}_{k+1}, \dots, \hat{x}_n)\)
\(= P(\hat{x})\)。

第二步成立是因为 \(p_k(x;\hat{x}) = 0\)，除非对所有 \(j \neq k\) 都有 \(\hat{x}_j = x_j\)。

有关吉布斯采样的更多信息，请参见 [Geman and Geman, 1984]。

### 13.2.6.3 使用吉布斯采样处理缺失数据的学习

我们使用的吉布斯采样方法称为候选方法（参见 [Chib, 1995]）。该方法的步骤如下：令 D 为我们有取值的变量的取值集合。根据贝叶斯定理，我们有

\[
P(\mathbf{D}|\mathbb{G}) = \frac{P(\mathbf{D}|\breve{\mathbf{f}}^{(\mathbb{G})}, \mathbb{G})\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbb{G})}{\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G})}, \tag{13.20}
\]

其中 \(\breve{\mathbf{f}}^{(\mathbb{G})}\) 是对 \(\mathbb{G}\) 中参数的任意值赋值。为了近似 \(P(\mathbf{D}|\mathbb{G})\)，我们选择 \(\breve{\mathbf{f}}^{(\mathbb{G})}\) 的某个值，精确计算等式 13.20 中的分子，并使用吉布斯采样近似分母。对于分母，我们有

\[
\rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G}) = \sum_{\mathbf{m}} \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbf{m}, \mathbb{G})P(\mathbf{m}|\mathbf{D}, \mathbb{G})
\]

其中 M 是具有缺失值的变量集合。

要使用吉布斯采样近似此和，我们执行以下操作：

- 1. 将未观测变量的状态初始化为任意值，从而得到一个完整数据集 D1。
- 2. 任意选择某个未观测变量 \(X_i^{(h)}\)，并使用以下公式获取 \(X_i^{(h)}\) 的一个值：
  
  \[
  P(x'_i^{(h)}|\mathbf{D}_1 - \{\breve{x}_i^{(h)}\}, \mathbb{G}) = \frac{P(x'_i^{(h)}, \mathbf{D}_1 - \{\breve{x}_i^{(h)}\}|\mathbb{G})}{\sum_{x_i^{(h)}} P(x_i^{(h)}, \mathbf{D}_1 - \{\breve{x}_i^{(h)}\}|\mathbb{G})}
  \]
  
  其中 \(\breve{x}_i^{(h)}\) 是 D1 中 \(X_i^{(h)}\) 的值，求和是对 \(X_i^{(h)}\) 空间中的所有值进行。分子和分母中的项可以使用等式 13.4 计算。
- 3. 对所有其他未观测变量重复步骤 (2)，其中第 (k+1) 次迭代中使用的完整数据集包含前 k 次迭代中获得的值。

这将产生一个新的完整数据集 D2。

- 4. 将前两步迭代 R 次，其中第 j 次迭代的完整数据集用于第 (j+1) 次迭代。这样将生成 R 个完整数据集。对于每个完整数据集 \(\mathbf{D}_j\)，计算
  
  \[
  \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}_j, \mathbb{G})
  \]
  
  使用等式 12.3。
- 5. 近似
  
  \[
  \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}, \mathbb{G}) \approx \frac{\sum_{j=1}^R \rho(\breve{\mathbf{f}}^{(\mathbb{G})}|\mathbf{D}_j, \mathbb{G})}{R}.
  \]

虽然候选方法可以应用于参数的任何 \(\breve{\mathbf{f}}^{(\mathbb{G})}\) 值，但某些赋值会导致更快的收敛。Chickering 和 Heckerman [1997] 讨论了选择该值的方法。
