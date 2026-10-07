
因此，多光谱图像是一个 3D 数组（体积图像为 4D），大小为 `$w \times h \times p$`，其中 `$(w,h)$` 是图像的大小，`$p$` 是采集通道的数量。

这对于分析可能很有意义：

- 将数据以匹配将使用的算法；
- 降低这些算法的时间复杂度；
- 降低问题的空间复杂度；
- 解除变量并寻找依赖关系；
- 为算法引入先验或重要的属性（归一化数据、稀疏特征…………）；
- 允许以精简的方式进行更直观的/或图形化的解释，图像形式为 `$w \times h \times k, kp$`（通常 `$k=2$` 或 3），或直接在屏幕上可视化这些信息。

经典上使用两种方法：从初始特征（在通道中测量的 `$p$` 个值）中选择被认为最相关的并消除其他的（这被称为**变量选择**）；或者从这些定量值通过线性或非变换构造新特征（这被称为**特征提取**）。

在这种背景下，降维方法经常被应用 [25]。我们在接下来的简单示例中，提出了多光谱成像中的线性降维方法及其在 `ClImg` 中的实现。

# 第 9 章 多光谱方法

## 9.1 降维方法

### 9.1.1 主成分分析

因子法旨在处理和可视化多维数据。同时考虑所有变量是一个困难的问题，但有时由于变量提供的信息存在冗余，该问题会变得更容易。因子方法的目标是利用这种冗余性，尝试用较少的新变量来替换初始变量，尽可能保留初始信息。

对于定量数据，*主成分分析*（PCA）[19] 是使用最广泛的方法之一。它认为新变量是初始变量的线性组合且互不相关的变量。

在接下来，数据将是定量变量数组 `$\mathcal{M}_{np}(\mathbb{R})$`，表示图像的一行像素，列描述该像素上测量的参数（通道）。

#### 原理

PCA 经常对中心化和/或标准化的变量处理。令 `$\mathbf{g} \in \mathbb{R}^p$` 为每个通道的算术平均值向量：

```
$$\mathbf{g} = \mathbf{X}^T\mathbf{D}1$$
```

**D** 是一个对角矩阵，每个 `$d_{ii}$` 给出个体 `$i$` 在数据中的重要性（通常 **D = $\frac{1}{n}$I**，我们将在后续假设如此），**I** 是 `$\mathbb{R}^n$` 的向量，其分量全部等于 1。矩阵 `$\mathbf{X}^T\mathbf{D}\mathbf{X}$` 是协方差矩阵。

目标是找到该矩阵的特征向量和特征值。特征向量为主成分，特征值是每个成分解释的方差量。

令 `$\mathbf{v}_1, \mathbf{v}_2, \dots, \mathbf{v}_p$` 为特征向量，`$\lambda_1 \ge \lambda_2 \ge \dots \ge \lambda_p \ge 0$` 为对应的特征值。

前 `$k$` 个特征向量定义了一个维度为 `$k$` 的子空间，该空间捕获了数据中最大的方差。数据到该子空间的投影给出：

$$\mathbf{Y} = \mathbf{X}\mathbf{V}_k$$

其中 `$\mathbf{V}_k$` 是以前 `$k$` 个特征向量为列的矩阵。

## 9.2 颜色成像

- 如果我们处理标准化的中心数据，我们保留对应值大于 1 的 PC（Kaiser 准则）。

第一个准则例如所示：

```cpp
float s = 0.9*val.sum(), inertia = val[0];
int nb_pca = 1;
while (inertia<s)
    inertia += val[nb_pca++];
```

### 9.1.2 示例

为了说明，我们提议处理来自太阳动力天文台（Solar Dynamics Observatory）¹ [33] 的太阳图像，其主要目标是理解和预测影响地球生命和技术系统的太阳变异。该任务包括三项科学调查（大气成像组件 (AIA)、极紫外线变异实验 (EVE) 和日震波磁力成像仪 (HMI)），提供了不同波长下的 `$p=19$` 图像（图 9.1）。

应用该方法，三个分量捕获了数据初始变化的 90% 以上。该代码：

```cpp
CImgList< imgOut(nb_pca,256,256);
cimg_forXYC(imgIn,x,y,c)
if (c<nb_pca) imgOut(c,x,y) = Xpca(c,x+y*imgIn.width());
imgOut.display();
```

允许显示相应的 PC（图 9.2）。

彩色图像是我们日常生活中不可或缺的一部分。不意外的是，它们代表了人们对数字图像处理感兴趣时最常遇到的多光谱图像。彩色图像的处理通常可以分通道进行，同时转换回标量处理，如之前章节中描述的那样。但通过推广灰度技术来开发专门的处理方法可能很有趣。作为说明，我们提议研究用于彩色成像的经典算法变体：中值滤波和边缘检测算法。作为介绍，我们通过 `ClImg` 库介绍了现有的主要颜色空间。[23] 中对颜色成像方面提出了更广泛的概述。

> ¹https://sdo.gsfc.nasa.gov/

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_0.png)

171 Å

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_1.png)

193 Å

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_2.png)

211 Å

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_3.png)

304 Å

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_4.png)

1600 Å

![](img/6b7de6c7ce31f7bb2927e7184da0492f_230_5.png)

HMI

图 9.1 – 来自太阳动力天文台的太阳图像示例。

### 9.2.1 色度空间

#### RGB 空间

RGB 是一种加色空间，到目前为止它是数字图像最常用的颜色空间。每种颜色由三值元组（通常在整数范围 `[0,255]` 内）进行编码，代表组成颜色的红、绿、蓝分量。彩色图像的存储和显示大部分使用 RGB 空间中的像素值编码。它是图像处理中的“默认颜色空间”。

#### XYZ

XYZ 颜色空间是为了纠正 RGB 空间的某些缺陷而定义的。该空间由三个主色 X、Y 和 Z 组成，通过 `(R, G, B)` 元组的线性变换获得。根据国际

```
$b^* = 200[f(Y/Y_0) - f(Z/Z_0)]$
```亮度 `$L^*$` 代表颜色的清晰度，`$a^*$` 和 `$b^*$` 分别代表绿/红颜色和蓝/黄色（色彩）。亮度通过对单色刺激距离的视觉实验计算。阈值 `($\delta/2$)` 被选择以抑制周围 0 的剧烈变化。这个立方体在寻找人类眼睛如何看待颜色方面很有趣，尽管已经表明该空间中的欧几里得范数不是完全可靠的衡量标准。方法 `CImg<T>::RGBtoLab()`, `CImg<T>::LabtoRGB()`, `CImg<T>::XYZtoLab()`, `CImg<T>::LabtoXYZ()` 和它们的 `get_*` 版本将图像转换为 `$L^*ab^*$` 空间。

#### YUV 空间

该系统由 PAL 标准引入，基于 RGB 组件的转换：

![](img/6b7de6c7ce31f7bb2927e7184da0492f_232_0.png)

Y 代表亮度（带有伽马校正），U 和 V 代表色度。CImg 提供了方法 `CImg<T>::RGBtoYUV()`, `CImg<T>::YUVtoRGB()`（以及 `get_*`），`CImg<T>::load_yuv()` 和 `CImg<T>::save_yuv()` 来处理 YUV 颜色空间中的图像。

#### YCbCr 空间

YCbCr 空间是数字电视编码的国际标准。它是 JPEG 标准用于彩色图像损压缩的一部分。它在概念上接近 YUV。相关的数学变换是：

![](img/6b7de6c7ce31f7bb2927e7184da0492f_232_1.png)

方法 `CImg<T>::RGBtoCbCr()`, `CImg<T>::YCbCrtoRGB()`（及其 `get_*` 版本）将 RGB 图像转换为 YCbCr 空间（反之亦然）。

#### 使用三角形坐标的 HSI

HSI 表示（色相、饱和度、强度）源自 RGB 值：

```
$H = \arccos\left(\frac{0.5(R-G) + (R-B)}{\sqrt{(R-G)^2 + (R-B)^2}}\right), S = 1-\frac{\min(R,G,B)}{R+G+B}, I = \frac{R+G+B}{3}$
```

以及 `CImg<T>::RGBHSI` 和 `CImg<T>::HSIGB`（及其 `get_*` 版本）允许计算这些分量。这种表示基于视觉心理学，主要用于计算机图形领域。

#### HSV 表示

与 HSI 类似，HSV（色相、饱和度、值）模型基于 RGB 值构建：`$M=\max(R,G,B)$` 和 `$m=\min(R,G,B)$`，则：

```
$S = 1-\frac{m}{M}, V = M \text{ and } H = \begin{cases} \frac{(60G-B+360)}{M-m} \pmod{360} & \text{if } M=R \\ \frac{B-R}{M-m} +120 & \text{if } M=G \\ \frac{60R-G}{M-m} +240 & \text{if } M=B \end{cases}$
```

方法 `CImg<T>::RGBtoHSV()` 和 `CImg<T>::HSVtoRGB()`（及其 `get_*` 版本）提供了彩色图像在 HSV 空间中的转换。

#### HSL 表示

与 HSI 和 HSV 一样，HSL（色相、饱和度、亮度）从 RGB 值构建：如果 `$M=\max(R,G,B)$` 和 `$m=\min(R,G,B)$`，则：

```
$L = \frac{M+m}{2}, S = \begin{cases} \frac{2L}{M+m} & \text{if } L<0.5 \\ \frac{M-m}{2-2L} & \text{otherwise} \end{cases}, H = \begin{cases} \frac{(60G-B+360)}{M-m} \pmod{360} & \text{if } M=R \\ \frac{B-R}{M-m} +120 & \text{if } M=G \\ \frac{60R-G}{M-m} +240 & \text{if } M=B \end{cases}$
```

方法 `CImg<T>::RGBtoHSL()` 和 `CImg<T>::HSLtoRGB()`（及其 `get_*` 版本）处理 HSL 颜色空间中的图像。

#### CMY 和 CMYK 空间

CMY（青、品、黄）是专门用于在纸上打印数字彩色图像的空间。它是颜色减法合成的结果，由 RGB 空间的反色表示：原点 `(0,0,0)` 颜色为白色，青、品、黄色为轴。假设 RGB 颜色分量在 `[0,1]` 区间，则：

```
C = 1 - R, M = 1 - G and Y = 1 - B
```

由于材料需要（打印机），该空间通过添加第四个分量 K（黑色）进行了扩展，这一方面解决了打印机通过混合青、品、黄墨水恢复正确灰度所需的困难，另一方面，打印机除了青、品、黄墨盒外，还有一个黑色墨盒。CMYK 分量的计算如下：

```
K = min(C,M,Y), C' = C-K / 1-K, M' = C-K / M-K and Y' = C-K / Y-K
```

方法 `CImg<T>::RGBtoCMYK()`, `CImg<T>::CMYKtoRGB()`, `CImg<T>::RGBtoCMYK()`, `CImg<T>::CMYKtoRGB()` 以及它们的 `get_*` 版本允许处理这些 CMYK。

图 9.3 和 9.4 展示了在这些色度空间中获得的各种颜色通道值，针对由 RGB 值编码的翠鸟图像（幅图的第一行）。所有通道均已归一化以便可视化。

### 9.2.2 彩色成像中的中值滤波

如果中值概念在 R 中定义明确，那么将其概念推广到 R^d 则要容易得多，因为该空间没有顺序关系。但是可以指定一种等价公式，用于为光谱图像定义中值滤波算法。

令 `X = (x_1 ... x_n)` 为 n 个实值的集合。X 的中值可以定义为 X 中的值 `xm`，使得：

```
(∀j ∈ [[1,n]]) ∑ |x_m - x_i| ≤ ∑ |x_j - x_i|
```

遵循此定义，向向量情况的转换显而易见：如果 `$\mathbf{X}=(x_1\dots x_n)$` 是 `$\mathbb{R}^d$` 中的向量集合（在我们的案例中，对于彩色图像 `$d=3$`，对于 CMYK 情况则 `$d=4$`），那么我们可以将 `$\mathbf{X}$` 的中值元素 `$\mathbf{x}_m$` 定义为满足以下等式的元素：

```
$\forall j \in[[1,n]] \sum_{i=1}^n ||\mathbf{x}_m-\mathbf{x}_i|| \le \sum_{i=1}^n ||\mathbf{x}_j-\mathbf{x}_i||$
```

`$|\cdot||$` 是一个向量范数。

代码段 9.1 针对 `$L_2$` 范数实现了该滤波器。注意，在本文介绍的基础版本中，算法的复杂度是非常大的：对于大小为 `$p$` 的邻域，计算距离需要 `$O(p^2)$`，而寻找最小距离需要 `$O(p)$`，因此每个处理像素的复杂度为 `$O(p^3)$`。

> 代码 9.1 — 颜色成像中的中值滤波。

```c
CImg> ColorMedianFiltering(CImg> imgIn)
{
// 转换到感知均匀空间
imgIn.RGBToFloat();

CImg>
imgOut(imgIn,x,y,vL)
V(5,5,1,3), // 5x5 颜色邻域
vL = V.get_shared_channel(0),
va = V.get_shared_channel(1),
vb = V.get_shared_channel(2);

cimg_for5x5(imgIn,x,y,0,0,vL,float)
{
ncimg_get_5x5(imgIn,x,y,0,1,va,float);
cimg_get_5x5(imgIn,x,y,0,2,vb,float);

// 到中心像素的距离。
float dmin = 0;
cImg> z = V.get_vector_at(2,2);
cimg_forXY(V,i,j)
{
CImg> zi = V.get_vector_at(i,j);
dmin += (zi - z).magnitude();
}

cimg_forXY(V,i,j)
{
float d = 0;
cImg> z = V.get_vector_at(i,j);
cimg_forXY(V, u, v)
{
  CImg<> zi = V.get_vector_at(u, v);
  d += (zi - z).magnitude();
  if (d<dmin) {
    dmin = d;
    imgOut(x, y, 0) = V(i, j, 0);
    imgOut(x, y, 1) = V(i, j, 1);
    imgOut(x, y, 2) = V(i, j, 2);
  }
}
  return imgOut.LabtoRGB();
}
```

图 9.5 展示了彩色图像的中值滤波结果。在彩色测试图样 (a) 中添加了盐粒噪声 (b)。

生成的图像通过多光谱中值滤波器 (d) 进行处理，并通过通过逐通道应用的更经典的中值滤波 (c) 进行处理（参见第 5.1.2 节）。我们在细节 (e) 和 (f) 中清楚地看到，专门为彩色图像设计的中值滤波最小化了“伪色”的出现（唯一由噪声产生的假颜色），这与独立应用于每个通道的滤波不同，并且产生了更少的几何畸变（如白色和黑色网格）。

最后我们注意到，由于这种滤波依赖于颜色空间中距离的定义，我们倾向于使用感知均匀空间 `$L^*a^*b^*$`。

### 9.2.3 颜色成像中的边缘检测

为了能够通过颜色信息检测轮廓，可以将图像处理为向量场。

二维彩色 `$I(\mathbf{x}) = (I_R(\mathbf{x}), I_G(\mathbf{x}), I_B(\mathbf{x}))^T$` 可以被视为 `$\mathbb{R}^3$` 中 `$\mathbb{R}^2$` 的一个向量场，它将像素 `$\mathbf{x}$` 关联到其在 RGB 通道上的值。然后我们可以计算 `$I$` 在 `$\mathbf{x}$` 处的雅可比矩阵，定义为：

```
$J_1(\mathbf{x}) = \begin{pmatrix} \frac{\partial I_R}{\partial x} & \frac{\partial I_R}{\partial y} \\ \frac{\partial I_G}{\partial x} & \frac{\partial I_G}{\partial y} \\ \frac{\partial I_B}{\partial x} & \frac{\partial I_B}{\partial y} \end{pmatrix} = (\nabla I_R(\mathbf{x}), \nabla I_G(\mathbf{x}), \nabla I_B(\mathbf{x}))$
```

其中第二部分涉及 R、G、B 通道的梯度，最后部分展示了由对分量的偏导数组成的 `$\mathbb{R}^3$` 向量。为了计算任意方向 `$\theta$` 的颜色梯度，我们使用方向导数的定义：

```
$\nabla_\theta I(\mathbf{x}) = J_1(\mathbf{x})(\cos(\theta)) = \mathbf{I}_x(\mathbf{x})\cos(\theta)$
```

`$\nabla_\theta I(\mathbf{x})$` 的范数被称为 **局部对比度**，记作 `$S_\theta(I)$`。使得 `$S_\theta(I)$` 最大的 `$\theta$` 方向可以通过使 `$S$` 对 `$\theta$` 求导为零来找到。也可以通过对分量求偏导来计算任意 `$\theta$` 方向的颜色梯度。
