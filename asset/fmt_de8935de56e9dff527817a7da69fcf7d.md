
Similarly, when the chromaticity coordinates of physical colors are plotted on the chromaticity chart, the result it yields is shown in Figure 9.8 which is rather intuitive to follow. First, the projection of the conical volume on the triangular plane shown in Figure 9.6 would lead to a horseshoe shaped as shown in Figure 9.8. Second, note that the higher `x` means a much larger proportion of `X` which in turn means more intensity in the longer wavelengths and hence red. Similarly, the higher value of `y` indicates more intensity in middle wavelengths which is green. If both `x` and `y` are small - i.e. `z` is high – it means that `Z` is highest indicating more intensity in the lower wavelengths or blue.

### Fun Facts

![](img/66c45bbed85bb7ba7f7b05dff49b5060_231_0.png)

This plot shows the actual sensitivities of the S, M and L cones in the human eye where S, M and L stand for short, middle and long wavelengths. Note that the M and L plots are very close to each other. Further, the number of S cones is also much less than the M and L cones. Note that these plots are significantly different from the standard observer functions shown in Figure 9.5. This is due to the fact that these plots were physiologically measured only after mechanisms to do so were available to biological scientists and happened much later than the design of the standard observer functions. However, it can be shown that the `LMS` space can be related to the `XYZ` space by a linear transformation.

Note that in the chromaticity chart all the monochromatic colors are at the periphery. This is called the spectral boundary of the chromaticity chart. It is almost as if the wavelengths 400 to 700 have been placed around the boundary. There exists a straight line periphery of the chart that connects the two ends of the horseshoe. Which wavelengths do they represent?

To answer this question, let us go back to the visible spectrum of light (Figure 9.2). There are no wavelengths corresponding to purple which nevertheless is a color we perceive quite often. Also the colors change hue smoothly across the wavelengths i.e. blue changes slowly through cyan to green which then changes slowly through green-yellow to yellow which then changes through orange to red. So, cyan, which can be thought of as a combination of blue and green rests between blue and green. Similarly, orange rests between yellow and red. But, where are the purples? Shouldn't there be shades of purples between the high wavelengths red and lower wavelengths blue completing a circular representation of the visible colors of light? This is exactly the purples that show up as the straight line periphery of the chromaticity chart. There is no single wavelength to represent these colors and hence it is called the non-spectral boundary of the chromaticity chart.

Let us now consider a color `P` in this chart as in Figure 9.8. We connect `W` and `P` and extend the line backwards to meet the periphery of the chromaticity chart at `B`. The wavelength of the color at `B` is considered to be the dominant wavelength of `P`. Dominant wavelength is the sensation of the monochromatic wavelength evoked by `P` and is an estimate of the perceptual property of hue. Note that instead of `P`, if we consider a color `P′` and try to find its dominant hue, we will end up in the non-spectral part of the boundary which does not have a wavelength attached to it. In such cases (for purples), a dominant hue is

未定义。相反，我们将 `$W$` 连接到 `$P'$`，并将直线向后延伸至 `$B'$`。这被称为*补色波长*，即如果 `$P'$` 存在主波长，那么它与补色波长的叠加将产生中性色 `$W$`。

在色度图中，任意颜色的饱和度定义为：从该颜色 `$P$` 到白点的距离，与经过 `$P$` 且从 `$W$` 延伸到边缘的直线距离之比。在图 9.8 中，饱和度由此表示为 `$\frac{a}{b}$`。注意，当 `$P$` 是单色光时，它与 `$B$` 重合。因此 `$a=b$`，饱和度达到 1 或 100%，这与单色光的预期一致。另一方面，如果 `$P=W$`，则 `$a=0$`，饱和度为 0%，这与消色差颜色的预期一致。

最后，让我们考虑颜色的另一个属性，称为*亮度*（luminance），记为 `$Y$`。它被定义为颜色的*感知亮度*。为此，考虑以下实验：考虑两种强度相同但颜色不同的光——一种蓝色和一种绿色。因此，蓝色的 `$Z$` 值较高，而绿色的 `$Y$` 值较高。尽管这两种颜色的强度相同，但几乎所有人类都会觉得绿色比蓝色更亮。这是因为中间波长的光被赋予了比其他波长更高的优先级，即 `$Y$` 所表示的成分。这源于进化方面的原因：人类为了在陆地上生存，必须对周围的绿色特别敏感。这就是 `$Y$` 被称为亮度的原因，并且在感知任务中通常被认为非常重要。例如，在压缩图像时，`$Y$` 通道保持全分辨率，而其他两个通道被大幅降采样。

### 9.2.3 感知均匀颜色空间

`CIE XYZ` 颜色空间非常适合颜色匹配应用。例如，如果你想要叠加两台投影仪并匹配它们的颜色——你只需要确保它们在两个重叠像素上投影出相同的 `$XYZ$` 值即可。然而，在某些应用中，颜色之间的感知距离更为重要。

我们所说的感知距离是什么意思？它指的是，在差异变得可见之前，我们需要从一种颜色移动多少距离。为了理解感知距离的重要性，让我们考虑图像压缩的一个应用。在压缩图像时，我们可能希望稍微改变颜色以帮助压缩。这意味着将颜色从它们在颜色空间中的原始位置移动。但是，我们希望移动的幅度刚好足够大，使得变化不可见，并且压缩后的图像看起来非常接近原始图像。原始图像和压缩图像颜色之间的距离可以让我们了解这些图像在感知上的接近程度，从而用它来评估不同的压缩技术。在这类应用中，颜色之间的距离变得非常重要。

不幸的是，`CIE XYZ` 颜色空间在感知上是不均匀的。这意味着

![](img/66c45bbed85bb7ba7f7b05dff49b5060_233_0.png)

**图 9.9.** 该图显示了绘制在 CIE 1939 色度图（左）和 CIE 1976 *u′v′* 图（右）上的麦克亚当椭圆。每个椭圆中的颜色对人眼来说是无法区分的。

在颜色空间的不同区域中，相等的距离并不代表相等的感知差异。感知均匀的颜色空间意味着，如果我们想在色度图中围绕某种颜色 *P* 绘制一个几何形状，以显示与 *P* 接近且无法与 *P* 区分开的所有颜色集合，那么这个形状应该是一个圆，并且无论 *P* 位于何处，圆的大小都应相同。然而，对于基于 CIE 1939 *XYZ* 颜色空间建立的色度图，情况并非如此。科学家麦克亚当在色度图中针对不同颜色绘制了这一几何形状，结果如图 9.9 所示。注意，这些都是椭圆，且椭圆的形状和大小随颜色的位置而变化。这表明我们区分不同绿色调的能力远比区分紫色或黄色的能力差。而我们区分蓝色的能力可能是最好的。

因此，在 1964 年以及随后的 1976 年，人们努力通过对色度坐标进行非线性变换来设计感知均匀的颜色空间。已经设计出了多个这样的空间，例如 `CIE LUV` 或 `CIE Lab`。图 9.9 展示了其中一种于 1976 年设计的颜色空间，称为 CIELUV 空间。请注意，其感知距离比 1939 年的色度图均匀得多，但仍不理想。这方面最流行的空间是后来设计的 CIELab 空间，它由 `CIE XYZ` 空间推导而来。在 `CIE Lab` 空间中，欧几里得距离为 3 被认为是最小可觉差。然而，如果你有颜色匹配的应用需求，那么没有什么能比得上简单而古老的 `CIE XYZ` 空间及其衍生的色度图。

### 趣味知识

你知道吗，感知距离的概念在感知研究文献中已被充分研究？人们一直想知道，我们可以容忍多大的刺激差异而不会注意到它。例如，如果你正背着一本沉重的书，而你的负荷中又加入了一本 20 页的薄书，你很可能不会注意到。然而，如果你的负荷本身是一本 20 页的薄书，你一定会注意到变化。因此，要考虑的更重要的不是刺激的绝对变化，而是刺激的相对变化。在前一种情况下，你的重量刺激只改变了几个百分点；而在后一种情况下，它几乎翻倍了。事实上，以发现者命名的韦伯定律——感知研究文献中一个著名的定律——指出，我们感知差异的能力（更正式的说法是差异阈限）与刺激量成正比。这个比例常数在不同感知类型中会变化，但根据经验，10% 被认为是一个相当好的近似值。我们在感知灰度范围时也会看到同样的现象。在较暗的灰度值上，我们对差异比对较亮的灰度值更敏感。这也是我们的显示器 γ > 1.0 的另一个原因。这有助于我们在较低通道值处提供比在较高通道值处更高的分辨率。

## 9.3 结论

渲染方程最早于 1986 年在计算机图形学的两篇开创性工作中引入——[Immel et al. 86] 和 [Kajiya 86]。它在图像合成中的应用则通过 James Arvo 博士在 [Arvo and Kirk 90] 中的开创性工作得到推广。颜色是视觉计算领域中最令人困惑的话题之一，这主要是因为颜色有着悠久的历史，并且在许多不同领域中以各种方式被广泛使用，从艺术、绘画、物理、视觉、人类感知、视频处理和压缩，到最近的图像处理、计算机视觉和图形学。[Stone 03] 是一本优秀的使用手册，有助于理解这些不同的观点。[Reinhard et al. 08] 则提供了详尽的正式论述。

## 参考文献

[Arvo and Kirk 90] James Arvo 和 David Kirk。“粒子传输与图像合成。”*SIGGRAPH 计算机图形学*，第 63–66 页。

[Immel et al. 86] David S. Immel、Michael F. Cohen 和 Donald P. Greenberg。“一种用于非漫射环境的辐射度方法。”SIGGRAPH 计算机图形学 20:4 (1986)，133–142。

[Kajiya 86] James T. Kajiya。“渲染方程。”SIGGRAPH 计算机图形学 20:4 (1986)，143–150。

[Reinhard et al. 08] Erik Reinhard、Erum Arif Khan、Ahmet Oguz Akyz 和 Garrett M. Johnson。《彩色成像：基础与应用》。A. K. Peters 出版社，2008 年。

[Stone 03] Maureen C. Stone。《数字色彩实地指南》。A K Peters，2003 年。

## 总结：你了解这些概念吗？

- 辐射度量学与光度学

- 辐射亮度与辐射照度

- 双向反射分布函数（BRDF）

- 漫射照明

- 镜面照明

- Phong 光照模型

- 可见光谱

- 颜色刺激

- 同色异谱

- 三刺激值

- CIE XYZ 空间

- 色度坐标与色度图

- 强度、色相与饱和度

- 感知距离

# 练习

+   1. 颜色 `$C_1 = (X_1, Y_1, Z_1)$` 和 `$C_2 = (X_2, Y_2, Z_2)$` 的光谱分别由 `$s_1(\lambda)$` 和 `$s_2(\lambda)$` 给出。设光谱 `$s_1$` 与 `$s_2$` 相乘形成的颜色为 `$s_3$`，即 `$s_3(\lambda) = s_1(\lambda) \times s_2(\lambda)$`。那么与 `$s_3$` 对应的 XYZ 坐标 `$C_3$` 是否等于 `$(X_1 X_2, Y_1 Y_2, Z_1 Z_2)$`？请通过计算证明你的答案。

+   2. 考虑上图中左侧图像里的四种光谱，它们的颜色与其可见颜色无关，仅用于可视化。

+   (a) 所有这些颜色的主波长之间有什么关系？

+   (b) 所有这些颜色的饱和度之间有什么关系？

+   (c) 在色度图上，这些颜色与白点的距离之间有什么关系？

+   (d) 这些颜色的 `$I = X + Y + Z$` 之间有什么关系？

+   (e) 所有这些颜色的色度坐标将位于同一个几何实体上（例如圆、抛物线）。这个几何实体是什么？

+   (f) 所有这些颜色的 CIE `$XYZ$` 坐标将位于同一个几何实体上（例如圆、抛物线）。这个几何实体是什么？

+   3. 考虑上图中右侧图像里的光谱，它们的颜色与其可见颜色无关，仅用于可视化。

+   (a) 蓝色光谱最可能是哪种光谱的互补色？

+   (b) 哪些光谱的色度坐标会位于同一条直线上？

+   (c) 如果橙色和粉色光谱的色度坐标分别为 `$(0.1, 0.1)$` 和 `$(0.6, 0.3)$`，那么它们相加形成的颜色最可能的色度坐标是什么？

+   4. 在下图中，将右侧的物体与左侧它们最可能的颜色光谱进行匹配。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_237_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_237_1.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_238_0.png)

+   5. 考虑一个朗伯表面。它的 BRDF 会有多少维？简要描述一个简单的硬件装置和一种能够测量朗伯表面 BRDF 的算法。

+   

+   6. 你正在使用光谱辐射计测量一个中心为 *P* 的表面面片。该面片的半径为 2 毫米。光以 45 度角入射，角宽度为 20 度。测得的能量为 200 瓦/纳米。求 *P* 处的辐照度和辐亮度。

+   

+   7. 当你在教室里打开投影仪时，你看到它主要投射出黑色和紫色。你判断可能是连接 R、G、B 三基色的某根电线出了故障。是哪一根？为什么？

## 颜色再现

也许在读完上一章关于颜色的论述后，你会想知道 XYZ 颜色空间有什么用？要理解这一点，我们必须看一看所谓的颜色再现。当你想到由任何设备创建的图像时——例如，数码相机拍摄图像、投影仪投射图像或打印机打印图像——这些都是对来自物理场景（例如相机所拍摄的场景）或另一台设备（例如打印机打印相机拍摄的图像）的颜色的再现。颜色再现的质量通过再现图像与原始图像或场景的接近程度来评估。“接近”一词既可以从定量上衡量，也可以从定性上衡量。
