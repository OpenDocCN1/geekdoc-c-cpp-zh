

使用附录 A.1.1 中分块矩阵的逆公式，联合分布的精度矩阵为

\(\left( \begin{array}{cc} C^{-1} + C^{-1}k(\mathbf{x}_*)k(\mathbf{x}_*)^T C^{-1} & -C^{-1}k(\mathbf{x}_*) \\ c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*) & \frac{-C^{-1}k(\mathbf{x}_*)}{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)} \\ \frac{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)}{1} & \frac{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)}{c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*)} \end{array} \right).\)

我们可以推断，给定 \(\mathbf{t}\) 时 \(t_*\) 的条件概率服从正态分布，其方差和均值为

\(\sigma^2(\mathbf{x}_*) = c(\mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*) = \sigma^2 + k(\mathbf{x}_*, \mathbf{x}_*) - k(\mathbf{x}_*)^T C^{-1} k(\mathbf{x}_*),\)
\(m(\mathbf{x}_*) = k(\mathbf{x}_*)^T C^{-1} \mathbf{t}.\)
(8.11)

由于 \(\mathbf{x}_*\) 是任意选择的（\(\mathbf{x}_1, \dots, \mathbf{x}_N\) 除外），这指定了一个函数上的分布。

设 \(\mathbf{x}_1^*, \dots, \mathbf{x}_{N^*}^*\) 为要进行预测 \(\mathbf{t}^* = (t_1^*, \dots, t_{N^*}^*)^T\) 的 \(N^*\) 个点。\((\mathbf{t}, \mathbf{t}^*)\) 的联合分布的协方差矩阵为

\(\left( \begin{array}{cc} \mathbf{C} & \mathbf{K} \\ \mathbf{K}^T & \mathbf{C}^* \end{array} \right),\)

其中 \(\mathbf{C}\) 与之前相同，\(\mathbf{K}\) 是一个由 \(k(\mathbf{x}_n, \mathbf{x}_m^*)\) 给出的 \(N \times N^*\) 矩阵，\(\mathbf{C}^*\) 的 \((i, j)\) 项为 \(k(\mathbf{x}_i^*, \mathbf{x}_j^*) + \sigma^2 \delta_{ij}\)。给定 \(\mathbf{t}\) 时 \(\mathbf{t}^*\) 的条件概率分布的均值和方差为

\(\mathbf{m}^* = \mathbf{K}^T \mathbf{C}^{-1} \mathbf{t},\)
\(\mathbf{\Sigma}^* = \mathbf{C}^* - \mathbf{K}^T \mathbf{C}^{-1} \mathbf{K}.\)

与之前一样，我们可以从此分布中抽取点值并将其作为函数绘制，以说明后验高斯过程的样本。图 8.13 说明了使用各种核的四个样本，以及来自函数 \(1 + x + \sin x\) 的四个训练数据点，该函数以红色绘制。条件分布的均值以蓝色绘制，并伴有两个标准差的灰色带。参数保持为 \(\theta_1 = \theta_2 = 1\)。噪声方差设置为 0.00001。分布在训练数据附近变得收紧，而在远离训练数据点时不确定性增加。在两个训练点之间的范围内，不确定性在中间最大。如右侧所示，远离训练数据时，分布变为高斯过程的先验分布（例如高斯核的图 8.12d），并添加了噪声，因为 \(\mathbf{K}\) 的项趋近于零，因为高斯核随点间距离的增加而减小。

将 (8.11) 与 (8.10) 进行比较，我们发现当核被选择为 \(k(\mathbf{x}, \mathbf{y}) = \mathbf{d}(\mathbf{x})^T \mathbf{A}^{-1} \mathbf{d}(\mathbf{y})\) 时，结果一致。然而，在上一节中，\(\mathbf{A}\) 的项是通过最大化对数证据确定的。同样，

![](img/d3c00252180686426c9e63ab889b535b_279_0.png)

(a) 高斯核，\(\theta_1 = \theta_2 = 1\)

![](img/d3c00252180686426c9e63ab889b535b_279_1.png)

(b) 指数核，\(\theta_1 = \theta_2 = 1\)

![](img/d3c00252180686426c9e63ab889b535b_279_2.png)

(c) 反多二次核，\(\theta_1 = \theta_2 = 1\)

图 8.13：不同核的后验高斯过程样本。

\(\theta_1\) 和 \(\theta_2\) 可以通过最大化训练数据的对数似然来选择，其由以下公式给出

\(\mathcal{L} = -\frac{1}{2} \left[ \log |\mathbf{C}| + \mathbf{t}^T \mathbf{C}^{-1} \mathbf{t} + N \log(2\pi) \right].\)

使用附录 A.2.4 和 A.2.7 中关于矩阵行列式和逆导数的公式，当矩阵的项依赖于一个变量时，我们得到

\(\frac{\partial}{\partial \theta_i} \mathcal{L} = -\frac{1}{2} \left[ \text{tr} \left( \mathbf{C}^{-1} \frac{\partial \mathbf{C}}{\partial \theta_i} \right) - \mathbf{t}^T \mathbf{C}^{-1} \frac{\partial \mathbf{C}}{\partial \theta_i} \mathbf{C}^{-1} \mathbf{t} \right].\)

\(\mathbf{C}\) 对 \(\theta_i\) 的导数的 \((m,n)\) 项为

\(\frac{\partial}{\partial \theta_i} (k(\mathbf{x}_m, \mathbf{x}_n) + \sigma^2 \delta_{mn}) = \frac{\partial}{\partial \theta_i} k(\mathbf{x}_m, \mathbf{x}_n).\)

![](img/d3c00252180686426c9e63ab889b535b_280_0.png)

(a) 高斯核，\(\theta_1 \approx 2.81, \theta_2 \approx 2.85\)

![](img/d3c00252180686426c9e63ab889b535b_280_1.png)

(b) 指数核，\(\theta_1 \approx 1.75, \theta_2 \approx 1.66\)

![](img/d3c00252180686426c9e63ab889b535b_280_2.png)

(c) 反多二次核，\(\theta_1 \approx 3.21, \theta_2 \approx 4.74\)

图 8.14：不同核的后验高斯过程样本。

因此，需要核关于其参数的导数。对于高斯核

```
\(k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right),\)
```

```
\(\frac{\partial}{\partial \theta_1} k(\mathbf{x}, \mathbf{y}) = 2\theta_1 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{2}{\theta_1} k(\mathbf{x}, \mathbf{y}),\)
\(\frac{\partial}{\partial \theta_2} k(\mathbf{x}, \mathbf{y}) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} \theta_1^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_2^2} \right) = \frac{\|\mathbf{x} - \mathbf{y}\|^2}{\theta_2^3} k(\mathbf{x}, \mathbf{y}).\)
```

将 \(\mathcal{L}\) 的梯度设为零并求解参数通常并不直接。然而，由于梯度已知，可以用它来迭代逼近最大值（参见例如 [2]）。

![](img/d3c00252180686426c9e63ab889b535b_281_0.png)

图 8.15：优化参数的线性核与高斯核之和。

图 8.14 显示了各种核的后验高斯过程的均值和两个标准差，其中参数已优化，以及四个样本。当使用高斯核时，数据点附近的拟合非常出色。反多二次核也表现良好，而指数核似乎不合适。

后验高斯过程的均值由于核的选择而在远离数据点时返回到零，尽管它比使用原始参数选择时更慢。因此，我们将高斯核与线性核结合。也就是说，核由以下公式给出

```
k(\mathbf{x}, \mathbf{y}) = \theta_1^2 + \theta_2^2 \mathbf{x}^T \mathbf{y} + \theta_3^2 \exp \left( - \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\theta_4^2} \right).
```

优化后，参数约为 \(\theta_1 \approx 10^{-5}, \theta_2 \approx 0.90, \theta_3 \approx 1.13\) 和 \(\theta_4 \approx 1.65\)。近似优劣在图 8.15 中在更宽的范围内得到说明。虽然均值偏离了真实函数，但一般趋势被保留。通过更多数据可以获得更好的近似。应使用哪种核的组合取决于应用，并且是活跃的研究领域，正在为特定用途开发新的核。

![](img/d3c00252180686426c9e63ab889b535b_282_0.png)

泰勒与弗朗西斯

泰勒与弗朗西斯集团

http://taylorandfrancis.com

## 特征学习

本章专注于推导构建充分数据模型所必需的构建模块。神经网络被重新审视，并解释了其众多变体，特别是激活（传播函数）和误差函数等设计选择如何取决于手头的任务。误差反向传播被普遍推导为对不同误差函数求导时链式法则的应用。自编码器被引入为非常简单的网络架构，并通过一个广泛的示例进行说明，展示神经网络如何为数据创建模型空间。探索了与其他技术的关系，以直观理解工作中的机制。本章以对模型空间推导的贝叶斯处理结束，并以印度自助过程为例进行说明。

在上一章中，模型空间的选择在很大程度上仍由用户决定，用户选择要使用的基函数或核。数据可以为这些选择提供信息或优化基函数或核的参数。如果基函数是以数据为中心的核，数据也以这种方式具有影响。然而，形状仍在很大程度上取决于用户选择。

在本章中，我们探讨数据决定模型空间的可能性。为此，需要许多来自同一过程生成的数据示例。例如，[26] 的 MNIST 数据集，其中生成过程是人们书写数字，包含 60,000 个手写数字图像，尺寸为 28 x 28 像素。目标是一种技术，它生成一个模型空间，其中如果重建是目标，则所有样本都得到同样好的表示，或者如果分类是目标，则被分离。

一个缺点是，只有在看到足够可靠的数据时才有可能实现。虽然可以有一些样本，其中某些特征未给出或给出了非可忽略的误差，但需要有足够多的样本，其中这些特征具有可靠的值。这被称为 _可信度_，是大数据四个 _V_ 之一。其他三个是 _体量_、_速度_ 和 _多样性_。

