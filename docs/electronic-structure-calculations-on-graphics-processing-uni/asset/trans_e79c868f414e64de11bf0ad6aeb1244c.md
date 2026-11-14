
其中我们已将指标压缩为 \(a \equiv (n, k)\)、\(b \equiv (m, q)\)，\(V_{a,b}\) 是一个由以下给出的复杂双粒子势：

```
\langle r | V_{a,b} | r' \rangle = f_b \int \frac{|r' \rho_a| |r'|^2}{|r - r'|} dr' \tag{7.53}
```

\(\rho_{a,b}\) 是一个由以下给出的双粒子密度：

```
\langle r | \rho_{a,b} | r' \rangle = \langle r | \tilde{\psi}_a \rangle \langle \tilde{\psi}_b | r' \rangle + \sum_{ij} Q_{ij}(r) \langle r | \tilde{\psi}_i \rangle \langle \tilde{\psi}_j | r' \rangle \tag{7.54}
```

而 \(D\) 是 \(V_{a,b}\) 的一个矩阵泛函，由以下给出：

```
$D_{ij}[V_{a,b}] = \sum_r Q_{ij}(r) \langle r | V_{a,b} | r \rangle \tag{7.55}$
```

我们已将对 \(r'\) 的求和在 Eq. (7.53) 中写为积分，以将其突出为 Poisson 求解。与 USPPs 的情况一样，\(Q\) 是重叠矩阵 \(S - I\) 的非平凡部分，而 \(D\) 是一个非局部势 \(D[V_{a,b}] \equiv V_{a,b}^{nl}\)。分解为对 \(k[b]\) 的求和将 Hartree-Fock 交换表征为一种全波函数-或轨道依赖-能量泛函。将计算视为对带指标对 \(a, b\) 的求和，类似于 Eq. (7.50)，可能很有用。VASP [13, 49] 中的 Hartree-Fock 交换项已被移植到 GPU [38]。我们使用此移植来演示 GPU 上精确交换的关键特性。

## 7.6.1 实现

精确交换的计算可分为两个阶段：双粒子势的构建阶段和作用阶段。构建阶段分别生成局部和非局部形式的双粒子势，即 Eqs. (7.53) 和 (7.55)。作用阶段，Eq. (7.51)，与第 7.2.1 节中常规单粒子势的作用相同，即 Eq. (7.6) 的最后两项。第 7.3 节中介绍的技术可以重复使用。因此，本节将重点介绍双粒子势的构建。

### 7.6.1.1 双面投影

与常规 PWDFT 类似，基变换是精确交换计算的重要部分。然而，此处我们还关注使用 \(Q_{ij}(r)\) 对 2-张量量进行投影，\(Q_{ij}(r)\) 在第 7.3.1 节中已介绍。\(Q_{ij}(r)\) 是一个 2,2-张量，它将对角实空间 1,1-张量与投影对联系起来。正向变换为

```
$D_{ij}[\phi] = \sum_r Q_{ij}(r) \phi(r) \tag{7.56}$
```

其中 \(\phi\) 是一个任意的对角实空间 1,1-张量。逆变换为

```
\(\tilde{\phi}_{ab}(r) = \sum_{ij} \langle r | r' Q_{ij} \rangle \langle r' | \phi_i | r \rangle \langle \phi_b | \phi_j \rangle \tag{7.57}\)
```

其中 \(\phi_a, \phi_b\) 是任意向量，\(\tilde{\phi}_{ab}\) 是它们的变换。我们将这些双面投影称为 *张量投影*，并将第 7.3.1 节中描述的过程称为 *向量投影*。虽然该过程在形式上是正确的，但张量 \(Q\) 具有可被利用来分解计算的附加结构。考虑到投影仪的 \(i,j\) 指标遍历角动量，Q 可以赋予额外的指标，这些指标遍历单个角动量 i 和 j 之和的总角动量 LM：

\hat{\phi}_{ab}(r) = \sum_{iLM} \langle r | r' \rangle Q_{ij}^{LM}(r') \langle r' | \phi_i \rangle \langle \phi_j | \phi_i \rangle. \tag{7.58}

其中 Q_{ij}^{LM}(r) 具有分析形式，可分离 i,j 和 r 的依赖关系：

Q_{ij}^{LM}(r) = q_{ij}^L g_L(|r - R|) Y_{LM}(r - R), \tag{7.59}

其中 R 是离子中心的位置，q_{ij}^L 是常数，Y_{LM} 函数是标准球谐函数。

逆双面投影可以重写为

\hat{\phi}_{ab}(r) = \sum_{r'} \langle r | r' \rangle \left[ \sum_{LM} g_L(|r' - R|) Y_{LM}(r' - R) \left( \sum_{i,j} q_{ij}^{LM} \langle \beta | \phi_i \rangle \langle \phi_j | \phi_i \rangle \right) \right]. \tag{7.60}

在此背景下，逆双面投影被分解为三个步骤：从 i,j-空间到 LM-空间的变换，从 LM-空间到 r'-空间的逆投影，以及从 r'-空间到完整 r-空间的散射。正向双面投影可以类似处理：

D_{ij}[\phi] = \sum_{LM} q_{ij}^{LM} \left[ \sum_{r'} g_L(|r' - R|) Y_{LM}(r' - R) \left( \sum_r \langle r' | r \rangle \phi(r) \right) \right]. \tag{7.61}

这里我们只是简单地反转了各个步骤。

从 r' 到 LM 空间的散射/收集和投影正是第 7.3.1 节中的向量投影。因此，我们可以重复使用向量投影内核 Listings 1 和 2。Q_{ij}^{LM} 分解将 (i,j,r) 上的嵌套循环转换为 (i,j) 和 (r) 上的顺序循环，并促进了向量投影代码的重用。因此，我们将专注于这种张量投影方法：即投影到 LM 以及从 LM 到 i,j 的变换。

### 7.6.1.2 双粒子伪密度

Eq. (7.54) 中的第一项是在实空间中的逐元素乘积。类似于动能和局部势的对角乘积中存在的逐元素乘积，此操作受带宽限制。通过分块构建多个势（这些势重用波函数）可以减少加载次数。Listing 6 演示了这一点。

### 7.6.1.3 双粒子增强密度

Eq. (7.54) 中的第二项是双粒子逆投影。使用 Eq. (7.60) 的形式，只需计算 q_{ij}^{LM} 给出的变换：

\hat{\rho}_{ab}(LM) = \sum_{i,j} \langle u_i | \beta \rangle q_{ij}^{LM} \langle \beta | u_a \rangle. \tag{7.62}

这类似于为每个 LM 计算广义内积：\langle u_i | q(LM) | u_a \rangle。幸运的是，Q 的每个块中只有约 10 个角动量指标 i,j,LM，因此每个内积都很小。此外，q_{ij}^{LM} 是实数。

由于尺寸小且类型混合，使用现有库难以高效执行此操作。相反，一个对 |u_a\rangle 进行分块的自定义内核可以实现合理的性能。此类内核的示例可在 Listing 7 中找到。

### 7.6.1.4 双粒子局部势

给定双粒子密度 \(\rho_{ab}\)，双粒子局部势 \(V_{ab}\) 的评估是 Eq. (7.53) 的 Poisson 求解。实空间中的 Poisson 求解是在倒空间中与向量 \(1/|G|^2\) 的逐元素乘积：

\(V_{ab,lm}(r) = f_b \sum_{k',m'} |r\rangle \left( \frac{\langle r' | \rho_{a,km}(r') \rangle}{|k+k'-q|^2} \right),\) (7.63)

这里我们重新引入了显式的 \(n,k,m\) 指标，并令 \(\langle r|V|r\rangle \equiv V(r)\) 和 \(\langle r'|\rho|r'\rangle \equiv \rho(r')\) 以简化记号。与之前一样，FFT 用于在实空间和倒空间之间转换，\(\langle g|r\rangle\) 和 \(\langle r|g\rangle\) 分别对应。乘以核的形式与动能中乘以 \(|g+k'|^2\) 或局部势中乘以 \(V^{xc}(r)\) 的形式相同。Listing 3 中找到的自定义内核可以重用。FFT 的数量为 \(2N_k^2\)，非常耗时。

### 7.6.1.5 双粒子非局部势

非局部双粒子势 \(D_{a,b}\)（Eq. (7.55)）的构建是正向张量投影：

\(D_{ij}[V_{a,b}] = \sum_{r'} Q_{i,r'}(r')|r\rangle \langle r|V_{a,b}|r\rangle \langle r|r'\rangle.\) (7.64)

与双粒子增强密度类似，可以使用中间 \(LM\) 变换来分解投影，如 Eq. (7.61) 所示。使用正向向量投影从 \(r\)-空间到 \(LM\)-空间，剩余操作为

\(D_{ij}[V_{a,b}] = \sum_{LM} D_{LM}[V_{a,b}] d_{ij}^{LM},\) (7.65)

这是 Eq. (7.62) 的逆运算。从计算上讲，这是对矩阵的加权求和。由于尺寸小且类型混合，自定义内核优于库调用。此类内核的示例可在 Listing 8 中找到。

## 7.6.2 优化

GPU 上高效并行实现精确交换的关键特征是灵活的循环分块方案。此类方案必须便于启动大型数据并行内核以充分占用单个 GPU，同时为多个 GPU 上的任务并行提供足够的分解。

当插入到迭代对角化器中（如第 7.2.5 节所讨论的）时，必须在每个 k 点的每个带上计算精确交换算子的作用。我们使用 Eq. (7.52) 给出的分解，将其识别为计算成对作用 \(\langle r|\hat{K}[i]|\hat{\Psi}_j\rangle\) 的表，然后对列求和。

| | \(\hat{\Psi}_1\) | \(\hat{\Psi}_2\) | \(\hat{\Psi}_3\) | \(\hat{\Psi}_4\) | ... |
|---|---|---|---|---|---|
| \(\hat{K}[1]\) | \(\langle r|\hat{K}[1]|\hat{\Psi}_1 \rangle\) | \(\langle r|\hat{K}[1]|\hat{\Psi}_2 \rangle\) | \(\langle r|\hat{K}[1]|\hat{\Psi}_3 \rangle\) | \(\langle r|\hat{K}[1]|\hat{\Psi}_4 \rangle\) | ... |
| \(\hat{K}[2]\) | \(\langle r|\hat{K}[2]|\hat{\Psi}_1 \rangle\) | \(\langle r|\hat{K}[2]|\hat{\Psi}_2 \rangle\) | \(\langle r|\hat{K}[2]|\hat{\Psi}_3 \rangle\) | \(\langle r|\hat{K}[2]|\hat{\Psi}_4 \rangle\) | ... |
| \(\hat{K}[3]\) | \(\langle r|\hat{K}[3]|\hat{\Psi}_1 \rangle\) | \(\langle r|\hat{K}[3]|\hat{\Psi}_2 \rangle\) | \(\langle r|\hat{K}[3]|\hat{\Psi}_3 \rangle\) | \(\langle r|\hat{K}[3]|\hat{\Psi}_4 \rangle\) | ... |
| \(\hat{K}[4]\) | \(\langle r|\hat{K}[4]|\hat{\Psi}_1 \rangle\) | \(\langle r|\hat{K}[4]|\hat{\Psi}_2 \rangle\) | \(\langle r|\hat{K}[4]|\hat{\Psi}_3 \rangle\) | \(\langle r|\hat{K}[4]|\hat{\Psi}_4 \rangle\) | ... |
| \(\vdots\) | | | | | |
| \(\sum\) | \(\langle r|\hat{K}|\hat{\Psi}_1 \rangle\) | \(\langle r|\hat{K}|\hat{\Psi}_2 \rangle\) | \(\langle r|\hat{K}|\hat{\Psi}_3 \rangle\) | \(\langle r|\hat{K}|\hat{\Psi}_4 \rangle\) | ... |
