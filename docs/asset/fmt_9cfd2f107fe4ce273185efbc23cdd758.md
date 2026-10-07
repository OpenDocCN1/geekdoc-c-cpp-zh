
图 7.2 – 以水平集形式表示的曲线 `$\gamma$`：`$\gamma = \psi^{-1}(0)$`。在这个例中，轮廓是一个圆，因此函数 `$\psi$` 是一个圆锥。

其中 `$d(\bullet)$` 是欧几里得距离，`$\mathbf{m}$` 是 `$\Omega \subset \mathbb{R}^2$` 中的一个点。

这种形式化的有趣之处在于，轮廓 `$\gamma$` 上每点的法向量 `$\mathbf{n}$` 及其曲率 `$\kappa$` 都可以通过施于隐式映射 `$\psi$` 的微分算子轻松计算：

$$\mathbf{n} = \frac{\nabla \psi}{\|\nabla \psi\|} \text{ 和 } \kappa = \nabla \cdot \frac{\nabla \psi}{\|\nabla \psi\|}$$

其中 `$\nabla$` 是空间梯度，即相对于 `$\mathbf{m}$` 的梯度。

为了初始化 `$\psi$` 函数，我们通常使用带符号距离计算算法（例如 [37] 中的快速行进算法）。在初始曲线 `$\gamma_0$` 具有简单形式的情况下，可以可以 `$\psi$` 的解析形式。这就是我们在代码 7.2 中做的，其中初始曲线是一个圆，`$\psi$` 的值对应于到圆的距离。

## 7.1 基于边缘的方法

```
Code 7.2 - 圆特殊情况下的函数 ψ 初始化。
```

```cpp
/*
InitLevelSet: 使用带符号欧几里得距离初始化水平集 (psi)。
初始轮廓是一个中心位于 (x0,y0) 半径为 r 的圆。

imgIn : 需要初始化的水平集函数
x0,y0,r : 用于初始化的圆参数
*/
void InitLevelSet(CImg<>& imgIn, int x0, int y0, int r) {
    cmig_forXY(imgIn,x,y)
    imgIn(x,y) = std::sqrt(sqr(x - x0) + cmig::sqr(y - y0))
}
```

### 7.1.3 演化方程

在 [37] 中已经证明 `$\gamma(t)$` 根据演化方程 `$\partial/\partial t = F \cdot n$` 演化，那么其隐式表示（即 `$\psi$` 函数）根据方程演化：

$$\partial\psi/\partial t = F\|\nabla\psi(m,t)\|  (7.2)$$

其中 `$F$` 是速度场 `$F = F \cdot n$` 的法分量。这仅在 `$\|\psi(m,t)\| = 1$` 属性随时间保持时（Eikonal 方程）成立。对函数 `$\psi$` 求解演化问题，因为可以从 `$\psi(t)$` 的演化推导出 `$\gamma(t)$` 的演化。通过这种由 `$\psi$` 对 `$\gamma$` 的隐式表示，请注意在模型的传播中仅使用了垂直于轮廓的 `$t$` 法分量。在后续，我们将引用速度场或点的速度值。

为了提取目标区域 `$R$`，需要从各种来源构建一个速度场 `$F$`。例如，在水平集公式中，Caselles 等人的测地模型提出了方程：

$$\partial\psi/\partial t = f(m)\|\nabla\psi(m,t)\kappa+\nabla f(m)\cdot\psi(m,t).$$

注意 `$F$` 的演化速率，隐式表示 `$\psi$` 在演化过程中保持其 `$\|\psi(m)\| = 1$` 的属性，使得 `$\psi$` 的演化与它表示的 `$\gamma$` 曲线之间的等效性（方程 7.2）保持有效。在实践中，每隔一段时间执行梯度归一化。这种归一化在算法上并不简单，我们不会讨论其实现的理论细节。

### 7.1.4 演化方程的离散化

该方法的核心是由速度函数 `$F$` 引导的迭代方案，必须定义停止准则。通过对区域 `$m \rightarrow (i, j)$` 和时间 `$t \rightarrow n$` 进行离散化，数值求解传播问题。点 `$m$` 在时刻 `$t$` 处的 `$\psi$` 值和速度 `$F$` 分别记为 `$\psi_{ij}^t$` 和 `$F_{ij}^t$`。函数 `$\psi$` 由带符号距离初始化。使用有限差分法，演化方程变为：

```cpp
$$\psi_{ij}^{t+1} = \psi_{ij}^t + \Delta t F_{ij}^t |\nabla \psi_{ij}^t|$$
```

## 第 7 章 分割

// 测地模型的函数。

```cpp
CImg<> f(imgIn.width(), imgIn.height());
cimg_forXY(f, x, y)
{
    float gx = GradImg(0, x), gy = GradImg(1, y);
    f(x, y) = exp_cost*(1/(1 + std::sqrt(gx*gx + gy*gy)) + ballon);
}
```

// f 的梯度计算。

```cpp
CImgList<> Grad_f = f.get_gradient();
```

// 传播算法的迭代方案。

```cpp
for (int iter = 0; iter < nbiter; ++iter)
```

// psi 的空间梯度。

```cpp
CImgList<>
GradLS_moins = LevelSet.get_gradient("xy",-1);
GradLS_plus = LevelSet.get_gradient("xy",1);
```

```cpp
cimg_forXY(LevelSet, x, y);
```

```cpp
float
Dxm = GradLS_moins(0, x, y), Dpx = GradLS_plus(0, x, y);
Dym = GradLS_moins(1, x, y), Dyp = GradLS_plus(1, x, y);
```

// 场的传播方案：

```cpp
float Nabla_plus = std::sqrt(cimg::std::max(Dxm, 0)) + 
cimg::std::sqrt(std::min(Dpx, 0)) + 
cimg::std::sqrt(std::max(Dym, 0)) + 
cimg::std::sqrt(std::min(Dyp, 0));
```

```cpp
Nabla_moins = std::sqrt(cimg::std::min(Dxm, 0)) + 
cimg::std::sqrt(std::max(Dpx, 0)) + 
cimg::std::sqrt(std::max(Dym, 0)) + 
cimg::std::sqrt(std::min(Dyp, 0));
```

```cpp
Fprop = -(std::max(f(x, y), 0)*Nabla_plus + std::min(x, y) + 
*Nabla_moins)
```

// 场的平流速度：

```cpp
float
u = Grad_f(0, x, y),
v = Grad_f(1, x, y);
Fadv = -(std::max(u, 0)*Dxm + std::min(u, 0)*Dpx + 
std::max(v, 0)*Dym + std::min(v, 0)*Dyp);
```

// 水集函数的更新。

```cpp
LevelSet(x, y) += delta_t*(alpha*Fprop + beta*Fadv);
```

## 7.2 基于区域的方法

```cpp
}
if (!(iter%20)) ResultSet.distance_eikonal(10,3);
}
```

图 7.1 展示了该算法的结果。

### 7.2.1 引言

在基于区域的方法中，具有同质特征的像素被分配到同一个区域，或通常分配到同一类。在图 7.3 的示例中，原始图像（图 7.3a）由两种纹理组成。通过使用梯度范数作为像素的特征（图 7.3b），我们获得了无法用于正确分割图像（即分离出两种纹理）的信息。相反，通过使用图像的局部方差，分割变得可能了（图 7.3c）。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_179_0.png)

图 7.3 – 基于区域的方法（合成案例）。(a) 原始图像，(b) 使用梯度，(c) 使用局部方差。

特征是一个概念（通常是向量 `$x_i \in \mathbb{R}^d$`），我们将其附加到图像的每个像素 `$i$` 上。特征的计算包括描述像素相对于强度（第 3 章）、梯度（第 5.1 节）、几何类型属性（第 6.1 节）、纹理（第 6.3 节）或取决于位置的任何值。在向量中，多种类型的特征可以共存。

### 7.2.2 基于直方图的方法

这些方法虽然实现简单，但通常性能较低，因为它们没有考虑到图像数据背后的空间信息。尽管如此，当图像对比度很高，或者分割的是一组代表同一场景但通过多个通道（例如雷达）或多种模态（例如医学成像）测量的图像时，它们仍然是有用的。其核心思想是寻找直方图的不同模式，这些模态代表了图像中尽可能多的对象类别。

如果对我们正在寻找的类别某些信息（特别是每个类别灰度出现的概率，以及类别的先验概率），则可以使用贝叶斯决策理论，并选择最小化错误代价的阈值（例如贝叶斯阈值化、内叶-皮尔森法）。如果没有，我们通过分析直方图来寻找多个区域或类别情况下的阈值：

- 直接阈值化：阈值自动从灰度直方图的统计计算中得出（众数、零交叉、最大熵、方差最大、动量守恒等）；

- 自适应阈值化：使用上述计算技术，关注准则的局部研究，即子区域（管理区域的大小、重叠）；

- 滞后阈值化：交互式或自动定义四个阈值，确定三类像素：拒绝像素（`$s_1-s_2$`）、接受像素（`$s_3-s_4$`）和候选像素（`$s_2-s_3$`）。对 (`$s_2-s_3$`) 和 (`$s_3-s_4$`) 进行凸性测试可以验证或失效候选像素（`$s_3-s_4$`）。也可以通过测地重建控制 (`$s_2-s_3$`) 的扩展。

#### OTSU 算法

`Otsu` 算法假设大小为 `$nx \times ny$` 的图像 `$I$` 由两个类组成，其分布未知。目标是找到一个阈值 `$s$`，使得两个类的分离得最好，即：

1. 它们的均值越远越；

2. 分布越紧凑越好（方差最小）。

设 `$M$` 为 `$I$` 中的最大灰。给定 `$s$`，图像划分为两个数量类 `$R_0$` 和 `$R_1$`：

```cpp
n0(s) = \sum_{g=0}^{s} h(g) \quad n1(s) = \sum_{g=s+1}^{M-1} h(g)
```

其中 `$h$` 是 `$I$` 的直方图。两个类的均值值为：

```cpp
mu_0(s) = \frac{1}{n0(s)} \sum_{g=0}^{s} gh(g) \quad \mu_1(s) = \frac{1}{n1(s)} \sum_{g=s+1}^{M-1} gh(g)
```

`$\sigma_0^2(s) = \frac{1}{n0(s)} \sum_{g=0}^{s} (g - \mu_0(s))^2 h(g); \quad \sigma_1^2(s) = \frac{1}{n1(s)} \sum_{g=s+1}^{M-1} (g - \mu_1(s))^2 h(g)$`。

类内方差和为：

$$\sigma_w^2(s) = P_0(s)\sigma_0^2(s) + P_1(s)\sigma_1^2(s) = \frac{n_0(s)\sigma_0^2(s) + n_1(s)\sigma_1^2(s)}{nx \times ny}$$

其中 `$P_0(s) = \frac{1}{nx \times ny} \sum_{g=0}^{s} h(g)$`  `$P_1(s) = \frac{1}{nx \times ny} \sum_{g=s+1}^{M-1} h(g)$`。

同样，类间方差计算为：

$$\sigma_b^2(s) = P_0(s)(\mu_0(s) - \mu_f)^2 + P_1(s)(\mu_1(s) - \mu_f)^2$$

其中 `$\mu_f = \frac{1}{nx \times ny}(n_0(s)\mu_0(s) + n_1(s)\mu_1(s))$` 是 `$I$` 的灰度均值。

`$I$` 的总方差是 `$\sigma_b^2(s)$` 和 `$\sigma_w^2(s)$` 之和。由于对于 `$I$` 它是常数，因此阈值 `$s$`可以通过最大化 `$\sigma_b^2(s)$` 或最小化 `$\sigma_w^2(s)$` 来找到。使用后者是因为它取决于统计数据。代码 7 实现了 `Otsu` 算法，图 7.4 显示了一些结果。

#### 代码 7.4 – Otsu 阈值化

```cpp
/*
Otsu 算法
imgIn : 输入图像
nb_levels : 箱的数量
*/
float Otsu(CImg& imgIn, int nb_levels)
{
float sigmaMax = 0;
long n0 = 0, n1;
int th = -1;
CImg<> hist = imgIn.get_histogram(nb_levels);
cimg_forX(hist, i)
{
  if (i < nb_levels - 1)
    // 如果 i==nb_levels - 1, 所有像素属于类 0。
    {
      n0 += hist[i];
      n1 = imgIn.size() - n0;

      float mu0 = 0, mul = 0;
      for (int j = 0; j <= i; j++) mu0 += j*hist[j];
      for (int j = i + 1; j < nb_levels; j++) mul += j*hist[j];
      mu0 /= n0;
      mul /= n1;

      if (n0 * n1 > 0)
        {
          float sigmaB = n0 * n1 * cimg::sqr(mu0 - mul) / cimg::sqr(imgIn.size());
          if (sigmaB > sigmaMax)
            {
              sigmaMax = sigmaB;
              th = i;
            }
        }
    }
}
return (float)th;
}
```

![](img/6b7de6c7ce31f7bb2927e7184da0492f_182_0.png) 原始图像

![](img/6b7de6c7ce31f7bb2927e7184da0492f_182_1.png) 阈值化图像

图 7.4 – Otsu 算法的使用。

#### BERNSEN 自适应阈值化

`Bernsen` 算法 [4] 根据每个像素 `(x,y)` 邻域 `$\mathcal{Y}(x,y)$` 内的最小和最大强度计算阈值。如果：

```cpp
I_{min}(x,y) = \min_{(i,j) \in \mathcal{Y}(x,y)} I(i,j)
I_{max}(x,y) = \max_{(i,j) \in \mathcal{Y}(x,y)} I(i,j)
```

阈值简单定义为均值 `$s(x,y) = (I_{max}(x,y) + I_{min}(x,y))/2$`，只要 `$c(x,y) = I_{max}(x,y) - I_{min}(x,y)$` 大于限制 `$c_{min}$`。否则，邻域内的所有像素都属于同一个区域。代码 7.5 利用 `CImg` 的邻域结构非常高效地实现了这种算法。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_183_0.png)

```cpp
/*
Bernsen 算法。

imgIn : 输入图像
cmin : 对比度的下限
*/
CImg<> Bernsen(CImg<> imgIn, float cmin)
{
  CImg<> imgOut(imgIn.width(),imgIn.height(),1,1,0);
  float valClass = 0;

  CImg<> N(5,5);
  cimg_forx5(imgIn,x,y,0,0,N,float)
  {
    float min, max = N.max_min(min);
    imgOut(x,y) = max - min>cmin ? (max + min) / 2 : valClass;
  }
  return imgOut;
}
```

图 7.5 展示了一个结果示例。

### 7.2.3 通过聚类分割

将特征视为 `$\mathbb{R}^d$` 中的点，可以使用无监督分类算法（也称为聚类算法）在该空间中寻找 `$I$` 的区域：属于 `$\mathbb{R}^d$` 中同一类的向量定义了属于 `$I$` 中同一区域的像素。在所有无监督分类算法中（参见示例 [3]），我们建议使用函数最小化方法。

# 第 7 章 分割

![](img/6b7de6c7ce31f7bb2927e7184da0492f_184_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_184_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_184_2.png)

图 7.5 – Bernesen 自适应阈值分割。

从形式上说，目标是根据图像 `$n$` 个像素的特征集 `$X = \{\mathbf{x}_i, i \in [[1, n]]\,, \mathbf{x}_i \in \mathbb{R}^d\}$` 计算一个划分，即 `$X$` 的一组 `$g$` 个非空子集 `$P = (P_1, P_2, \dots, P_g)$`，使得：

- 1. `($\forall k \neq 1$) $P_k \cap P_1 = \emptyset$`

- 2. `$\bigcup_{i=1}^g P_i = X$`

使用函数最小化的聚类方法在参数化的划分集合上定义一个代价函数，并通过优化该代价来找到“最佳”的划分。很多情况下，目标函数需要预先确定所需的类别数 `$g$`。
