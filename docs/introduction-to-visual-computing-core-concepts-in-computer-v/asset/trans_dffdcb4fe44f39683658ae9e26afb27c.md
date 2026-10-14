

这种光效率低下成为在显示器上创建光谱准确的颜色再现的主要制约因素。光谱准确的显示器需要高度饱和（因此带宽窄）的原色，并且这些原色必须足够明亮以满足显示器所需的光效率。直到今天，创建用于显示器的如此超亮的饱和原色在实践上几乎是不可能的。但是，未来六原色激光投影仪所承诺的色域，如图10.3中青色多边形所示，显示出实现这一目标的希望，希望很快就能实现。

## 有趣的事实

色彩标准世界对于消费者来说可能是一个令人困惑的方面。术语 NTSC、HDTV、UHDTV 究竟意味着什么，以及它们对图像质量有什么影响？色彩标准定义的起源可以追溯到1940年代，当时电视行业感到有必要为视频信号的传输定义一些标准。由于那时是黑白电视的时代，与传输相关的唯一属性是图像的空间分辨率，其分辨率为 640 × 480，分辨率为 4:3 的纵横比（屏幕宽度与高度之比）。1953年，随着彩色电视的出现，色彩被添加到标准中。这包括指定标准二维色域和白点（如图10.3所示）。这一直是主要标准，直到大约2010年，数字内容的出现导致了 HDTV（高清电视）标准的发展。这将分辨率更改为 1920 × 1080，并略微扩展了色域（如图10.3所示）。这也引入了宽屏电视的概念，其纵横比为16:9。最近，有一种新的标准称为 UHDTV（超高分辨率电视），其分辨率加倍至 3840 × 2160。但我们已经达到了在标准电视尺寸下用 HDTV 感知分辨率的能力极限。因此，UHDTV 在分辨率方面并不能带来巨大的质量差异。然而，色域也显著扩展，承诺带来更加鲜艳的显示。此外，UHDTV 标准现在允许高动态范围图像，这与扩展的色域一起，应该大大改善电视的色彩质量。

## 10.5 结论

色彩再现需要结合精确的数学以及人类感知的局限性和/或不精确性——通常涉及人类认知——使其成为非常困难的科学或应用。

像 [Palmer 99] 这样的书籍所提供的对人类感知的深入了解，在这个领域非常有用。专注于色彩再现工程方面的文本包括 [Hunt 95, Berns et al. 00]。来自生物学、艺术、科学和工程等不同领域的人们参与色彩模型的发展，既是福也是祸，导致色彩再现成为一个复杂的探索领域。因此，经常有用的是从另一种视角来看待色彩，如 [Livingstone and Hubel 02]。

在1990年代末和2000年代初期，对高动态范围图像进行了大量工作。这是由 [Debevec and Malik 97] 中捕获 HDR 图像的初始工作所刺激的。这导致了在传统显示器上显示此类图像的适当色调映射算子的大量工作 [Tumblin and Turk 99, Larson et al. 97, Gallo et al. 09]。设计了新的 HDR 相机 [Yasuma et al. 10]。能够真正显示如此高动态范围的显示器也被设计出来 [Seetzen et al. 04]。今天，这样的显示器变得更加主流，正在市场中缓慢出现。HDR 成像至今仍是一个活跃的研究领域 [Gupta et al. 13]。关于 HDR 成像管道的综合参考是 Reinhard 等人关于该主题的最新书籍 [Reinhard et al. 05]。多光谱相机 [Yasuma et al. 10, Susanu 09, Shogenji et al. 04] 和显示器 [Li et al. 15] 已经被探索过，但它们尚未进入消费设备。唯一成功的案例是使用 RGBW 投影仪，在投影灰度时除了红色、绿色和蓝色滤光片外还使用一个清晰滤光片，以提高亮度等级。然而，这并不能帮助增加二维色域，因为白色位于 R、G 和 B 创建的色域内。

## 参考文献

[Berns et al. 00] Roy S. Berns, Fred W. Billmeyer, and Max Saltzman. Billmeyer and Saltzman’s Principles of Color Technology. Wiley Interscience, 2000.

[Debevec and Malik 97] Paul E. Debevec and Jitendra Malik. “Recovering High Dynamic Range Radiance Maps from Photographs.” In Proceedings of the 24th Annual Conference on Computer Graphics and Interactive Techniques, SIGGRAPH ’97, pp. 369–378, 1997.

[Gallo et al. 09] O. Gallo, N. Gelfand, W. Chen, M. Tico, and K. Pulli. “Artifact-free High Dynamic Range Imaging.” IEEE International Conference on Computational Photography (ICCP).

[Gupta et al. 13] M. Gupta, D. Iso, and S.K. Nayar. “Fibonacci Exposure Bracketing for High Dynamic Range Imaging.” pp. 1–8.

[Hunt 95] R. W. G. Hunt. The Reproduction of Color. Fountain Press, 1995.

[Larson et al. 97] G. W. Larson, H. Rushmeier, and C. Piatko. “A Visibility Matching Tone Reproduction Operator for High Dynamic Range Scenes.” *IEEE Transactions on Visualization and Computer Graphics* 3:4.

[Li et al. 15] Yuqi Li, Aditi Majumder, Dongming Lu, and Meenakshisundaram Gopi. “Content-Independent Multi-Spectral Display Using Superimposed Projections.” *Computer Graphics Forum.*

[Livingstone and Hubel 02] Margaret Livingstone and David H. Hubel. *Vision and Art : The Biology of Seeing.* Harry N Abrams, 2002.

[Palmer 99] Stephen E. Palmer. *Vision Science.* MIT Press, 1999.

[Reinhard et al. 05] Erik Reinhard, Greg Ward, Sumanta Pattanaik, and Paul Debevec. *High Dynamic Range Imaging: Acquisition, Display, and Image-Based Lighting (The Morgan Kaufmann Series in Computer Graphics).* Morgan Kaufmann Publishers Inc., 2005.

[Seetzen et al. 04] Helge Seetzen, W. Heidrich, W. Stuezlinger, G. Ward, L. Whitehead, M. Trentacoste, A. Ghosh, and A. Vorozcovs. “High Dynamic Range Display Systems.” *ACM Transactions on Graphics (special issue SIGGRAPH).*

[Shogenji et al. 04] R. Shogenji, Y. Kitamura, K. Yamada, S. Miyatake, and J. Tanida. “Multispectral imaging using compact compound optics.” *Opt. Exp.*, p. 16431655.

[Susan 09] Petrescu S. Nanu F. Capata A. Corcoran P. Susanu, G. “RGBW Sensor Array.” *US Patent 2009/0,167,893.*

[Tumblin and Turk 99] J. Tumblin and G. Turk. “Low Curvature Image Simplifiers (LCIS): A Boundary Hierarchy for Detail-Preserving Contrast Reduction.” pp. 83–90.

[Yasuma et al. 10] F. Yasuma, T. Mitsunaga, D. Iso, and S.K. Nayar. “Generalized Assorted Pixel Camera: Post-Capture Control of Resolution, Dynamic Range and Spectrum.” *IEEE Transactions on Image Processing* 99.

## 摘要：你知道这些概念吗？

- 3D 或 2D 设备色域
- Gamma 函数
- 色彩管理
- 色域转换和匹配
- 动态范围
- 适应
- 高动态范围成像
- 多光谱成像

## 练习

- 1. $C_1$ 和 $C_2$ 是具有色度坐标 $(0.33, 0.12)$ 和 $(0.6, 0.3)$ 的颜色。应以什么比例混合这些颜色以生成色度坐标为 $(0.5, 0.24)$ 的颜色 $C_3$？如果 $C_3$ 的强度为 90，则 $C_1$ 和 $C_2$ 的强度是多少？

- 2. 考虑一个线性显示器，其红色、绿色和蓝色原色的色度坐标分别为 $(0.5, 0.4)$、$(0.2, 0.6)$ 和 $(0.1, 0.2)$。红色、绿色和蓝色通道的最大亮度分别为 100、200 和 $80 cd/m^2$。生成将该设备的 RGB 坐标转换为 XYZ 坐标的矩阵。RGB 输入为 $(0.5, 0.75, 0.2)$ 时，该设备产生的颜色的 XYZ 坐标是多少？

- 3. 考虑 CIE XYZ 空间中的两种颜色 $C_1 = (X_1, Y_1, Z_1)$ 和 $C_2 = (X_2, Y_2, Z_2)$。设其色度坐标分别为 $(x_1, y_1)$ 和 $(x_2, y_2)$。
  - (a) 如果 $C_1$ 是纯无彩色，则其三刺激值和色度坐标将满足什么约束？在这种情况下，黑白是否位于 XYZ 空间中从原点到 $C_1$ 的射线上？请证明。
  - (b) 如果 $C_2 = (50, 100, 50)$，则 $(x_2, y_2)$ 的值是多少？
  - (c) $C_2$ 的主波长是多少？
  - (d) 要创建色度坐标为 $(7/24, 10/24)$ 的颜色，$C_1$ 和 $C_2$ 应以什么比例混合？该混合所需的 $C_1$ 的强度和亮度是多少？

- 4. 当我们将蓝色颜料与黄色颜料混合时，我们得到绿色。但当我们将蓝色光投影到黄色光上时，我们得到棕色。你如何解释这种矛盾？

- 5. 考虑具有线性伽马函数的灰度图像。你将如何改变伽马函数以使图像具有更高的对比度？

- 6. 伽马函数的另一个名称是色调映射算子。考虑一个 8 位显示器（每个通道用 8 位整数表示），其色调映射算子为 $i^2$，适用于所有通道，其中 $i$ 为通道输入。考虑亮度、对比度、色彩分辨率、白点和色偏的特性。在以下每种情况下，哪些特性会发生变化？
  - (a) 色调映射算子改为 $i^3$，适用于所有通道。

