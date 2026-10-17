
## 9.2 颜色成像

遵循此定义，向向量情况的转换显而易见：如果 `X=(x1…xn)` 是 `R^d` 中的向量集合（在我们的案例中，对于彩色图像 `d=3`，对于 CMYK 情况则 `d=4`），那么我们可以将 `X` 的中值元素 `x_m` 定义为满足以下等式的元素：

```
$\forall j \in[[1,n]] \sum_{i=1}^n ||\mathbf{x}_m-\mathbf{x}_i|| \le \sum_{i=1}^n ||\mathbf{x}_j-\mathbf{x}_i||$
```

`|\cdot||` 是一个向量范数。

代码段 9.1 针对 `L_2` 范数实现了该滤波器。注意，在本文介绍的基础版本中，算法的复杂度是非常大的：对于大小为 `p` 的邻域，计算距离需要 `O(p^2)`，而寻找最小距离需要 `O(p)`，因此每个处理像素的复杂度为 `O(p^3)`。

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

图 9.5 展示了彩色图像的中值滤波结果。在彩色测试图样 (a) 中添加了盐粒噪声 (b)。生成的图像通过多光谱中值滤波器 (d) 进行处理，并通过通过逐通道应用的更经典的中值滤波 (c) 进行处理（参见第 5.1.2 节）。我们在细节 (e) 和 (f) 中清楚地看到，专门为彩色图像设计的中值滤波最小化了“伪色”的出现（唯一由噪声产生的假颜色），这与独立应用于每个通道的滤波不同，并且产生了更少的几何畸变（如白色和黑色网格）。

最后我们注意到，由于这种滤波依赖于颜色空间中距离的定义，我们倾向于使用感知均匀空间 `L*a*b*`。

### 9.2.3 颜色成像中的边缘检测

为了能够通过颜色信息检测轮廓，可以将图像处理为向量场。

二维彩色 `I(x) = (I_R(x), I_G(x), I_B(x))^T` 可以被视为 `R^3` 中 `R^2` 的一个向量场，它将像素 `x` 关联到其在 RGB 通道上的值。然后我们可以计算 `I` 在 `x` 处的雅可比矩阵，定义为：

```
$J_1(\mathbf{x}) = \begin{pmatrix} \frac{\partial I_R}{\partial x} & \frac{\partial I_R}{\partial y} \\ \frac{\partial I_G}{\partial x} & \frac{\partial I_G}{\partial y} \\ \frac{\partial I_B}{\partial x} & \frac{\partial I_B}{\partial y} \end{pmatrix} = (\nabla I_R(\mathbf{x}), \nabla I_G(\mathbf{x}), \nabla I_B(\mathbf{x}))$
```

其中第二部分涉及 R、G、B 通道的梯度，最后部分展示了由对分量偏导数组成的 `R^3` 向量。为了计算任意 `theta` 方向的颜色梯度，我们使用方向导数的定义：

```
$\nabla_\theta I(\mathbf{x}) = J_1(\mathbf{x})(\cos(\theta)) = \mathbf{I}_x(\mathbf{x})\cos(\theta)$
```

`nabla_theta I(x)` 的范数被称为 **局部对比度**，记作 `S_theta(I)`。使得 `S_theta(I)` 最大的 `theta` 方向可以通过使 `S` 对 `theta` 求导为零来找到。也可以通过对分量求偏导来计算任意 `theta` 方向的颜色梯度。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_240_0.png)

图 9.4 – 图像在不同颜色空间的表示。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_2.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_3.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_4.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_241_5.png)

图 9.5 – 单色中值滤波与彩色中值滤波的比较。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_2.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_3.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_4.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_5.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_6.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_242_7.png)

原始图像

轮廓的切向量

梯度范数

梯度相位

图 9.6 – 彩色成像中的局部对比度和梯度方向。

## 10. 3D 可视化

`ClImg` 库具有可视化和渲染 3D 网格对象的基本能力，这可以帮助开发者表示复杂的图像数据。在本章中，我们将对这些可能性进行快速概览，首先描述控制创建 3D 网格对象的通用原理，然后详细介绍这些对象在库内部的表示方式。我们将几个示例来说明不同的实际用例。

## 10.1 3D 网格对象的结构

在 `ClImg` 中，一个 3D 网格对象完全由四个不同结构的并集定义：

- 一组 3D 点，定义了对象的 N 个顶点。这些点的 3D 坐标存储在大小为 `N × 3` 的 `ClImg<T>` 图像中，其中 T 通常是 `float`。

- 一组 P 个原元（primitives），组成对象。每个原元可以是：四边形、三角形、段、点、球体（完美球面）或精灵（小图像）。段、三角形和四边形可以设置纹理。这存储为包含 P 个图像的 `ClImg<T>`，每个图像表示对象的一个单个原元。类型 T 通常是 `unsigned int`。

- 一组 P 个材质（materials），定义了每个原元的颜色或纹理。该集合存储为 `ClImgList<T>` 图像列表，每个图像表示单个原元的材质。类型 T 通常是 `unsigned char`。

- 一组 P 个透明度（opacities），定义了对象中每个原元的透明水平。该集合存储为大小为 `1 × P` 的图像 `ClImg<T>` 或 `CImg<T>` 列表。类型 T 通常是 `float`。

定义了这四个数据集后，可以通过 `CImg<T>::display_object3d()` 方法交互式地查看对应的 3D 对象，或者通过 `CImg<T>::draw_object3d()` 方法在图像中绘制它。此外，有一组 `CImg<T>` 方法返回预定义的 3D 网格对象，例如 `CImg<T>::box3d()`、`CImg<T>::sphere3d()`、`CImg<T>::torus3d()`、`CImg<T>::cylinder3d()` 等。两个独立的 3D 对象可以合并为一个，使用 `CImg<T>::append_object3d()` 方法。注意，材质和透明度集合没有出现在这些特性的签名中，因为它们只参与 3D 对象的装饰。代码 10.1 展示了如何使用这些不同函数创建并可视化复合 3D 网格对象（带球的链），连接多个简单的 3D 原元（圆环和球体）。

### 代码 10.1 - 简单3D 对象的创建与可视化

```cpp
// 要生成的 3D 对象结构
CImg<> g_points;
CImgList<unsigned int> g_primitives;

// 在链中添加圆环。
CImgList<unsigned int> primitives;
CImg<> points;
for (unsigned int k = 0; k<8; ++k) {
    points = CImg<>::torus3d(primitives, 100, 30);
    points.resize_object3d(240, 160, 60, k*30.f, 0.f);
    if (k%2) points.rotate_objectd(1, 0, 90);
    g_points.append_object3d(primitives, points);
}

// 在链的末尾添加球体。
points = CImg<>::sphere3d(primitives, 150).shift_object3d(100,0,0);
g_points.append_object3d(primitives, points);

// 创建带有颜色渐变的 800x600 背景。
CImg<unsigned char> background(1,2,1,3,"[64,128,255]:[255,255,255]",false);
background.resize(800,600,1,3);
```

```cpp
// 启动 3D 交互查看器。
background.display_object3d("3D Object",g_points,primitives);
```

ClImg 查看器中显示的 3D 对象。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_245_0.png)

图 10.1 – 代码 10.1 的结果：简单 3D 网格对象的创建。

## 10.2 函数 `z = f(x,y)` 的 3D 绘制

在不进一步探讨 `ClImg` 3D 网格对象实现细节的情况下，我们就可以利用已讨论的概念来构建一个可视化双变量函数 `f` 的有趣应用程序，形式为 3D 高度图。想法是允许用户为程序指定数学公式 `f(x,y)` 并创建一个 3D 形式的可视化。首先，我们从命令行获取不同的参数值（为用户未指定的参数定义默认值），并初始化函数 `f` 区域的最小和最大边界 `(x0,y0) - (x1,y1)`：

### 代码 10.2 - 从命令行获取参数。

在整个区域 `(x0,y0)-(x1,y1)` 上评估函数 `f(x,y)` 得于 `CImg<T>` 构造函数的以下版本：

```cpp
CImg(unsigned int size_x, unsigned int size_y,
unsigned int size_z, unsigned int size_c,
const char *values, bool repeat_values);
```

该构造函数的重载允许指定一个字符串参数 `values`，包含你希望赋予图像像素的值。该字符串可以是由逗号分隔的值列表，也可以是为构建中图像的每个像素进行评估的数学表达式。

我们将传递给构造函数的字符串将由三个公式拼接组成，前两行对预定义的 `x` 和 `y` 设置新值，以便它们线性归一化到区间 `[x0,x1]` 和 `[y0,y1]`。最后一行只是要评估的函数 `f(x,y)`。我们还允许平滑结果并归一化其值：

### 代码 10.3 — 生成高度图 `z = f(x,y)`.

```cpp
CImg<char> s_expr(1024);
std::printf(s_expr,"x = lerp(%g,%g,x/(w-1));");
       "y = lerp(%g,%g,y/(h-1));";
       "%s";
       x0,y0,y1, expr);
CImg<> elevation(resolution,resolution,1,1,s_expr,true);
elevation.blur(sigma).normalize(factor);
```

在第二步中，我们使用相同的构造函数生成一个由四种颜色（红、橙、黄和白）线性插值构建渐变色板（代码 10.4）。

```cpp
CImg<unsigned char>
lut(4,1,1,3,"!?[255,79,106]:"); // 红
     "X=1:192,115,149"; // 橙
     "X=2:[231,250,90]:"; // 黄
     "[355,255,255],",true); // 白
lut.resize(256,1,1,3);
```

```cpp
// 生成 'elevation' 的颜色表示。
CImg<unsigned char>
c_elevation = elevation.get_normalize(0,0.255).map(lut);
```
