

### 算法 8.1 单层感知器学习

输入：训练数据 \(X=\{\mathbf{x}_1,\dots,\mathbf{x}_N\}\) 和关联标签 \(\{t_1,\dots,t_N\}\)，其中 \(\mathbf{x}_n \in \mathbb{R}^D\)，\(t_n \in \{-1,+1\}\)；学习率 \(\eta > 0\)。

输出：训练好的单层感知器，其最优权重集为 \(\mathbf{w}\)。

```text
1: Randomly initialize the set of weights w = (w1, ..., wd) to zero.
2: repeat
3:   for n in {1,...,N} do
4:     Compute the neuron output o_n = sign(w^T x_n)
5:     if o_n != t_n then
6:       w <- w + η t_n x_n      # misclassified data
7:     end if
8:   end for
9: until All training data are correctly satisfied or a specified minimum number of iterations are executed
```

感知器准则等价于求解线性不等式 \(t_n \mathbf{w}^T \mathbf{x}_n > 0\) 对所有 \(\mathbf{x}_n\) 成立，这可以通过增量方式一次一个样本完成，也可以通过批量方式完成。

SLP 学习如算法 8.1 所示。它等价于感知器准则上的随机梯度下降。算法的一些变体使用随 \(n\) 线性递减的学习率 \(\eta(n)\)。对于每个被误分类的样本 \(\mathbf{x}_n\)，训练过程在数据属于类 \(C_2\) 时将数据加到权重上，并在数据属于 \(C_1\) 时从权重中减去输入数据。这种基于标签的选择性更新的效果是逐步重新调整分离超平面，使其朝向最优分离两个类的方向 [19,35]。感知器算法的批量版本对误分类样本的累积和执行类似的更新：

\[
\mathbf{w} \leftarrow \mathbf{w} + \eta(t) \sum_{n,\, o_n \neq t_n} \mathbf{x}_n t_n \tag{8.21}
\]

其中学习率 \(\eta(t)\) 随训练时间 \(t\) 线性递减。更新在执行指定次数的 epoch 或所有数据都被正确分类时完成。它是 delta 规则的直接应用，因为权重根据其对误差的贡献进行更新。

感知器收敛定理保证了该过程的最优性：如算法 8.1 所示的学习算法，只要类是线性可分的，就能在有限次迭代内找到最优权重集 [35,52,114]。

对于非线性问题，没有成功的保证。在这种情况下，学习旨在实现在可容忍的误差范围 \(\gamma\) 内的分类性能，使得

\[
t_n \mathbf{w}^T \mathbf{x}_n > \gamma \tag{8.22}
\]

对所有 \(n\) 成立。感知器学习随后最小化相对于该范围的误分类误差，给出

\[
\mathbf{w} \leftarrow \mathbf{w} + \eta t_n \mathbf{x}_n \quad \text{if } -t_n \mathbf{w}^T \mathbf{x}_n > \gamma. \tag{8.23}
\]

对于满足方程 8.22 条件的 \(\gamma > 0\)，感知器边界定理给出了可实现错误数的上界。假设存在一组归一化的权重 \(\mathbf{w}\) 使得 \(\|\mathbf{w}\| = 1\)，并且整个训练集包含在一个直径为 \(D\) 的球内（对所有 \(n\)，\(\|\mathbf{x}_n\| < D\)），则感知器学习算法在训练集 \(X\) 上犯的错误数 \(M\) 至多为 \(D^2/\gamma^2\)。然而，事先并不知道最优的 \(\gamma\)。在实践中，\(\gamma\) 可以在学习方案完成后设为

\[
\gamma = \min_n t_n \mathbf{w}^T \mathbf{x}_n \tag{8.24}
\]

该值可用于提供误差率的上界。注意该上界不依赖于输入数据的维度，使得感知器适用于大维度数据。为了消除对 \(D\) 的依赖，通常将每个训练数据归一化为 \(\mathbf{x}_n/\|\mathbf{x}_n\|\)，从而得到形式为 \(1/\gamma^2\) 的上界。

### 8.3.1.2 多类感知器

原始感知器算法处理的是两类问题，并使用具有阈值激活的单个输出单元。对于具有 \(K > 2\) 个类 \(C_1,\dots,C_K\) 的分类问题，感知器在输出层中具有 \(K\) 个输出单元，每个类一个输出单元，且所有输出单元接收相同输入数据。每个输出 \(j\) 都有自己的一组权重 \(\mathbf{w}_j\)。这等价于多类线性机 [35,104]，其中第 \(j\) 个输出单元为类 \(C_j\) 实现线性判别函数。对于输入数据 \(\mathbf{x}=(1,x_1,\dots,x_d)\)，每个输出单元 \(j\) 计算净值 \(v_j=\mathbf{w}_j^T \mathbf{x}\) 和输出值 \(o_j=v_j\)，其中列向量 \(\mathbf{w}_j=(w_{0j},w_{1j},\dots,w_{dj})\) 是权重集，\(w_{ij}\) 表示第 \(i\) 个输入单元与第 \(j\) 个输出单元之间的连接，\(w_{0j}\) 为偏置。与两类感知器不同，输出单元是线性单元；不使用阈值激活。线性激活的使用允许对输出产生的分数进行渐进比较，而使用阈值单元产生 \(-1\) 或 \(1\) 则无法实现。

分类通过选择输出值最高的输出单元的类来完成：

\[
\mathbf{x} \in C_k \quad \text{if } k = \arg\max_j o_j. \tag{8.25}
\]

多类感知器的监督训练旨在在输入数据属于代表性类别 \(C_k\) 时生成正值 \(o_k\)，而在输入数据属于除 \(C_k\) 之外的类别时生成负值。为了实现这一结果，多类感知器学习在误分类时实现竞争学习方案。给定训练数据 \(X=\{\mathbf{x}_1,\dots,\mathbf{x}_N\}\)，其关联期望输出 \(\mathbf{t}_n=(t_{n1},\dots,t_{nK})\)，其中 \(t_{nj}\) 使用 1-of-K 原则编码为集合 \(\{-1,1\}\) 中的值，如

\[
t_{nk} = \begin{cases} 1 & \text{if } \mathbf{x}_n \in C_k \\ -1 & \text{otherwise,} \end{cases} \tag{8.26}
\]

则，对于属于类 \(C_k\) 的输入数据 \(\mathbf{x}_n\) 生成输出 \(o_k\)，当 \(\mathbf{x}_n\) 被误分类到类 \(C_q\) 时，多类感知器执行更新：

\[
\mathbf{w}_j \leftarrow \mathbf{w}_j + \eta t_{nj} \mathbf{x}_n \quad \text{for } j \in \{k,q\}. \tag{8.27}
\]

与两类情况类似，仅当输入数据被误分类时才发生更新。其效果是增加正确类别的权重向量 \((\mathbf{w}_k \leftarrow \mathbf{w}_k + \eta \mathbf{x}_n)\) 并减少竞争类别的权重向量 \(\mathbf{w}_q \leftarrow \mathbf{w}_q - \eta \mathbf{x}_n\)。多类感知器学习如算法 8.2 所示。

### 算法 8.2 多类感知器学习

输入：训练数据 \(X=\{\mathbf{x}_1,\dots,\mathbf{x}_N\}\) 和学习率 \(\eta > 0\)。

输出：训练好的单层多类感知器，其最优权重集为 \(\mathbf{w}\)。

```text
1: Initialize the set of weights W = (w1, ..., wK) to zero; K is the number of classes.
2: repeat
3:   for n in {1,...,N} do
4:     for j in {1,...,K} do
5:       Compute the j-th neuron output o_nj = w_j^T x_n
6:     end for
7:     Get q = arg max_j o_nj
8:     Get k index of correct category of x_n
9:     if k != q then   # misclassified data
10:      w_k <- w_k + η x_n   # adjust right category
11:      w_q <- w_q - η x_n   # adjust wrong category
12:    end if
13:  end for
14: until All training data are correctly satisfied or a specified minimum number of iterations are executed
```

### 8.3.1.3 感知器增强

感知器本质上是一种线性判别机。性能仅在有限次迭代步骤内对线性可分分类问题得到保证 [35,114]。此外，感知器对噪声非常敏感，这严重限制了其在现实场景中的性能。

使用边界 \(\gamma\) 作为性能权衡使我们能够将感知器适应具有挑战性的非线性场景。为了克服原始感知器在噪声环境下遇到的一些学习问题，已经提出了更鲁棒的感知器学习变体。口袋算法 [44] 在学习过程中保持一个“口袋”中的良好权重，并在标准感知器次优时使用口袋中的良好权重估计。Adatron [3] 提出了一种高效的自适应学习方案，而投票感知器 [41] 在学习过程中嵌入了边界最大化。事实上，已经证明投票感知器可以实现与基于核的支持向量机相似的性能，同时是一个更简单、更容易训练的模型。

### 8.3.2 Adaline

自适应线性神经元 Adaptive Linear Neuron (ADALINE) 由 Widrow 和 Hoff [5] 于 1960 年提出，作为 McCulloch 和 Pitts [91] 二进制阈值门的改编。像感知器一样，adaline 是一个单层神经网络，具有由多个单元组成输入层和单个输出单元。并且像感知器一样，输出单元是线性阈值单元。然而，而感知器侧重于优化净值函数的符号，adaline 侧重于最小化净值与目标之间的平方误差。我们首先描述针对两类问题的原始 adaline 网络，然后描述多类设置的扩展。

### 8.3.2.1 两类 Adaline

对于两类分类问题 \(C_1\) 和 \(C_2\)，标签为 \(-1\) 和 \(+1\)，adaline 具有单个阈值线性神经元，其权重向量 \(\mathbf{w}=(w_1,\dots,w_d)\) 从输入节点接收数据并产生输出 \(o \in \{-1,1\}\)，类似于感知器。与感知器不同，adaline 优化代价函数 \(E_a\)，定义为局部均方误差之和：

\[
E_a = \sum_n (t_n - v_n)^2 \tag{8.28}
\]

其中 \(t_n\) 为样本 \(\mathbf{x}_n\) 的期望输出，\(t_n \in \{-1,1\}\)，\(v_n\) 为输出单元的净值。该误差使用净值而非输出值定义。adaline 准则的最小化是一个自适应（迭代）过程，以 Widrow-Hoff 学习规则实现，也称为 delta 规则：

\[
\mathbf{w} \leftarrow \mathbf{w} + \eta (t_n - v_n) \mathbf{x}_n \tag{8.29}
\]

