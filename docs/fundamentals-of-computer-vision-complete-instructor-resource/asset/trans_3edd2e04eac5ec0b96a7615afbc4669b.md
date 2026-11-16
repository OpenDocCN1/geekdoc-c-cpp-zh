

将等式 10.21 代入等式 10.19，我们得到

```
\(\epsilon(m) = \sum_{i=m+1}^d E\{(y_i - E\{y_i\})^2\}.\)
```

将等式 10.11 代入等式 10.22：

```
\(\epsilon(m) = \sum_{i=m+1}^d E\{(\mathbf{b}_i^T \mathbf{x} - E\{\mathbf{b}_i^T \mathbf{x}\})^2\}\)
```

```
\(= \sum_{i=m+1}^d E\{(\mathbf{b}_i^T \mathbf{x} - E\{\mathbf{b}_i^T \mathbf{x}\})(\mathbf{b}_i^T \mathbf{x} - E\{\mathbf{b}_i^T \mathbf{x}\})\}\)
```

```
\(= \sum_i \mathbf{b}_i^T \{E(\mathbf{x} - E(\mathbf{x}))(\mathbf{x}^T - E\{\mathbf{x}^T\})\mathbf{b}_i\}\)
```

```
\(= \sum_i \mathbf{b}_i^T \{E(\mathbf{x} - E(\mathbf{x}))(\mathbf{x} - E(\mathbf{x}))^T\}\mathbf{b}_i\)
```

现在我们认识到等式 10.26 中 b 之间的项是 x 的协方差：

```
\(\epsilon(m) = \sum_{i=m+1}^d \mathbf{b}_i^T K_x \mathbf{b}_i.\)
```

我们可以对等式 10.27 求导，将结果设为零，并试图找到向量 \(\mathbf{b}_i\)，但这行不通，因为使函数最小化的 \(\mathbf{b}\) 是零向量。我们必须利用它们是单位向量这一事实。也就是说，对于每个 \(i\)，\(\mathbf{b}_i^T \mathbf{b}_i = 1\)。我们通过使用拉格朗日乘数将其作为约束条件。

回顾，目标函数可以通过添加一个等于零的项（乘以标量拉格朗日乘数）在约束条件下得到最小化。对于我们的问题，目标函数变为

```
\(\sum_i [\mathbf{b}_i^T K_x \mathbf{b}_i - \lambda_i (\mathbf{b}_i^T \mathbf{b}_i - 1)].\)
```

为了避免与求和索引混淆，对某个任意 \(\mathbf{b}\)（例如 \(\mathbf{b}_k\)）求导。这样做，人们会发现，对 \(i\) 求和中仅涉及 \(k\) 的项才是非零的，因此求和消失，我们得到

```
\(\nabla_{\mathbf{b}_k} \epsilon = 2K_x \mathbf{b}_k - 2\lambda_k \mathbf{b}_k.\)
```

整理后，这变为

```
\(K_x \mathbf{b}_k = \lambda_k \mathbf{b}_k.\)
```

也就是说，最优基向量是 \(K_x\) 的特征向量。

y 的协方差可以通过以下方式轻松与 \(K_x\) 相关联：

```
\(K_y = E\{(\mathbf{y} - E\{\mathbf{y}\})(\mathbf{y} - E\{\mathbf{y}\})^T\} = B^T K_x B\)
```

其中矩阵 \(B\) 的列由基向量 \((\mathbf{b}_1, \mathbf{b}_2, \dots, \mathbf{b}_d)\) 组成。

此外，如果 \( B \) 的列是 \( K_x \) 的特征向量，那么 \( B \) 将是对角化 \( K_x \) 的变换，从而得到

\( K_y = \begin{bmatrix} \lambda_1 & 0 & \dots & 0 \\ 0 & \lambda_2 & \dots & 0 \\ \dots & \dots & \dots & \dots \\ 0 & 0 & \dots & \lambda_d \end{bmatrix} . \) (10.32)

将等式 10.32 代入等式 10.27，我们得到

\( \epsilon(m) = \sum_{i=m+1}^d \mathbf{b}_i^T \lambda_i \mathbf{b}_i . \) (10.33)

由于 \( \lambda_i \) 是标量，

\( \epsilon(m) = \sum_{i=m+1}^d \lambda_i \mathbf{b}_i^T \mathbf{b}_i . \) (10.34)

并且，再次记着 \(\mathbf{b}_i\) 的标准正交条件，

\( \epsilon(m) = \sum_{i=m+1}^d \lambda_i . \) (10.35)

因此，我们用一个 \( m \) 维向量 \(\mathbf{y}\) 来表示一个 \( d \) 维测量 \(\mathbf{x}\)，其中 \( m < d \)，

\( y_i = \mathbf{b}_i^T \mathbf{x} , \) (10.36)

并且 \(\mathbf{b}_i\) 是 \(\mathbf{x}\) 协方差的特征向量。将随机向量用协方差矩阵的特征向量展开，称为卡胡宁-洛ève展开，或“K-L 展开”。

## 10.3.2 K-L 展开的性质

不失一般性，特征向量 \(\mathbf{b}_i\) 可以按其对应的特征值排序。也就是说，为特征向量分配下标，使得

\( \lambda_1 > \lambda_2 > \dots > \lambda_d . \) (10.37)

然后，我们将对应于 \(\lambda_1\) 的 \(\mathbf{b}_1\) 称为“主要特征向量”。

考虑二维高斯：

\( G(x, y) = \frac{1}{2\pi|K|} \exp \left( - \frac{\begin{bmatrix} x & y \end{bmatrix} K^{-1} \begin{bmatrix} x \\ y \end{bmatrix}}{2} \right) , \) (10.38)

并考虑该高斯的 \( C \) 层集，\( G(x, y) = C \)。

![](img/5f95dd954ac63cc68119f6f48ca99e18_243_0.png)

现在，我们对两边取对数，得到

```
\ln C = \ln \left( \frac{1}{2\pi |K|} \right) - \frac{[x \ y] K^{-1} \begin{bmatrix} x \\ y \end{bmatrix}}{2}. \quad (10.39)
```

由于 \(|K|\) 是标量常数，我们将所有常数合并为一个新常数 \(C' = \ln C - \ln(\frac{1}{2\pi |K|})\)，并得到

```
$C' = [x \ y] K^{-1} \begin{bmatrix} x \\ y \end{bmatrix}. \quad (10.40)$
```

现在，使用 $K^{-1} = \begin{bmatrix} k_{11} & k_{12} \\ k_{21} & k_{22} \end{bmatrix}$ 展开逆协方差矩阵，我们得到

```
$C' = k_{11}x^2 + 2k_{12}xy + k_{22}y^2. \quad (10.41)$
```

为了证明等式 10.41 表示椭圆而不是其他二阶函数，我们必须更仔细地检查协方差矩阵。我们对 $K^{-1} = E \Lambda E^T$ 进行特征值分解。在此分解中，$\Lambda$ 是对角矩阵，特征值在对角线上。如果特征值均为正，则这表示椭圆。由于协方差矩阵总是有正特征值，因此等式 10.41 表示椭圆。

在更高维度中，相同的论证得出结论：高斯的层集将是椭球体或超椭球体。

如果我们将点 x 的分布视为由超椭球体表示，那么该椭球体的主轴将穿过数据的重心，并沿着 $K_x$ 最大特征值对应的特征向量方向。如图 10.5 所示。因此，K-L 变换将椭圆拟合到二维数据，将椭球体拟合到三维数据，并将超椭球体拟合到更高维数据。

## 用于直线拟合

考虑随机向量 x 的一组实例，\(\{x\}_i, i = 1, \dots, m\)。我们希望找到最能拟合这组数据的直线。将原点移动到该组数据的重心。然后，用其单位法向量 \(\mathbf{n}\) 来表征（目前未知的）最佳拟合直线。然后，对于每个点 \(x_i\)，\(x_i\) 到最佳拟合直线的垂直距离将等于该点在 \(\mathbf{n}\) 上的投影，如图 10.6 所示。将此

![](img/5f95dd954ac63cc68119f6f48ca99e18_244_0.png)

距离表示为 \(d_l(\mathbf{n})\)：

```
d_l(\mathbf{n}) = \mathbf{n}^T \mathbf{x}_l. \quad (10.42)
```

为了找到最佳拟合直线，最小化垂直距离平方和，

```
\epsilon = \sum_{l=1}^m d_l^2(\mathbf{n}) = \sum_{l=1}^m (\mathbf{n}^T \mathbf{x}_l)^2 = \sum_{l=1}^m (\mathbf{n}^T \mathbf{x}_l)(\mathbf{x}_l^T \mathbf{n}) = \mathbf{n}^T \left( \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T \right) \mathbf{n} \quad (10.43)
```

受限于 \(\mathbf{n}\) 是单位向量的约束条件，

```
\mathbf{n}^T \mathbf{n} = 1. \quad (10.44)
```

使用拉格朗日乘数进行约束最小化需要最小化

```
\mathbf{n}^T \left( \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T \right) \mathbf{n} - \lambda (\mathbf{n}^T \mathbf{n} - 1). \quad (10.45)
```

定义 \(S = \sum_{l=1}^m \mathbf{x}_l \mathbf{x}_l^T\)，按如下方式求导：

```
\frac{\partial \epsilon}{\partial \mathbf{n}} \left( \mathbf{n}^T S \mathbf{n} - \lambda (\mathbf{n}^T \mathbf{n} - 1) \right). \quad (10.46)
```

对二次型 \(\mathbf{n}^T S \mathbf{n}\) 求导，得到 \(2S\mathbf{n}\)，将导数设为零得到

```
2S\mathbf{n} - 2\lambda \mathbf{n} = 0 \quad (10.47)
```

这与前面提到的相同的特征值问题。因此我们可以断言：最佳拟合直线穿过数据点的均值，并沿着该组数据协方差的主要特征向量方向。

我们现在已经看到了两种不同的方法来找到最能拟合数据的直线：第 5.4.2 节中描述的最小二乘法，如果应用于拟合直线而不是平面，则最小化数据点到直线的垂直距离。本节中描述的方法最小化等式 10.43 所述的垂直距离。该

