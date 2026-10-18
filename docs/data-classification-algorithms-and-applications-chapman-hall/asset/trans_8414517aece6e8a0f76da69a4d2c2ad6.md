

将输出层记为 \(\mathcal{H}_L\)，输入层记为 \(\mathcal{H}_0\)，权重更新为

\[
\nabla w_{ij}^{(l)} = -\eta \, \delta_j^{(l)} z_i^{(l-1)} \tag{8.73}
\]

对任意给定权重 \(w_{ij}^{(l)}\) 和 \(l \in \{1,\dots,L\}\)，其中 \(\delta_j^{(l)}\) 通常被称为层 \(\mathcal{H}_l\) 中单元 \(j\) 的“信用”。我们指出，MLP 在公式 8.73 中的权重更新实现了 Hebbian 学习规则。

要更新单元的权重需要计算该单元的信用。计算每个单元的信用取决于其在网络中的位置。对应于第 \(k\) 个输出单元（为简单起见，不使用 softmax 变换）的信用 \(\delta_k\) 为

\[
\delta_k = \frac{\partial E}{\partial o_k} \frac{\partial o_k}{\partial v_k^{(L)}} \tag{8.74}
= \varphi'(v_k^{(L)}) \frac{\partial E}{\partial o_k} \tag{8.75}
\]

其中 \(\varphi'(\cdot)\) 是激活函数的导数。当使用 sigmoid 函数和 MSE 准则时，输出单元的信用为

\[
\delta_k = \varphi(v_k)(1 - \varphi(v_k))(o_k - t_k) \tag{8.76}
= o_k(1 - o_k)(o_k - t_k) \tag{8.77}
\]

对于层 \(\mathcal{H}_l\) 中的隐藏单元，其信用 \(\delta_h^{(l)}\) 取决于其在层 \(\mathcal{H}_{l+1}\) 中的接收单元：

\[
\delta_h^{(l)} = \frac{\partial E}{\partial z_h^{(l)}} \frac{\partial z_h^{(l)}}{\partial v_h^{(l)}} \tag{8.78}
= \varphi'(v_h^{(l)}) \sum_{h' \in \mathcal{H}_{l+1}}
\frac{\partial E}{\partial v_{h'}^{(l+1)}} \frac{\partial v_{h'}^{(l+1)}}{\partial z_h^{(l)}} \tag{8.79}
= z_h^{(l)}(1 - z_h^{(l)}) \sum_{h' \in \mathcal{H}_{l+1}}
\delta_{h'}^{(l+1)} w_{hh'}^{(l+1)} \tag{8.80}
\]

其中我们在推导公式 8.80 时假设使用了 sigmoid 函数。

信用是使用公式 8.77 从输出单元计算出来，然后使用公式 8.80 传播到隐藏层。这两个公式是反向传播算法的基础，使其能够通过将信用从输出层传播到隐藏层来计算每个权重的梯度下降。反向传播算法在算法 8.4 中进行了说明。

## 8.5.4 增强反向传播

标准反向传播算法是一种一阶优化方法。其收敛性对网络大小、数据中的噪声水平以及学习率的选择高度敏感：收敛可能缓慢，并且可能导致误差曲面的不良局部最小值 [7]。可以通过数据归一化和使用标准梯度下降方法的增强替代方案来提高反向传播算法的性能。因此，在呈现给 MLP 之前，数据通常被归一化到 \([-1, 1]\) 之间。同样，在反向传播之前，网络权重通常以零均值和方差为 1 进行初始化。

### 算法 8.4 反向传播算法

**输入：** 训练数据 \(X = \{x_1, \dots, x_N\}\) 和相关目标 \(\{t_1, \dots, t_N\}\)；\(x_n \in \mathbb{R}^d\)，\(t_n = (t_{n1}, t_{n2}, \dots, t_{nK})\) 且 \(t_{nk} = \delta_{jk}\) 为 \(x_n \in C_j\) 的克罗内克记号；学习率 \(\eta > 0\)。

**输出：** 具有最优权重集 \(w\) 的训练好的多层感知器。

```text
1: Randomly initialize the set of weights w = {w_ij} with zero means and unit variance, preferably
2: for t in {1, ..., T} do    # for each epoch up to T
3:   for n in {1, ..., N} do    # for each sample
4:     Forward propagation to get output o = (o1, ..., oK) and activations {z_j^(l)}
5:
6:     for l in {L, L-1, ..., 1} do
7:       for j in H_l do    # for all units in layer H_l
8:         if unit j is an output unit then
9:           δ_j = δ_j^(L) = o_j(1 - o_j)(o_j - t_j)
10:        end if
11:        if unit j is an internal hidden unit in layer H_l then
12:          δ_j^(l) = z_j^(l)(1 - z_j^(l)) Σ_{h ∈ H_{l+1}} δ_h^(l+1) w_{jh}^(l+1)
13:        end if
14:
15:        for i in H_{l-1} do
16:          w_{ij}^(l) ← w_{ij}^(l) - η(t) z_i^(l-1) δ_j^(l)    # weight update
17:        end for
18:
19:     end for
20:     end for
21:   end for
22: end for
23: w_{ij}^(l) : weight from unit i to unit j in layer H_l
24: z_i^(l) : output of unit i in layer H_l
25: η(t) : learning rate at iteration t
26: δ_j^(l) : error term (credit) of unit j in layer H_l
```

对梯度下降的增强包括，除其他技术外，使用动量平滑器 [116]、使用动态学习率 [7, 129]、弹性反向传播算法和 Quickprop 算法。

### 8.5.4.1 带动量的反向传播

使用动量因子 \(\alpha > 0\) 作为

\[
\Delta w = -\eta \frac{\partial E}{\partial w}(t) + \alpha \Delta w(t - 1) \tag{8.81}
\]

有助于缓解梯度下降过程中的噪声振荡。这假设梯度下降是在目标函数 \(E\) 上以批量方式进行的。

### 8.5.4.2 Delta-Bar-Delta

学习率的最佳选择取决于误差曲面的复杂性和网络架构。为了规避这一问题，delta-bar-delta 算法 [66] 为网络中的每个权重 \(w\) 分配一个单独的学习率 \(\eta_w\)。该权重在学习过程中根据梯度的方向进行更新。delta-bar-delta 算法对目标函数 \(\mathcal{E}\) 的操作如下。

首先，它在每次迭代 \(t\) 时估计误差导数的移动平均值 \(\widehat{\partial \mathcal{E}/\partial w}(t)\)，以减少梯度波动，如

\[
\widehat{\frac{\partial \mathcal{E}}{\partial w}}(t) = \beta \frac{\partial \mathcal{E}}{\partial w}(t)
+ (1 - \beta) \widehat{\frac{\partial \mathcal{E}}{\partial w}}(t - 1) \tag{8.82}
\]

其中 \(0 < \beta < 1\)。然后，单独的学习率按如下方式更新：

\[
\eta_w(t + 1) =
\begin{cases}
\eta_w(t) + \kappa, & \text{if } \widehat{\frac{\partial \mathcal{E}}{\partial w}}(t) \frac{\partial \mathcal{E}}{\partial w}(t - 1) > 0,\\[4pt]
(1 - \rho)\eta_w(t), & \text{if } \widehat{\frac{\partial \mathcal{E}}{\partial w}}(t) \frac{\partial \mathcal{E}}{\partial w}(t - 1) < 0,\\[4pt]
\eta_w(t), & \text{otherwise.}
\end{cases} \tag{8.83}
\]

当连续梯度指向同一方向时，学习率会增加，否则会减小。元学习参数 \(\kappa\)、\(\rho\)、\(\beta\) 的选择由各种考虑因素驱动，特别是数据类型。已建议使用动量来减少梯度振荡 [95]。更新以批量模式进行。一种可用于在线设置的 delta-bar-delta 算法的增量版本是可用的 [125]。

### 8.5.4.3 Rprop 算法

寻找抗噪声的反向传播算法一直是各种研究的主题 [63]。弹性反向传播 Rprop 算法 [112] 是解决这一问题的方案之一，因为它旨在消除更新步骤中误差导数范数的影响，而专注于通过监控其符号来关注梯度的方向。Rprop 对目标函数 \(\mathcal{E}\) 操作，并在时间 \(t\) 更新每个权重为

\[
\Delta w(t) = -\gamma_w(t) \operatorname{sign}\left(\frac{\partial \mathcal{E}}{\partial w}(t)\right) \tag{8.84}
\]

其中 \(\gamma_w\) 是在每次训练迭代 \(t\) 时跟踪的更新步长，并按如下方式更新

\[
\gamma_w(t + 1) =
\begin{cases}
\min\{\eta_+ \gamma_w(t), \gamma_{\max}\}, & \text{if } \frac{\partial \mathcal{E}}{\partial w}(t) \frac{\partial \mathcal{E}}{\partial w}(t - 1) > 0,\\[4pt]
\max\{\eta_- \gamma_w(t), \gamma_{\min}\}, & \text{if } \frac{\partial \mathcal{E}}{\partial w}(t) \frac{\partial \mathcal{E}}{\partial w}(t - 1) < 0,\\[4pt]
\gamma_w(t), & \text{otherwise.}
\end{cases} \tag{8.85}
\]

其中 \(0 < \eta_- < 1 < \eta_+\)，典型值分别为 0.5 和 1.2，且初始更新值设为 \(\delta_w = 0.1\)。

Rprop 的效果是在误差曲面的平坦区域和接近局部最小值的区域加速学习。更新量的大小通过使用 \(\gamma_{\min}\) 和 \(\gamma_{\max}\) 来限制，以适度加速。

### 8.5.4.4 Quick-Prop

二阶算法比单纯的梯度值考虑了更多关于误差曲面形状的信息。如果在每一步考虑误差曲面的曲率，可以进行更有效的优化。然而，这些方法需要估计 Hessian 矩阵，这对于前馈网络来说计算成本很高 [7]。可以采用伪牛顿方法来简化 Hessian 矩阵的形式 [10]，其中仅计算对角分量，得到

\[
\Delta w(t) = \frac{\frac{\partial \mathcal{E}(t)}{\partial w}}{\frac{\partial^2 \mathcal{E}(t)}{\partial w^2}} \tag{8.86}
\]

Quickprop 算法进一步将二阶导数 \(\frac{\partial^2 \mathcal{E}}{\partial w^2}\) 近似为一阶导数连续值的差，得到

\[
\Delta w(t) = \Delta w(t - 1)
\frac{\frac{\partial \mathcal{E}(t)}{\partial w}}
{\frac{\partial \mathcal{E}(t)}{\partial w} - \frac{\partial \mathcal{E}(t - 1)}{\partial w}} \tag{8.87}
\]

不需要矩阵求逆，且在寻找所需的二阶偏导数时所涉及的计算工作有限。Quick-prop 依赖于误差曲面的众多假设，包括二次形式和 Hessian 矩阵的非多元性质。因此，需要各种启发式方法使其在实践中工作。这包括将更新 \(\Delta w(t)\) 限制为某个最大值，并在近似 Hessian 的符号在多个连续迭代中未改变时切换到简单的梯度更新 [36, 37]。

## 8.5.5 泛化问题

泛化问题在机器学习中以及特别是在神经网络中是众所周知的。给定一个训练集，网络可能在训练集上实现良好的分类性能，但无法很好地推广到测试环境。这可能是由于多种因素造成的。一个因素是过度训练，即网络完美地学习数据集而不是学习底层映射。另一个因素是训练大小与参数数量之间的不平衡比率，其中权重数量相对于数据量过大。

*早停* 是一种广泛用于防止过拟合的方法。其思想是定期使用单独的验证集估计误差，并在验证集上的误差开始增加时停止训练。交叉验证是另一种替代方法，但需要训练多个网络，这可能耗时。改善泛化的另一种有用方法是 *带噪声训练* [2, 20]。向训练集添加小方差白噪声的效果等同于添加更多训练数据，这可能防止网络对特定数据集过拟合。

## 8.5.6 模型选择

*模型选择*，即适当选择单元数量，是一个困难的问题。对于 MLPs 有多种模型选择标准可用。除了标准模型选择标准如 AIC、BIC 和 MDL 外，特定于神经网络的标准包括广义最终预测误差 GPE [99] 和 Vapnik-Chervonenkis VC 维 [127]，它表达了网络实现最优分类任务的能力，并提供了实现目标误差概率所需的训练集数量的界限。然而，给定一个网络，估计 VC 界是一个具有挑战性的任务，有时会导致不合理的庞大网络。相反，最近的进展使用深度学习的概念来选择性地训练大型网络以实现准确的性能，正如我们将在下一节中看到的那样。

## 8.6 深度神经网络

深度学习方法旨在学习和利用神经网络生成其隐藏层中数据的内部特征表示的能力。如前所述，对于多层架构，每个隐藏层的输出是一组由

