
![](img/d9a4cc12c48f7466f309cbd3c4549c73_103_0.png)

**图 3.4：** 原始感知机

- 3. 激活函数 *f(x)* 限制神经元的输出。通常输出被限制在区间 [0,1]，或者也可以为 [-1,1]。

单层感知机的架构如图 3.5 所示。响应单元的输入是关联单元的输出，它是一个二值向量。由于权重调整仅在关联单元和响应单元之间进行，因此该网络被称为单层网络。所示架构仅由关联单元和响应单元组成。输入层由神经元 X₁、...、Xₙ 组成，这些神经元通过加权互连与输出神经元相连。存在一个公共偏置“1”。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_104_0.png)

**图 3.5：** 单层感知机的架构

## 算法

单层感知机的训练和测试算法如下所示。该算法可在 MATLAB 中实现。

### 参数

```
x: Input vector (x₁, ..., xᵢ, ..., xₙ)
t: Target vector
w: Weight vector for the output unit (w₁, ..., wⱼ, ..., wₙ)
y: Activation function f(y_in)
b: Bias value
θ: Threshold value
```

### 训练算法

单层感知机训练算法的伪代码如下所示

```
Initialize the weights (either to zero or to a small
random value)
Set learning rate α (in the interval [0,1])
While not stopping condition do,
    For each training pair s:t
        Assign input unit activations xᵢ = sᵢ
        Compute the response of output unit:

            y_in = b + ∑ᵢ xᵢwᵢ

            y = f(y_in) = ⎧  1,        if y_in > θ
                         ⎨  0,        if −θ ≤ y_in ≤ θ
                         ⎩ −1,        if y_in < −θ

Update weights and bias according to,
    If y ≠ t,
        wᵢ(new) = wᵢ(old) + αtxᵢ
        b(new) = b(old) + αt
```

```
    If y_j ≠ t_j,
        w_ij(new) = w_ij(old) + αt_jx_i
        b_j(new) = b_j(old) + αt_j
    else
        w_i(new) = w_i(old)
        b(new) = b(old)

    End If
End For
End While
```

### 多输出类别的感知机测试算法

具有多个输出类别的单层感知机测试算法伪代码如下所示

```
Set the weights from the training algorithm
For each input vector x
    Compute the response of output unit:
        y_in_j = Σ_i x_i w_i
        y = f(y_in_j) = {
            1,   if y_in_j > θ
            0,   if -θ ≤ y_in_j ≤ θ
            -1,  if y_in_j < -θ
        }
End For
End
```

## 3.3.2 感知机网络的 MATLAB 实现

考虑一个 4 输入 1 输出的问题，其中如果输入模式中 1 的个数为奇数，则输出应为“一”，否则输出应为“零”。

录入输入向量和目标向量

```matlab
clear
inp = [0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1;
       0 0 0 0 1 1 1 1 0 0 0 0 1 1 1 1;
       0 0 1 1 0 0 1 1 0 0 1 1 0 0 1 1;
       0 1 0 1 0 1 0 1 0 1 0 1 0 1 0 1];
out = [0 1 1 0 1 0 0 1 1 0 0 1 0 1 1 0];
```

使用 MATLAB 神经网络工具箱中的 newff 函数创建一个网络。newff 函数创建一个前馈网络。它需要四个输入，并返回网络对象。第一个输入是一个 R×2 矩阵，包含输入向量 R 个元素各自的最小值和最大值。第二个输入是一个数组，包含各层的大小。第三个输入是一个元胞数组，包含各层要使用的传递函数名称。最后一个输入包含要使用的训练函数名称。

```matlab
network = newff([0 1; 0 1; 0 1; 0 1], [6 1], {'logsig','logsig'});
```

在训练前馈网络之前，必须初始化权重和偏置。newff 命令会自动初始化权重，但可能需要重新初始化它们。这可以通过 init 命令完成。

```matlab
network = init(network);
```

sim 函数用于模拟网络。sim 函数接收网络输入和网络对象 net，并返回网络输出。

```matlab
y = sim(network, inp);
figure, plot(inp, out, inp, y, 'o'),
title('Before Training');
axis([-5 5 -2.0 2.0]);
```

与 traingd 相关的七个训练参数为：epochs、show、goal、time、min_grad、max_fail 和 lr。这里定义了迭代次数和学习率，如下所示

```matlab
network.trainParam.epochs = 500;
network.trainParam.lr = 0.05;
```

训练网络。模拟网络并绘制结果（图 3.6）

```matlab
network = train(network, inp, out);
y = sim(network, inp);
figure, plot(inp, out, inp, y, 'o'),
title('After Training');
axis([-5 5 -2.0 2.0]);
```

更新后的权重和偏置值

```matlab
Layer1.Weights = network.iw1
Layer1.Bias = network.b1
Layer2.Weights = network.lw2
Layer2.Bias = network.b2
Actual.Desired = [y' out']
```

输出：
```
TRAINLM, Epoch 0/500, MSE 0.376806/0,
Gradient 0.527346/1e-010
TRAINLM, Epoch 25/500, MSE 5.86095e-005/0,
Gradient 0.0024019/1e-010
TRAINLM, Epoch 34/500, MSE 1.67761e-012/0,

Gradient 2.89689e-011/1e-010
TRAINLM, Minimum gradient reached, performance goal
was not met.

Layer1.Weights =

   -9.5620    9.4191    6.5063   -11.2360
    8.7636   10.0589  -10.4526    -8.9109
    9.8375  -11.4056   14.3788    -5.5974
    7.4334   10.0157  -13.7152     5.9788
  -10.6286   14.6436   10.6738   -15.2093
    8.7772   -6.0128    6.6699     9.0275

Layer1.Bias =

  -11.8265
   -5.8238
    4.2346
   -7.7644
   -5.0030
   -6.0732

Layer2.Weights =

  -28.4686   17.7464  -10.1867  -26.2315   28.9088
   27.1797

Layer2.Bias =

   -4.4138
```

![](img/d9a4cc12c48f7466f309cbd3c4549c73_109_0.png)

**图 3.6：** 训练前与训练后的模式，34 轮迭代结束时的性能与目标

## 3.3.3 前馈反向传播网络

前馈、反向传播架构由 Rumelhart、Hinton 和 Williams 于 20 世纪 70 年代初提出。目前，反向传播架构是用于复杂多层网络的最常见、最高效且简单的模型。该网络被广泛应用于图像处理、信号处理、人脸识别、语音识别等众多领域。这种网络架构已经衍生出大量具有不同拓扑结构和各种训练方法的网络类型。其主要能力是针对未定义问题获得非线性解。

### 架构

典型的反向传播网络具有一个输入层、一个输出层以及至少一个隐藏层。隐藏层的数量没有理论限制，但通常只有一层或两层。已有研究表明，解决任意复杂度的问题至少需要四层（三个隐藏层加一个输出层）。每一层都与后续层全连接，如图 3.7 所示。

输入层和输出层表示回忆期间的信息流。回忆是将输入数据输入已训练的网络并接收答案的过程。反向传播不在回忆期间使用，而仅在网络学习训练集时使用。

层数以及每层处理单元的数量是重要的决策。这些前馈反向传播拓扑的参数也是最难以捉摸的。只有一些随着时间积累、并被大多数将这一架构应用于其问题的研究人员和工程师遵循的一般规则。

- *规则 A：隐藏层中处理单元的数量应随着输入输出关系复杂度的增加而增加。*
- *规则 B：如果所建模的过程可分离为多个阶段，则可能需要额外的隐藏层。如果该过程不可分离为多个阶段，那么额外的层可能只是实现记忆，而不是真正的通用解。*
- *规则 C：可用训练数据量设定了隐藏层中处理单元数量的上限。要计算这个上限，请使用训练集中输入输出对示例的数量，并将该数量除以输入的总数*
