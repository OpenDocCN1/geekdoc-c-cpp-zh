
![](img/6b7de6c7ce31f7bb2927e7184da0492f_61_0.png)

图 3.2 —— 数学变换的示例。从左到右是：输入图像 $I$、$exp(I/50)$、$10\sqrt{I}$、$log(1+|I|)$ 和 $I^3$。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_61_1.png)

图 3.3 —— 从公式

最后，有时可能使用另一个图像 J 来转换图像。`CImg` 提供了执行图像之间点操作的方法：加法（重载运算符 `+`, `-`）、乘法（`mul(CImg<T>& imq)`）、除法（`div(CImg<T>& img))`），甚至幂运算（`pow(CImg<T>& imq)`），其中 `I` 中的每个像素提升到 `J` 中对应像素的灰度幂。例如，在图 3.4 中写入

```cpp
CImg<C> C = A.get_pow(B);
```

在 `A` 和 `B` 上产生图像 `C`。

# 第3章. 点处理变换

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_2.png)

图 3.4 – 使用另一图像对图像进行点处理的示例。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_3.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_4.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_5.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_62_6.png)

图 3.5 – 某些二值操作的说明。

代码 3.3 – 使用 LSB 方法进行隐术。

```
CImg<unsigned char>
imgIn("butterfly.bmp"),
mess("message.bmp");
// 像素在0的背景上被设置为1。
mess.threshold(128);
CImg<unsigned char> imgIn2 = imgIn.get_channel(0);
// 编码步骤。我们移除了最低位中的 1。
imgIn2 &= 0xFE;
// 在最低位中编码消息。
CImg<unsigned char> imgOut = imgIn2 | mess;
// 解码步骤。
CImg<unsigned char> res = (imgOut&1) *= 255;
```

## 3.1 图像操作

隐术是隐藏的艺术：它的目的是让消息在不被察觉的情况下传递在另一个消息内部，它与密码学（“秘密的艺术”）不同，后者寻求让消息对任何其他人都是不可理解的。用比喻来说，隐术就像是将金钱埋在你的花园里，而密码学则是将它锁在保险箱里。这没有什么可以阻止这两种技术，就像人们可以将保险箱埋在花园里一样。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_63_0.png)

a) 消息

![](img/6b7de6c7ce31f7bb2927e7184da0492f_63_1.png)

隐术是隐藏的艺术：它的目的是让消息在不被察觉的情况下传递在另一个消息内部，它与密码学（“秘密的艺术”）不同，后者寻求让消息对任何其他人都是不可理解的。用比喻来说，隐术是将金钱埋在你的花园里，而密码学则是将它锁在保险箱里。这没有什么可以阻止这两种技术，就像人们可以将保险箱埋在花园里一样。

b) 原始图像

![](img/6b7de6c7ce31f7bb2927e7184da0492f_63_2.png)

c) 带有隐藏消息的图像

![](img/6b7de6c7ce31f7bb2927e7184da0492f_63_3.png)

d) 解码消息

图 3.6 – 使用最低位编码策略的隐术。

### 3.1.3 对比度增强

当图像 $I$ 的对比度较低时，增加其灰度范围（或彩色图像的颜色范围）可能是很有。为了做到这一点，最简单的方法是在区间 $[0, N-1]$ 上定义一个分段线性函数。该区间被划分为 $M$ 个子区间 $[g_i, g_{i+1}]$，其中 $g_0 = 0, g_{M-1} = N-1, i \in [0, M-2]$，并且对于这些每一个区间，定义一个线性变换：

```
$$\forall j \in [g_i, g_{i+1}] \quad T_i(j) = a_i \cdot j + b_i$$
```

其中 $T_i(g_{i+1}) = T_{i+1}(g_{i+1}), i \in [0, M-2]$。

这组变换可以用于，例如计算图像的负值，或执行阈值操作。它们可以通过查找表（LUT）来视化，查找表给出了新旧灰度之间的对应关系（图 3.7）。当然，之前描述的数学变换定义了 LUT，对应于在图像强度域上的函数图。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_64_0.png)

图 3.7 – 某些查找表。

## 3.2 直方图操作

一类重要的点操作与图像或部分图像的直方图有关。

### 3.2.1 定义

一类重要的点操作与图像或部分图像的直方图相关。

定义：直方图与图像或部分图像的直方图相关。

### 3.2.2 直方图规格

一类重要的点操作与图像或部分图像的直方图相关。

直方图与图像或部分图像的直方图相关。

### 3.2.3 局部直方图规格

之前的方法为输入图像 $I$ 中具有相同灰度的所有像素分配了理想灰度。因此，变换后图像中的区域会有明显的边界，这可能不遵循 $I$ 中的原始边界。为了解决这个问题，可以仅在像素的邻域内计算直方图，并仅将规格应用于此中心像素。这种简单的修改导致了空间图像处理技术的定义，将在第 5.1 节中以空间过滤为例进行说明。

## 3.2 直方图操作

![](img/6b7de6c7ce31f7bb2927e7184da0492f_67_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_67_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_67_2.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_67_3.png)

图 3.8 – 直方图均衡化。

```cpp
CImg<> hist = imgIn.get_histogram(nb, vmin, vmax);
long int cumul = 0;
```

```cpp
// 累积直方图。
cimg_forX(hist, pos)
{
    cumul += hist[pos];
    hist[pos] = cumul;
}
```

```cpp
if (cumul==0) cumul = 1;
```

```cpp
// 均衡化图像。
cimg_for(imgIn, off)
{
    int pos = (int)((imgIn[off] - vmin) * (nb - 1)/vdiff);
    if (pos>=0 && pos<(int)nb)
        imgOut[off] = vmin + vdiff*hist[pos]/size;
}
```

```cpp
return imgOut;
```

![](img/6b7de6c7ce31f7bb2927e7184da0492f_68_0.png)

# 4. 数学形态学

数学形态学 [36] 是最初设计用于探索图像中对象几何结构的形式化方法。基于这些工具的技术发展使得应用领域得以扩大，例如用于对比度增强或滤波。从“模式识别”的角度来看，图像处理旨在从给定图像中提取几何信息（位置、周长、面积、方向、……），从而在场景中区分对象。

在数学形态学的语文中，为了提取特定的几何结构，关键在于设计一种形状算子，该算子具有某些预期的属性（例如平移不变性），并允许区分特定的对象。这里会产生几个问题，特别是对象是不透明的，因此形状信息不是相加的。事实上，场景中的对象主要以两种形式组合：

- * 通过集合的并（重叠对象）：$X = X_1 \cup X_2$

- * 通过集合的交（遮挡）：$X = X_2 \setminus X_1 = X_1^c \cap X_2$

设计的形状算子 $\Psi$ 必须对并集和交集满足分配律（等同于线性），即：

- * $\Psi_\delta(X_1 \cup X_2) = \Psi_\delta(X_1)\Psi_\delta(X_2)$

- * $\Psi_\epsilon(X_2 \setminus X_1) = \Psi_\epsilon(X_1)\cap\Psi_\epsilon(X_2)$

第一个操作被称为形态学膨胀（dilation），第二个操作被称为形态学腐蚀（erosion）。这两个操作是数学形态学的的基础，在此基础上可以设计更复杂的形态算子。

在下文中，我们在二值图像背景下规定腐蚀、膨胀以及各种操作的概念，然后将讨论扩展到更一般的灰度图像情况。

## 4.1 二值图像

设 $A, B \subset \mathbb{Z}^2$ 为两个集合，元素标记为 $\mathbf{a} = (a_1, a_2)$ 和 $\mathbf{b} = (b_1, b_2)$：

- * $A$ 关于 $x = (x, y)$ 的平移记作 $(A)_x$，为 $(A)_x = \{\mathbf{c} = a+x, \mathbf{a} \in A\}$

- * $B$ 的反射记作 $B'$，为 $B' = \{-\mathbf{b}, \mathbf{b} \in B\}$

- * $A$ 的补集记作 $A^C = \{\mathbf{x}, \mathbf{x} \notin A\}$

- * $A$ 与 $B$ 的差为 $A \setminus B = A \cap B^C = \{\mathbf{x}, \mathbf{x} \in A, \mathbf{x} \notin B\}$

在本节中，$A$ 是二值图像，$B$ 是二值形状算子。

### 4.1.1 膨胀与腐蚀

> **定义 4.1.1** $A$ 被 $B$ 膨胀记作 $A \oplus B$，由以下集合定义

$$A \oplus B = \{\mathbf{x}, (B')_x \cap A \neq \emptyset\}$$

> **定义 4.1.2** $A$ 被 $B$ 腐蚀记作 $A \ominus B$，由以下集合定义

$$A \ominus B = \{\mathbf{x}, (B)_\mathbf{x} \subseteq A\}$$

$B$ 是形状算子，在数学形态学中称为**结构元素**（structuring element）。

为了清楚起见，对于二值对象 $A$ 和二值对称结构元素 $B$，形态学的简单操作包括遍历图像并将 $B$ 视为一个二值掩码：如果以 $x$ 为中心时，$B$ 与 $A$ 相交，则 $A$ 被 $B$ 膨胀在 $\mathbf{x}$ 处的值为 1，否则为 0。同样，如果 $B$ 未被完全包含在 $A$ 中，则 $A$ 被 $B$ 腐蚀在 $\mathbf{x}$ 处的值为 0，否则为 1（图 4.1）。因此，腐蚀根据 $B$ 缩小 $A$，而膨胀则扩展 $A$。

当 $B$ 不对称时，必须考虑结构元素的反射（图 4.2）。

很容易证明，相对于补集，腐蚀是膨胀的偶变换：$A \ominus B = (A^C \oplus B^C)^C$。因此，它等同于对对象进行腐蚀，或对其补集进行膨胀。

在 `CImg` 中的实现使用了专门的方法 `CImg<T>::erode()` 和 `CImg<T>::dilate()`（代码 4.1）。

```cpp
Code 4.1 膨胀与腐蚀。
```

```cpp
CImg<unsigned char> img("in.png");
// 结构元素。这里是一个 3x3。
```

## 4.1 二值图像

```cpp
CImg<unsigned char> B(3,3);
B.fill(1);

CImg<unsigned char> imgErode = img.erode(B); // 腐蚀
CImg<unsigned char> imgDilate = img.dilate(B); // 膨胀
```

![](img/6b7de6c7ce31f7bb2927e7184da0492f_71_0.png)

原始图像

腐蚀

![](img/6b7de6c7ce31f7bb2927e7184da0492f_71_1.png)

膨胀

图 4.1 – 使用 $3 \times 3$ 结构元素的腐蚀和膨胀。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_71_2.png)

图 4.2 – 腐蚀与膨胀。结构元素 $B$ 不对称。

结构元素的大小会影响结果。特别是，腐蚀会移除小于结构元素尺寸的细节；相反，膨胀会扩大对象并连接它们。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_0.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_1.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_2.png)

图 4.3 – 结构元素大小的影响。

### 4.1.2 开运算与闭运算

基于膨胀和腐蚀算子，我们可以定义两个新操作：**开启**（opening）和**闭运算**（closing）。

> **定义 4.1.3** $A$ 的 $B$ 开运算为 $A \circ B = (A \oplus B) \ominus B$

> **定义 4.1.4** $A$ 的 $B$ 闭运算为 $A \nabla B = (A \ominus B) \oplus B$

开运算通常会平滑二值形状的轮廓，断开对象间的连接（颈），并消除小的孤立对象（根据 $B$ 的意义）。闭运算倾向于平滑轮廓，聚集小的空洞（根据 $B$ 的意义）并连接轮廓。

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_3.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_4.png)

![](img/6b7de6c7ce31f7bb2927e7184da0492f_72_5.png)

图 4.4 – 使用 $11 \times 11$ 结构元素的开运算和闭运算。

```cpp
Code 4.2 开运算与闭运算的实现。
```

```cpp

CImg<unsigned char> img =("in.png");

// 结构元素。这里是一个 3x3。

CImg<unsigned char> B(3,3);

B.fill(1);

CImg<unsigned char> imgErode = img.erode(B);           // 腐蚀

CImg<unsigned char> imgDilate = img.dilate(B);        // 膨胀

CImg<unsigned char> imgOpening = imgErode.get_dilate(B); // 开运算
```
