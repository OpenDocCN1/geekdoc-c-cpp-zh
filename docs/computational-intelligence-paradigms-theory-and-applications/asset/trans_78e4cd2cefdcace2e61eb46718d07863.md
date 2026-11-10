
![](img/d9a4cc12c48f7466f309cbd3c4549c73_111_0.png)

**图3.7：** 反向传播网络

以及网络中的输出处理单元。然后将该结果再除以一个五到十之间的缩放因子。较大的缩放因子用于相对含噪的数据。高度含噪的输入数据需要二十或五十的因子，而与输出单元有精确关系的非常无噪声的输入数据可能映射到大约二。因此，隐藏层有必要具备若干处理单元。

网络一经创建，教学（训练）过程便开始了。这种教学利用一种学习规则，它是 Delta 规则的变体。该规则首先确定误差，即实际输出与期望输出之间的差值。基于该误差，连接权重按误差的比例增加，以获得全局精度。在对单个节点执行此操作时，输入、输出和期望输出应出现在同一处理单元处。该学习规则的复合部分用于让系统确定哪个输入对错误输出的贡献最大，以及该元素如何改变以纠正误差。非活动节点不会对误差有贡献，也无需更新其权重。

为解决这个问题，训练输入被送入网络的输入层，并在输出层比较期望输出。在学习过程中，通过网络进行前向扫描，逐层计算每个单元的输出。实际输出与目标输出之间的差值被反向传播到前一层（或多层），该差值由传递函数的导数修正，连接权重通常使用 Delta 规则进行调整。此过程对前一层（或多层）继续进行，直到到达输入层。

反向传播网络的学习规则有许多变体。可以使用不同的误差函数、传递函数，甚至传递函数导数的修正方法。引入动量误差的概念，是为了在最小化不稳定行为的同时实现更迅速的学习。在这里，误差函数或 delta 权重方程经过修改，使得前一次 delta 权重的一部分被传递到当前 delta 权重中。用工程术语来说，这相当于对 delta 权重项施加低通滤波器，因为总体趋势得到增强，而振荡行为被抵消。这允许使用较低的、通常较慢的学习系数，但能产生更快的学习。

另一种用于使网络收敛的常见技术是，仅在向网络呈现许多对输入及其期望输出之后更新权重，而不是在每次呈现之后更新。这种网络称为累积反向传播，因为直到呈现完整的一对集合后，delta 权重才会累积。在累积期间呈现的输入-输出对的数量称为一个 epoch（轮次）。该 epoch 可以对应于完整的训练对集合，也可以对应于一个子集。

## 反向传播网络的算法

本节讨论前馈反向传播网络的训练算法和应用算法。

### 训练算法

反向传播的训练算法涉及四个阶段：

- 1. 权重初始化
- 2. 前馈
- 3. 误差反向传播
- 4. 权重和偏置的更新

在第一阶段，即权重初始化阶段，会分配一些小的随机值。

在前馈阶段，每个输入单元（Xᵢ）接收输入信号，并将该信号传送到每个隐藏单元 z₁ ... zₚ。每个隐藏单元随后计算激活函数，并将其信号 zᵢ 发送到每个输出单元。输出单元计算激活函数，以形成网络对给定输入模式的响应。

在误差反向传播期间，每个输出单元将其计算出的激活值 yₖ 与其目标值 tₖ 进行比较，以确定该模式在该单元处相关联的误差。基于该误差，计算因子 δₖ（k=1 ... m），并用于将输出单元 yₖ 处的误差分配回前一层中的所有单元。类似地，为每个隐藏单元 zⱼ 计算因子 δⱼ（j=1 ... p）。

在最后阶段，使用 δ 因子和激活值更新权重和偏置。

### 参数

训练算法中使用的各种参数如下：

- x：输入训练向量 x = (x₁, ..., xₙ)
- t：输出目标向量 t = (t₁, ..., tₘ)
- δₖ := 输出单元 yₖ 的误差
- δⱼ := 隐藏单元 zⱼ 的误差
- α := 学习率
- v₀ⱼ := 隐藏单元 j 的偏置
- zⱼ := 隐藏单元 j
- w₀ₖ := 输出单元 k 的偏置
- yₖ := 输出单元 k

反向传播网络训练算法的伪代码如下。该算法按各个阶段给出：

```
Initialization stage:
Initialize weights v and w to small random values
Initialize learning rate
While not stopping condition for phase I DO
    For each training pair

        Feed forward stage:
        Each input unit receives the input signal $x_i$ and transmits to all units in the hidden layer.
        Each hidden unit $(z_j,\ j=1,\ldots,p)$ sums its weighted input signals:
        $$z_{in_j}=v_{0j}+\sum_{i=1}^{n}x_i v_{ij}$$
        Applying activation function:
        $$z_j=f(z_{in_j})$$
        and sends this signal to all units.
        Each output unit $(y_k,\ k=1,\ldots,m)$ sums its weighted input signals:
        $$y_{in_k}=w_{0k}+\sum_{j=1}^{p}z_j w_{jk}$$
        Applies its activation function to calculate output signals:
        $$y_k=f(y_{in_k})$$

        Back propagation of errors:
        Each output unit $(y_k,\ k=1,\ldots,m)$ receives a target pattern corresponding to an input pattern; error information term is calculated as:
        $$\delta_k=(t_k-y_k)f'(y_{in_k})$$
        Each hidden unit $(z_j,\ j=1,\ldots,p)$ sums its delta inputs from units in the layer above:
        $$\delta_{in_j}=\sum_{k=1}^{m}\delta_k W_{jk}$$
        The error information is calculated as:
        $$\delta_j=\delta_{in_j}f'(z_{in_j})$$

        Updation of weights and biases:
        Each output unit $(y_k,\ k=1,\ldots,m)$ updates its bias and weights $(j=0,\ldots,p)$. The weight correction term is given by:
        $$\Delta W_{jk}=\alpha\delta_k z_j$$
        The bias correction term is given by:
        $$\Delta W_{0k}=\alpha\delta_k$$
        $$W_{jk(new)}=W_{jk(old)}+\Delta W_{jk};\quad W_{0k(new)}=W_{0k(old)}+\Delta W_{0k}$$
        Each hidden unit $(z_j,\ j=1,\ldots,p)$ updates its bias and weights $(i=0,\ldots,n)$.
        The weight correction term
        $$\Delta V_{ij}=\alpha\delta_j x_i$$
        The bias correction term
        $$\Delta V_{0j}=\alpha\delta_j$$
        $$V_{ij(new)}=V_{ij(old)}+\Delta V_{ij},\quad V_{0j(new)}=V_{0j(old)}+\Delta V_{0j}$$
    End For
    Test the stopping condition
End while
End
```

停止条件可以是最小化误差、epoch 数量等。

### 参数选择

用于训练的参数应选择为使网络高效运行。初始值分配将在下一节讨论。

**初始权重：** 初始权重决定误差梯度是否达到全局（或仅局部）最小值，以便网络收敛。如果初始权重过大，则到每个隐藏单元或输出单元的初始输入信号将落入饱和区，其中 sigmoid 的导数具有非常小的值（f(net)=0）。如果初始权重过小，则到隐藏单元或输出单元的净输入将趋近于零，从而导致学习极其缓慢。为了获得最佳结果，初始权重和偏置设置为 -0.5 到 0.5 之间或 -1 到 1 之间的随机数。

**学习率的选择：** 高学习率会导致快速学习，但权重可能振荡；而较低学习率会导致学习较慢。采用学习率的建议方法如下：

- 从高学习率开始并稳步降低它。权重向量的变化必须很小，以减少振荡或任何发散。
- 一个简单的建议是，增大学习率以改善性能，减小学习率以使性能变差。
- 另一种方法是将学习率加倍，直到误差值变差。

