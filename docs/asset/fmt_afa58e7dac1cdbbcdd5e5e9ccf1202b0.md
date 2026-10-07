
```c
CImg<> Takahara(CImg<& imgIn)
{
  CImg<> imgOut(imgIn);

//Kuwara.
CImgList<unsigned char> Kuhara(4,5,1,1,0);
img_for(Kuwara[0],0,0,2,1) Kuhara(j) = 1;
for (int i = 1; i<4; ++i)
Kuwara[i] = Kuhara[0].rotate(i*90);

```,// 邻域分析.

CImg<>

mu(9,1,1,0),

sigma(9,1,1,0),

st,

N(5,5);

CImg<int> permutations;

cimg_for5x5(imgIn,x,y,0,0,N, float)

{

  CImg<> res(4);
  for (int i = 0; i<4; ++i) {
    res[i] = N.get_mul(Kuwahara[i]);
    st = res[i].get_stats();
    mu[i] = st[2];
    sigma[i] = st[3];
  }
  sigma.sort(permutations);
  imgOut(x,y) = mu[permutations[0]];
}

return imgOut;

```
![](img/6b7de6c7ce31f7bb2927e718da0492f_99_0.png)

噪声图像（高斯噪声 $\mathcal{N}(0,4)$）Nagao Kuwahara

图 5.12 – Nagao 和 Kuwahara 滤波器的比较。

## 5.2 递归滤波

如前，图像轮廓检测需要可以通过离散卷积实现的导数（第 5.1.3 节，公式 5.1）。通过这种方法，检测可以形式化为空间域中的滤波问题。然而，这种数值计算在存在噪声时是不有效的，因此要在导数中添加平滑滤波器。例如，Prewitt 和 Sobel 的工作（图 5.8）针对该任务使用平均滤波或高斯低通滤波器是经典的。这种方法的一个典型示例可以在 [5] 中找到，该文献开发了一种最优有限响应（FIR）滤波器。

第 5 章 滤波

作者提出了通过高斯函数的导数进行近似的方法（公式 5.3）。该滤波器允许 Canny 标准则达到 0.97，从而使最优结果下降了 20%。

```
$h_{opt}(x) \approx h_{canny}(x) = -x\exp\left(\frac{(\alpha x)^2}{2\pi}\right) \quad (5.3)$
```

该滤波器的标准差与滤波器的缩放参数成反比。需要注意的是，按照 Canny 的建议，该算子的直接实现所需的操作次数与滤波器的标准差成正比，这意味着其算法复杂度很高，特别是在需要大滤波器的高噪声图像情况下。

### 5.2.2 Deriche 滤波器

在 Deriche 的工作 [10] 中，作者采用了 Canny 的准则，并成功开发了一种无限脉冲响应（IIR）滤波器形式的更简单的解析解，其递归实现确保了无论滤波器宽度如何，操作次数都是恒定的。通过放宽对 FIR（有限脉冲响应）滤波的选择，选择了不同的边界条件（$h(0)=0, h'(+\infty)=0$ 和 $h'(0)=s$），我们得到了以下系数值：$c_0=c_1=c_2=c_4=0$。根据公式 5.2，最优边缘检测滤波器变为：

```
$h_{opt}(x) = cxe^{-\alpha x} \sin \omega x$.
```

该算子的 Canny 标准 $\Sigma$ 提升了 25% ($\Sigma=\sqrt{3}$)。极限 $\omega \to 0$ 提供了遵循这三个性能标准要求的最佳折中方案（公式 5.4）。该算子对应 Canny 标准优化问题的精确解。这种最优边缘检测算子在文献中被称为*Deriche滤波器*。

```
$h_{opt}(x) = h_{deriche}(x) = -cxe^{-\alpha x}$ with $c = \frac{(1-e^{-\alpha x})^2}{\alpha}$ \quad (5.4)$
```

其中 $c$ 是滤波器的归一化系数。在文献中，根据所需的归一化类型，经常找到不同的 $c$ 值。图 5.14 展示了 Canny（公式 5.3）和 Deriche（公式 5.4）滤波器。

该滤波器允许我们使用基于一阶导数滤波器 $f_{deriche}(x)$ 的轮廓检测器。这个标记为 $f_{deriche}(x)$ 的平滑滤波器通过积分最优滤波器 $f_{deriche}(x)$ 。我们也可以通过最优解推导出二阶导数滤波器。

```
$f_{deriche}(x) = k(\alpha|x|+1) e^{-\alpha|x|}$ with $k = \frac{(1-e^{-\alpha x})^2}{1+2\alpha e^{-\alpha x}-e^{-2\alpha x}}$ \quad (5.5)$
```

## 5.2 递归滤波

![](img/6b7de6c7ce31f7bb2927e7184da0492f_103_0.png)

图 5.14 – 用于计算一阶导数的连续形式的 Canny 滤波器和 Deriche 滤波器。

# DERICHE 滤波器族的实现

Deriche 轮廓滤波器不仅对应于 Canny 标准优化问题的精确解，而且具有一个显著特性（与其平滑滤波器和导数滤波器相同），即可以用少量操作进行递归实现，与滤波器宽度无关。

有限与无限脉冲响应滤波器的区别

- FIR 滤波器是其有限尺寸允许通过实现数值卷积的滤波器，其输出 $I_o[i]$ 与输入（记为 $I_i[i]$）之间的关系写入如下：

```
$$I_o[i] = \sum_{k=-L}^{L} H[k] \times I_i[i-k].$$
```

$H[i]$ 是滤波器的数值脉冲响应。如果滤波器的脉冲响应是无限的则无法使用此表达式。
如果系统是 BIBO（有界输入有界输出）稳定的，那么对于任何输入，系统的输出也是稳定的。在离散信号上，系统是 BIBO 稳定的当且仅当 $\sum_{n=-\infty}^{\infty} |h(n)| = ||h||_1 < \infty$。很容易证明，如果 $L < \infty$，无论使用什么系数，FIR 滤波器都是无条件稳定的。

IIR 滤波器可以精确地递归实现，其计算成本低于前者，但必须注意它们的稳定性。输出（记为 $I_o[i]$）与输入 $I_i[i]$ 之间的关系写入如下：

```
$I_o[i] = \sum_{k=0}^{N} b_k \times I_i[i-k] - \sum_{k=1}^{M} a_k \times I_o[i-k] \quad (5.6)$
```

其中系数 $a_i$ 和 $b_i$ 根据滤波器的脉冲响应 $H[i]$ 计算。这种类型的滤波器使用递归方案，需要 $(N+M+1)$ 次操作，该数量更小且与滤波器的大小无关。还需要注意的是，与 Deriche 滤波器或其导数及平滑滤波器的卷积可以用公式 5.6 的形式精确实现。这种显著特性并非所有 IIR 滤波器所具有（高斯滤波器不是）。以最小二乘法近似高斯滤波器及其导数的卷积递归实现已由 Deriche [1] 和其他作者 [4] 开发。由 $K$ 个样本的一维信号 $I_l$ 与最优 Deriche 轮廓检测滤波器的卷积通过以下二阶公式精确实现：

导数滤波器：

```
$h_{deriche}(x) = -ce^{-\alpha|x|}$
```

```
$$\begin{cases} I_o[i] = \dots \text{for } i \in [1,K] \end{cases}$$
```
（注：此处原文公式似乎不完整）其中 $a = ce^{-\alpha}, b_1 = -2e^{-\alpha}$ 和 $b_2 = e^{-2\alpha}$。

### 5.2 递归滤波（续）

平滑滤波器：

```- $f_{deriche}(x) = k(\alpha|x|+1)e^{-\alpha|x|}$
```

```
$I_o[i] = a_0 + a_1I_o[i-1] + a_2I_o[i-2] + a_3I_o[i-3] \quad i \in [1,K]$
$a_0=0, a_1 = k(\alpha-1)e^{-\alpha}, a_2 = k(\alpha+1)e^{-\alpha}, b_1 = -2e^{-\alpha}, b_2 = e^{-2\alpha}$
```
代码 5.6 允许沿 X 轴应用 Deriche 滤波器。order 参数允许选择平滑滤波器（0阶）、一阶导数（1阶）或二阶导数（2阶）。

# 代码 5.6 - Deriche 滤波器

```c
/*
1D信号上的 Deriche 滤波器（沿 X 轴）。

imgIn      : 输入图像
alpha      : 缩放参数
order      : 滤波器阶数           (0: 平滑, 1: 一阶导数
           2: 二阶导数)
boundary_conditions : 边界条件
*/
void deriche(float imgIn, float alpha, unsigned int order=0,
             bool boundary_conditions=true)
{
    // 滤波器系数
    float
    ema = std::exp(-alpha),
    ema2 = std::exp(-2*alpha),
    b1 = -2*ema,
    b2 = -2*ema,
    a0 = 0, a1 = 0, a2 = 0, a3 = 0,
    coefp = 0, coen = 0;
    switch (order)
    case 0: // 0 阶（平滑）
        float k = (1 - ema)/(1 + 2*alpha*ema - ema2);
        a0 = k;
        a1 = k*(alpha - 1)*ema;
        a2 = k*(alpha + 1)*ema;
        a3 = -k*ema;
        break;
    case 1: { // 1 阶（一阶导数）
        float k = -(1 - ema)/(2*(ema + 1)*ema);
        a0 = a3;
        a1 = k*ema;
        a2 = -a1;
    }
    break;
    case 2: { // 2 阶（二阶导数）
        float
        ea = std::exp(-alpha);
        k = (-ema2 - 1)/(2*alpha*ema);
        kn = (-2*(-1 + 3*ea - 3*ea*ea + ea*ea*ea))/(3*ea + 1 + 3*ea*ea + ea*ea*ea);
        a0 = kn;
        a1 = -kn*(1 + k*alpha)*ema;
        a2 = -kn*(1 - k*alpha)*ema;
        a3 = -kn*ema;
    }
    coefp = (a0 + a1)/(1 + b1 + b2);
    coen = (a2 + a3)/(1 + b1 + b2);
    // 应用递归滤波器（逐行处理）
    CImg<> Y(imgIn.width());
    cimg_forYC(imgIn,y,c)
    {
      float *X = imgIn.data(0,y,0,c);
      // 从左到右计算
      float yb = 0, yp = 0, xp = 0;
      if (boundary_conditions) {
        xp = X[0];
        yb = yp = coefp*xp;
      }
      cimg_forX(imgIn,m)
      {
        float xc, yc;
        xc = X[m];
        yc = Y[m] = a0*xc + a1*xp - b1*yb;
        xp = xc;
        yp = yc;
      }
      // 从右到左计算
      float xn = 0, xa = 0, yn = 0, ya = 0;
      if (boundary_conditions) {
        xn = X[imgIn.width()-1];
        ya = ya = coen*xn;
      }
      cimg_forX_rev(imgIn,m)
      {
        float xc, yc;
        xc = X[m];
        yc = Y[m] = a0*xc + a1*xp - b1*yb; // 注意：原文逻辑此处似乎重复或不完整
      }
    }
}
```

## 5.2 递归滤波

```
xn = xa = X[imgIn.width() - 1];
yn = ya = cofn.xn;
}
for (int n = imgIn.width() - 1; n>=0; --n) {
    float xc = X[n],
    yc = a2*xn + a3*xa - b1*yn - b2*ya;
    xa = xn;
    xn = xc;
    ya = yn;
    yn = yc;
    X[n] = Y[n] + yc;
}
```

# DERICHE 滤波器的结果

使用 Deriche 滤波器可以执行许多有趣且快速的过程。图像平滑（0阶滤波器）

由于其递归实现，无论参数 $\alpha$ 指定滤波器宽度如何，Deriche 平滑滤波器具有恒定的计算复杂度。利用滤波器的可分离性，我们可以通过沿 X 轴滤波来对二维图像 $I$ 进行平滑，然后转置图像（等同于旋转 90°），再次应用滤波器并再次转置图像（代码 5.7）。

> 代码 5.7 – 使用 Deriche 滤波器对二维图像进行平滑。

```cpp
CImg = imgIn("test.bmp"); // Loading the image
dereriche(imgIn,alpha,0); // X filtering
imgIn.transpose();
dereriche(imgIn,alpha,0); // Y filtering <==
imgIn.transpose(); // X filtering of transposed image
```
```

图 5.15 展示了不同 $\alpha$ 值的平滑滤波结果。此尺度参数越大，图像的平滑程度越低。

92

第 5 章 滤波

![](img/6b7de6c7ce31f7bb2927e7184da0492f_108_0.png)

图 5.15 – 不同尺度参数 $\alpha$ 值的 0阶 Deriche 滤波器（平滑滤波器）的结果。

梯度范数的计算（一阶滤波器）：

为了计算梯度范数，我们可以计算沿 X 轴的一阶导数和沿 Y 轴的一阶导数（通过转置图像），然后从两个滤波后的图像计算梯度范数。对于每个导数，最好沿相反轴使用 0 阶 Deriche 滤波器对图像进行预平滑，以便在空间平滑的图像上以等向性的方式计算导数（代码 5.8）。

$$\begin{cases} \frac{\partial I}{\partial x}(x,y) = (I * f_{deriche}(y)) * h_{deriche}(x) \\ \frac{\partial I}{\partial y}(x,y) = (I * f_{deriche}(x)) * h_{deriche}(y) \end{cases}$$

$|I|(x,y) = \sqrt{\left(\frac{\partial I}{\partial x}(x,y)\right)^2 + \left(\frac{\partial I}{\partial y}(x,y)\right)^2}}$

# 代码 5.08 – 使用 Deriche 滤波器计算梯度范数。

```cpp
CImg imgIn = imgIn("image.bmp"); // Loading the image
imgX = imgIn.get_transpose();
imgY = imgIn;

dereriche(imgX,alpha, 0); // Pre-smooth along 'Y' for 'd/dX'
dereriche(imgY,alpha, 0); // Pre-smooth along 'X' for 'd/dY'
```

## 5.2 递归滤波

```cpp
imgX.transpose(); imgY.transpose();
dereriche(imgX,alpha,1); // First derivative along 'X'
dereriche(imgY,alpha,1); // First derivative along 'Y'
imgY.transpose();
```

```cpp
CImg Norme = (imgX.sqr() + imgY.sqr()).get_sqrt();
```

图 5.16 展示了在不同 $\alpha$ 值下 Deriche 滤波器计算梯度范数的结果。提取图像梯度的局部极大值允许我们检测轮廓。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_109_0.png)

图 5.16 – 不同尺度参数 $\alpha$ 值的的一阶 Deriche 滤波（梯度范数计算）结果

拉普拉斯计算（二阶滤波器）：

拉普拉斯算子等于图像沿 X 和 Y 轴的二阶导数和。可以使用二阶 Deriche 滤波器快速快速地计算（代码 5.9）。
