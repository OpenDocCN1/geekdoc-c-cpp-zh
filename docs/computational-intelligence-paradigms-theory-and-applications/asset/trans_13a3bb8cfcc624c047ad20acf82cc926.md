
$$\begin{aligned}
u_{jk(\mathrm{new})} &= u_{jk(\mathrm{old})}+\alpha(y_k-u_{jk(\mathrm{old})}) \\
&= (1-\alpha)u_{jk(\mathrm{old})}+\alpha y_k;\quad k=1\text{ to }m \\
t_{ji(\mathrm{new})} &= t_{ji(\mathrm{old})}+\alpha(x_i-t_{ji(\mathrm{old})}) \\
&= (1-\alpha)t_{ji(\mathrm{old})}+\alpha x_i;\quad i=1\text{ to }n
\end{aligned}$$

所示的权重变化为学习率乘以误差。

### 训练算法

使用的参数如下

- \(x\) - 输入训练向量 \(x=(x_1, \ldots, x_i, \ldots, x_n)\)
- \(y\) - 目标输出向量 \(Y=(y_1, \ldots, y_k, \ldots, y_m)\)
- \(z_j\) - 簇单元 \(Z_j\) 的激活值
- \(x^*\) - 向量 \(x\) 的近似
- \(y^*\) - 向量 \(y\) 的近似
- \(v_{ij}\) - 从 x 输入层到 Z 簇层的权重
- \(u_{jk}\) - 从 x 输入层到 Z 簇层的权重
- \(t_{ji}\) - 从 x 输入层到 X 簇层的权重
- \(u_{ik}\) - 从 x 输入层到 Y 簇层的权重
- \(\alpha, \beta\) - Kohonen 学习期间的学习率
- \(a, b\) - Grossberg 学习期间的学习率

该算法使用欧氏距离法或点积法来计算获胜单元。获胜单元在训练的第一阶段和第二阶段都会被计算。在训练的第一阶段，使用 Kohonen 学习规则进行权重更新；在训练的第二阶段，使用 Grossberg 学习规则。

完整 CPN 的伪代码如下，

```
Initialize weights v and w
Initialize learning rates α and β
While not stopping condition for phase I Do
    For each training input pair x:y
        Assign X input layer activations to vector x
        Assign Y input layer activations to vector y
        Calculate winning cluster D(j) = ∑ᵢ (xᵢ - vᵢⱼ)², i = 1 to n
        Update weights
        v_ij(new) = v_ij(old) + α(x_i - v_ij(old)); i = 1 to n
        w_jk(new) = w_jk(old) + β(y_k - w_jk(old)); k = 1 to m
    End For
    Reduce learning rates α and β
    Test stopping condition for Phase I training
End while
While not stopping condition for phase II Do
    For each training input pair x:y
        Assign X input layer activations to vector x
        Assign Y input layer activations to vector y
        Calculate winning cluster D(j) = ∑ᵢ (xᵢ - vᵢⱼ)²; i = 1 to n
        Update weights from unit z_j to the output layers
        (α and β are constant in this phase)
        U_ij(new) = w_jk(old) + α(y_k - w_jk(old)); k = 1 to m
        t_ij(new) = t_ij(old) + α(x_i - t_ij(old)); i = 1 to n
    End For
    Reduce learning rates α and β
    Test for stopping condition for phase II training
End while
```

获胜单元的选择通过点积或欧氏距离完成。

点积通过计算净输入得到。

$$Z_{inj} = \sum_i x_i v_{ij} + \sum_k y_k w_{kj}$$

净输入最大的簇单元为获胜者。此处向量应归一化。在欧氏距离中，

$$D_j = \sum_i (x_i - v_{ij})^2$$

与输入向量的距离平方最小者为获胜者。

若获胜单元的选择出现平局，则选择索引最小的单元。

与获胜的 Kohonen 神经元相关联。这会将权重向量移动到输入向量所在区域。训练开始时，权重调整仅限于最接近获胜者的那些 Kohonen 神经元。该调整半径逐渐减小，直到仅调整与获胜 Kohonen 神经元相关联的权重。

还有一种方法，为每个 Kohonen 神经元赋予一个“良心”。如果它获胜的时间超过了其应得份额，例如 1/k（其中 k 是 Kohonen 神经元数量），它就会提高阈值以降低自己的获胜机会，从而让其他神经元有机会接受训练。由此可对权重进行初始化。

### 4.2.4 概率神经网络

概率神经网络的发展基于 Parzen 窗，这些网络由 Donald Specht 根据其论文设计。论文《用于分类、映射或联想记忆的概率神经网络》和《概率神经网络》分别于 1988 年和 1990 年发表。模式分类是该网络的主要应用领域，且该网络基于贝叶斯理论。贝叶斯理论于 20 世纪 50 年代发展起来，它允许考虑事件的相对似然，并应用先验信息来改善预测。贝叶斯理论所需的概率密度函数使用 Parzen 窗构建。

概率神经网络的学习过程是一种监督学习，在此学习过程中，分布函数在模式层内形成。这些分布函数用于估计输入特征向量的似然性。学到的模式按照先验概率（也称为相对频率）进行分组，以确定给定输入向量最可能的类别。如果具备关于先验概率的知识，则假定所有类或类别都是等可能的。特征向量根据输入特征向量与某类分布函数之间的最短欧氏距离来确定类别。

概率神经网络的基本结构如图 4.4 所示。基本架构包含三层：输入层、模式层和输出层。输入层具有许多元素，因为描述待分类对象需要可分离参数。模式层以如下方式组织训练集：每个输入向量都由一个独立的处理单元表示。输出层也称为求和层，根据待识别的类别具有大量处理单元。求和层中的每个处理单元都与模式层中的处理单元结合；如果它们关联到同一类别，则生成该类别作为输出。根据应用情况，如果输入在进入网络之前尚未归一化，偶尔会添加第四层来对输入向量进行归一化。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_151_0.png)

图 4.4：一个概率神经网络示例

模式层构成了贝叶斯分类器的神经网络实现，其中依赖于类别的概率密度函数（PDF）使用 Parzen 估计器近似。通过使用 Parzen 估计器确定 PDF，可最小化对训练集进行错误分类的期望风险。使用 Parzen 估计器时，只要训练集能充分表示类别差异，随着训练样本数量增加，分类会越来越接近真实的底层类别密度函数。

模式层由与训练集中每个输入向量相对应的一个处理单元组成。每个输出类别应包含相同数量的处理单元，否则少数类别可能会被错误地偏向，从而导致分类结果较差。模式层中的每个处理单元只训练一次。当输入向量与训练向量匹配时，处理单元被训练为返回高输出值。为了获得更好的泛化能力，在训练网络时加入平滑因子。在这种情况下，训练向量在训练集中不必按任何预定义顺序排列，因为特定向量的类别由输入的期望输出指定。学习函数仅选择正确输出类别中的第一个未训练处理单元，并更新其权重以匹配训练向量。

模式层基于竞争对输入向量进行分类，其中只有与输入向量匹配度最高者获胜并生成输出。因此，对于任何给定输入向量仅生成一个分类类别。如果输入模式与编程到模式层中的模式之间没有关系，则不生成输出。

为了微调对象分类，加入了 Parzen 估计器。该过程通过将构建到处理单元中的每个训练模式的出现频率相加来执行。从根本上说，一个类别中每个示例发生的概率分布会乘入其各自的训练节点。类似地，将对象更准确的期望添加到特征中，使其可被识别为该类别的成员。

与前馈反向传播网络相比，概率神经网络的训练要简单得多。无论如何，如果类别之间的差异变化很大，模式层可能会非常庞大。这种网络有许多支持者，因为其优化基础建立在众所周知的经典数学之上。

由于概率网络基于贝叶斯理论进行分类，因此必须以贝叶斯最优方式将输入向量分类为两个类别之一。该理论提供了一种代价函数，以涵盖以下事实：将实际上属于类别 A 的向量错误分类，可能比将属于类别 B 的向量错误分类更糟。贝叶斯规则将一个属于类别 A 的输入向量分类为，

$$P_A C_A f_A(x) > P_B C_B f_B(x)$$

其中，
- \(P_A\) - 类别 A 中模式出现的先验概率
- \(C_A\) - 与向量分类相关的代价
- \(f_A(x)\) - 类别 A 的概率密度函数

使用贝叶斯理论估计的 PDF 应在所有 x 上为正且可积，并且结果必须为 1。

概率神经网络使用以下公式来估计概率密度函数，

$$f_A(x)=\frac{1}{(2\pi)^{n/2}\sigma^n}\frac{1}{m_A}\sum_{i=1}^{m_A}\exp\left[-\frac{(x-x_{Ai})^T(x-x_{Ai})}{2\sigma^2}\right]$$

