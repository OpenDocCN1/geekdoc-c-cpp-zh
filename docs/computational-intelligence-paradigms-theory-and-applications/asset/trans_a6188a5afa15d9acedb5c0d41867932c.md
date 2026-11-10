

![](img/d9a4cc12c48f7466f309cbd3c4549c73_167_0.png)

**图4.10：汉明网络架构**

## 应用流程

所用参数为，

- n —— 输入节点（输入向量）的数量
- m —— 输出节点（示例向量）的数量
- e(j) —— 第 j 个示例向量

应用流程的伪代码如下：

```
Initialize weights for storing m exemplar vectors
wᵢⱼ = eᵢ(j)/2, (i=1..n, j=1..m)
Initializing the bias
bⱼ = n/2 (j=1..m)
For each vector x
    Compute the net input to each unit yⱼ
    Y_inⱼ = bⱼ + ∑ᵢ₌₁ⁿ xᵢwᵢⱼ
    Initialize activations for Max Net
    yⱼ(0) = y_inⱼ (j=1,..m)
    Max net iterates to find the best match exemplar
End For
```

与霍普菲尔德网络相比，汉明网络更具优势。当输入位错误具有随机性时，汉明网络采用最优最小误差分类器对输入向量进行分类。与霍普菲尔德网络相比，汉明网络使用的处理单元更少。类别层对整个类别只需要一个元素，而不是为每个输入节点设置单独元素。汉明网络比霍普菲尔德网络更快、更准确，因为它稳定所需时间更少。

## 4.3.5 双向联想记忆

Bart Kosko 开发了一种模型来推广霍普菲尔德模型，这被称为双向联想记忆（BAM）。在 BAM 中，模式以一对双极向量的形式表示；当呈现含噪输入时，会确定与该输入模式关联的最近模式。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_168_0.png)

**图4.11：双向联想记忆示例**

双向联想记忆网络的基本模型如图4.11所示。BAM 模型的作用等同于输出处理节点。隐藏层由独立的关联存储器组成，并表示输入向量的大小。各单元的长度不必相等。中间层彼此全连接。输入层和输出层仅用于实现目的；它们是向网络输入信息和从网络检索信息的手段。Kosko 最初的研究目标是用于光学处理的双向联想记忆层，这种处理不需要正式的输入和输出结构。

向量以关联对的形式存储在中间层。每当呈现含噪模式时，中间层会来回摆动，直到达到稳定状态。稳定状态表示最近学习到的关联，并给出与最初呈现的输入模式相似的最佳输出。与霍普菲尔德网络类似，当训练集的补集被用作未知输入向量时，双向联想记忆网络容易错误地找到已训练模式。

### 架构

BAM 中的层称为 X 层和 Y 层，而不是输入层和输出层，因为权重是双向的，并且算法在更新各层激活值之间交替进行。BAM 有三种形式：

- 1. 二值型
- 2. 双极型
- 3. 连续型

但这三种类型的架构保持不变。BAM 的架构如图4.12所示。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_169_0.png)

**图4.12：双向记忆网络架构**

异联想 BAM 网络在 X 层有“n”个单元，在 Y 层有“m”个单元。层间连接是双向的，即如果从 X 层发送到 Y 层的信号的权重矩阵为 W，则从 Y 层发送到 X 层的信号的权重矩阵为 W_T。

BAM 架构类似于单层前馈网络，仅由一层加权互连组成。输入层有“n”个输入神经元，输出层有“m”个输出神经元。训练过程基于赫布学习规则。这是一个全互连网络，其中输入和输出不同。双向联想记忆最重要的特征是，从 X 层到 Y 层以及从 Y 层到 X 层都存在加权互连。一层到另一层及其反向连接在图4.12中用双向箭头表示。权重在 X 层与 Y 层之间以及从 Y 层到 X 层进行调整。

### 双向联想记忆网络的类型

BAM 有两种类型。它们是：

- 离散 BAM
- 连续 BAM

### 离散 BAM

训练模式可以是二值型或双极型。在两种格式中，权重均由训练向量对的双极形式的赫布外积之和求得。使用带阈值的阶跃激活函数作为激活函数。通常，双极向量能改善网络的性能。

用于存储输入向量和目标向量集合 $s(p): t(p)$（$p=1,\ldots,P$）的权重矩阵，其中

$$s(p)=(s_1(p),\ldots,s_i(p),\ldots,s_n(p))$$

并且可以借助赫布规则确定。

对于二值输入向量，权重矩阵可由以下公式确定。

$$W_{ij}=\sum_p(2s_i(p)-1)(2t_j(p)-1)$$

对于双极输入向量，权重矩阵由下式给出：

$$W_{ij}=\sum_p s_i(p)t_j(p)$$

### 激活函数

离散 BAM 的激活函数取决于使用的是二值向量还是双极向量。激活函数是相应的阶跃函数。对于二值输入向量，Y 层的激活函数为

$$y_j = \begin{cases} 1, & \text{if } y_{inj} > 0 \\ y_j, & \text{if } y_{inj} = 0 \\ 0, & \text{if } y_{inj} < 0 \end{cases}$$

X 层的激活函数为

$$x_i = \begin{cases} 1, & \text{if } x_{inj} > 0 \\ x_i, & \text{if } x_{inj} = 0 \\ 0, & \text{if } x_{inj} < 0 \end{cases}$$

对于双极向量，Y 层的激活函数为

$$y_j = \begin{cases} 1, & \text{if } y_{inj} > \theta_j \\ y_j, & \text{if } y_{inj} = \theta_j \\ -1, & \text{if } y_{inj} < \theta_j \end{cases}$$

X 层的激活函数为

$$x_i = \begin{cases} 1, & \text{if } x_{inj} > \theta_i \\ x_i, & \text{if } x_{inj} = \theta_i \\ -1, & \text{if } x_{inj} < \theta_i \end{cases}$$

如果净输入等于阈值，激活函数会决定将该单元的激活值保持在其前一值。上式中，$\theta_i$ 表示阈值。

### 连续 BAM

连续 BAM 由 Kosko 于1988年提出。连续双向联想记忆能够将输入平滑且连续地转换到 [0,1] 区间内的相应输出范围。连续 BAM 对所有单元使用逻辑 S 形函数作为激活函数。

对于二值输入向量 $(s(p),t(p))$，$p=1,2,\ldots,P$，权重由以下公式确定。

$$w_{ij}=\sum_p (2s_i(p)-1)(2t_j(p)-1)$$

Y 层

逻辑 S 形激活函数由下式给出：

$$f(y_{inj})=\frac{1}{1+\exp(-y_{inj})}$$

若计算中包含偏置：

$$y_{inj}=b_j+\sum_i x_iw_{ij}$$

### X 层

逻辑 S 形激活函数由下式给出：

$$f(x_{inj})=\frac{1}{1+\exp(-x_{inj})}$$

若计算中包含偏置：

$$x_{inj}=b_j+\sum_i x_iw_{ij}$$

根据 Haines 和 Hecht-Nielsen 的研究，BAM 的存储容量为 min(n, m)，其中，  
n 是 X 层中的单元数，  
m 是 Y 层中的单元数。  
需要注意的是，如果为每个单元选择合适的非零阈值，这一容量可扩展到 min(2n, 2m)。

### 应用算法

从训练过程中获得最终权重。输入模式被呈现给 X 层和 Y 层。计算 Y 层的净输入和激活值。然后将信号发送到 X 层，并在此处求出其净输入和激活值。以这种方式测试双向联想记忆的性能。双向记忆网络的伪代码如下：

```
Initialize the weight to store a set of P vectors
Initialize all activations to 0

For each testing input
    Assign activation of X-layer to current pattern
    Input pattern y is presented to the Y-layer
    While activations are not converged do
        Compute the net input y_{inj} = ∑_i w_{ij}x_i
        Compute activations, y_i = f(y_{inj})
        Send signals to the X-layer
        Compute the net input x_{ini} = ∑_i w_{ij}y_i
        Compute the activations x_i = f(x_{ini})
        Send signals to the Y-layer
```

