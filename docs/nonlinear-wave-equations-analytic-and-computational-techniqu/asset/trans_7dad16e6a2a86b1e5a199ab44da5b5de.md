

**图3.** 重复图2的计算，但在构建矩阵时不施加零模式滤波器。\(n=20\)的解已被\(n=100\)的第二个实例所取代。（左上和底部）在300位精度下，\(\widehat{G_n(f)}\)几乎完全被舍入误差破坏。（右上）在600位精度下，舍入误差被充分抑制以获得准确结果。误差在\(k=\pm M/2\)附近最大，并随着\(n\)的增加向内传播。
确实以超指数方式增长，但抵消足够强，使得\(\widehat{G_n(f)}\)保持相当平坦。因此，对于大的\(n\)，\(\|\widehat{G_n(\varepsilon f)}\|_F\)像\(\varepsilon^n\)一样衰减，即使\(\|\widehat{A_n(\varepsilon f)}\|_F\)对于任何正\(\varepsilon\)最终停止衰减。

**j = 10, n = 10**　　**j = 10, n = 30**　　**j = 10, n = 100**

![](img/c92a9d81ba7f671c83a4c600d27389fb_201_0.png)

**图4.** 对于示例2，绘制了\(\widehat{A_n(f)}\)和\(\widehat{G_n(f)}\)第\(j=10\)列矩阵元素的幅度，其中\(n=10,30,100\)。对于较小的\(n\)，\(\widehat{G_n(f)}_{kj}\)的幅度与\(\widehat{A_n(f)}_{kj}\)相似，表明几乎没有发生抵消。当\(n\)达到100时，对于典型的\(j,k\)值，\(\widehat{A_n(f)}_{kj}\)的前90位数字已在递推(3.14)中被消去，从而得到\(\widehat{G_n(f)}_{kj}\)。

![](img/c92a9d81ba7f671c83a4c600d27389fb_202_0.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_202_1.png)

**图5.** 对于示例3，绘制了\(\widehat{A_n(f)}\)和\(\widehat{G_n(f)}\)第10列矩阵元素的幅度，其中\(n=10\)和150。必须选择相当大的\(M\)（\(M=24576\)）以防止在\(n=150\)之前误差向内传播到\(k=0\)。注意，当\(n=150\)时，对于该列，\(\widehat{A_n(f)}\)的超过250位前导数字相消以形成\(\widehat{G_n(f)}\)。

除了直观确认舍入误差没有破坏小\(|k|\)时的\(\widehat{G_n(f)}_{jk}\)（如图3–5所示），我们还通过检查每个\(\widehat{G_n(f)}\)的自伴性来验证结果。这是通过测量

\[
r_n=\frac{\max_{j,k\in\mathcal K}\left|\widehat{G_n(f)}_{kj}-\overline{\widehat{G_n(f)}_{jk}}\right|}{\|\widehat{G_n(f)}\|_F},\qquad \mathcal K=\{k:|k|<K/2\}. \tag{3.22}
\]

实现的。在图6中，我们绘制了三个示例的\(r_n\)随\(n\)的变化。注意，在示例1的无滤波情况下，300位精度不足以避免\(\widehat{G_n(f)}\)对称性中的\(O(1)\)误差，而600位精度至少给出90位正确数字。这与图3的结果一致，其中左上面板中信号与噪声几乎无法区分，而在右上面板中信号则高出许多个数量级。事后看来，1500位精度对示例3而言是多余的，因为当\(n=150\)时，\(\widehat{G_n(f)}\)的对称性误差仍低于\(10^{-200}\)。DNO展开正确性的进一步验证将在下一节给出，届时将在一个已知解的情况下用它来计算\(G(\eta)\mathcal{D}\)。

**示例1**　　**示例2**　　**示例3**

![](img/c92a9d81ba7f671c83a4c600d27389fb_203_0.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_203_1.png)

![](img/c92a9d81ba7f671c83a4c600d27389fb_203_2.png)

**图6.** 矩阵\(\widehat{G_n(f)}\)中对称性误差随\(n\)的变化图。虽然对数据进行滤波能显著改善带限情形，但更重要的因素是底层浮点运算的精度。

### 3.2. 说明AFM方法成功与失败的示例

在本节中，我们给出的示例表明，即使对于任意小振幅的带限波剖面\(\eta\)，系统(2.5)–(2.6)（将其中的和理解为无穷级数）也可能无法为某类狄利克雷数据产生诺依曼数据，该类数据包括实解析函数，无论计算中使用多少位精度。

AFM和AFM*方法都涉及作用于未知诺依曼数据的线性算子。在本节中，我们研究这些线性算子截断的奇异值分解（SVD）。通过对列进行过采样，我们获得了(2.7)中底层拟矩阵\(A\)和\(B\)（其列为连续函数）的SVD的更好近似。这引出了AFM/AFM*方法的正则化版本，其中最简单的版本（无伪逆截断）等价于在尝试使用基函数\(e^{ikx}\cosh(k(\eta(x)+h))\)表示\(\mathcal{D}(x)\)或\(\mathcal{N}(x)\)之前，先对它们执行Gram-Schmidt正交化。即使对于\(\mathcal{D}(x)\)不存在形如(2.5)的级数，正则化方法也能使这些方法得以使用。

我们现在构造一个不存在这种级数的函数\(\mathcal{D}(x)\)。考虑函数

\[
\varphi(x,y)=\frac{1}{2}\operatorname{Im}\left\{\cot\left(\frac{x+iy}{2}\right)-\cot\left(\frac{x+iy+2ih}{2}\right)\right\}. \tag{3.23}
\]

它在\(x\)方向是\(2\pi\)-周期的，并且在集合\((2\pi\mathbb{Z})\times\{0,-2h\}\)之外的所有\(x,y\)上是调和的。此外，\(\varphi(x,-h-y)=\varphi(x,-h+y)\)，因此对所有\(x\)有\(\varphi_y(x,-h)=0\)。

在\(y=-h\)处求值，我们得到

\[
\varphi(x,-h)=\frac{\sinh h}{\cosh h-\cos x}=1+2\sum_{k=1}^{\infty} e^{-kh}\cos kx=\sum_{k=-\infty}^{\infty} e^{-|k|h}e^{ikx}.
\]

对于\(-2h<y<0\)范围内的\(y\)值，我们还可以写出

\[
\varphi(x,y)=1+2\sum_{k=1}^{\infty} e^{-kh}\cosh(ky+kh)\cos kx
=1+\sum_{k=1}^{\infty}\left(e^{ky}+e^{-k(y+2h)}\right)\cos kx, \qquad (-2h<y<0). \tag{3.24}
\]

在形式(3.23)中，\(\varphi\)除极点外表现良好。然而，AFM公式基于通过级数(3.24)表示\(\mathcal{D}\)，而该级数对于\(y\ge 0\)是发散的。因此，我们预期对于延伸到\(y=0\)上方的波剖面\(\eta(x)\)会出现问题。

说明这些困难的最简单示例是无限深度情形，其中

\[
\eta(x)=-\varepsilon\cos(x). \tag{3.25}
\]

在(2.7)中引入权重\(w_k=\cosh(k(\eta_{\max}+h))\)，并取\(h\to\infty\)的极限，系统(2.4)变为

\[
\int_0^L e^{|k|(\eta-\eta_{\max})} e^{-ikx}\mathcal{N}(x)\,dx
=
\int_0^L -i\operatorname{sgn}(k)e^{|k|(\eta-\eta_{\max})} e^{-ikx}\partial_x\mathcal{D}(x)\,dx, \tag{3.26}
\]

其中\(\eta_{\max}=\max_{0\le x\le 2\pi}\eta(x)=\varepsilon\)。类似地，(2.5)和(2.6)变为

\[
\sum_k c_k e^{|k|(\eta-\eta_{\max})} e^{ikx} = \mathcal{D}, \tag{3.27}
\]

\[
\mathcal{N} = (-i\partial_x)\sum_k c_k \operatorname{sgn}(k) e^{|k|(\eta-\eta_{\max})} e^{ikx}. \tag{3.28}
\]

在我们的情形中，在(3.23)中使用\(\cot\frac{x+iy}{2}=\frac{\sin x-i\sinh y}{\cosh y-\cos x}\)，我们有

\[
\varphi(x,y)=\frac{1}{2}\left(-\frac{\sinh y}{\cosh y-\cos x}+1\right),
\qquad
\mathcal{D}(x)=\frac{1}{2}\left(\frac{\sinh(\varepsilon\cos x)}{\cosh(\varepsilon\cos x)-\cos x}+1\right), \tag{3.29}
\]

\[
\mathcal{N}(x)=\varphi_y-\eta_x\varphi_x
=\frac{\cosh(\varepsilon\cos x)\cos x-1+\varepsilon\sin^2 x\,\sinh(\varepsilon\cos x)}{2(\cosh(\varepsilon\cos x)-\cos x)^2}.
\]

由于\(\eta\)在\(x\in2\pi\mathbb{Z}\)处下探至极点之下，\(\varphi\)在\(-\infty<y<\eta(x)\)上是调和的。此外，\(\mathcal{D}(x)=\varphi(x,\eta(x))\)是实解析的且是\(2\pi\)-周期的。尽管如此，在整个区间\(0\le x\le2\pi\)上，不存在(3.27)的有效解。从(3.24)中，我们看到系数

\[
c_k=
\begin{cases}
1, & k=0,\\
\frac{1}{2} e^{|k|\eta_{\max}}, & k\ne 0,
\end{cases} \tag{3.30}
\]

在\(\{x:\eta(x)<0\}\)上有效，但在其他地方无效；见图7。

![](img/c92a9d81ba7f671c83a4c600d27389fb_205_0.png)

**图7.** 对于\(\eta(x)=-\varepsilon\cos x\)，\(\varepsilon=0.5\)，比较\(\mathcal{D}\)和\(\mathcal{N}\)的级数表示(3.27)、(3.28)、(3.30)（蓝色曲线）与精确公式(3.29)（红色标记）。级数在\(|k|=64\)处截断，结果在128个网格点上绘制。使用中心有限差分来计算(3.28)中的导数。正如所料，级数在\(\frac{\pi}{2}\le x\le\frac{3\pi}{2}\)处发散，此时\(\eta(x)\ge0\)。

仍然存在这样的可能性：对于任意给定的容差，可以选择\(c_k\)使得(3.27)在指定容差内近似满足。换句话说，左边不再被视为级数，而是被视为可以任意精度逼近\(\mathcal{D}\)的基函数的有限线性组合。为了提高精度，可能不仅要增加更多项，还需要改变所有系数\(c_k\)。为了探索这种可能性，我们构造\(M\times(K-1)\)矩阵\(A\)和\(B\)，其元素为

\[
A_{jk}=\frac{1}{M}\exp(|k|[\eta(x_j)-\eta_{\max}]) e^{ikx_j},\qquad
B_{jk}=i\operatorname{sgn}(k)A_{jk}, \tag{3.31}
\]

其中\(-K/2<k<K/2\)，\(x_j=2\pi j/M\)，且\(M\ge K\)。然后我们计算奇异值分解\(A=USV^*\)，其中\(S\)和\(V\)为方阵，\(U\)的维度为\(M\times(K-1)\)，并计算

\[
\mathcal{N} = U \operatorname{pinv}(S) V^* B^* \partial_x \mathcal{D}, \qquad \mathrm{(AFM)}, \tag{3.32}
\]

\[
\mathcal{N} = -\partial_x B V \operatorname{pinv}(S) U^* \mathcal{D}, \qquad \mathrm{(AFM^*)}. \tag{3.33}
\]

这里\(\partial_x\)通过FFT以谱方式计算（无滤波器）。此处的想法是，对(2.7)中\(A\)和\(B\)的每一列进行足够多的点采样，使得对(3.31)中所得矩阵\(A\)计算SVD，等价于对(2.7)中拟矩阵\(A\)（其列为连续的\(L^2\)函数）计算SVD（除了在若干位置有\(\sqrt{M}\)的缩放）：

\[
A=USV^*, \qquad U:\mathbb{C}^{K-1}\to L^2, \qquad S:\mathbb{C}^{K-1}\to\mathbb{C}^{K-1}, \qquad V:\mathbb{C}^{K-1}\to\mathbb{C}^{K-1}. \tag{3.34}
\]

这里\(A\)已被截断为有\(K-1\)列，\(U\)和\(V\)是酉矩阵，\(S\)是对角矩阵且对角元素为正且递减，\(L^2\)配备内积\(\langle f,g\rangle=\frac{1}{2\pi}\int_0^{2\pi} f\bar g\,dx\)以避免在其他地方出现\(\sqrt{2\pi}\)因子。\(U\)的列构成\(A\)的列张成空间的一组标准正交基。一旦达到足够的网格分辨率，在\(M\)个配置点上逼近\(\mathcal{D}\)和\(\mathcal{N}\)，就可以利用三角多项式在网格点之间插值，从而在整个\((0,2\pi)\)上获得精确的逼近。矩阵形式的\(U\)的列可以看作是(3.34)中拟矩阵\(U\)的列的采样版本，相差一个\(\sqrt{M}\)因子。对于较小的\(M\)值，三角插值变得不太精确，并且误差在除以小奇异值时可能被显著放大。我们注意到，如果将(3.32)和(3.33)中的伪逆替换为逆，则可以使用QR分解代替SVD来获得\(A\)的列张成空间的标准正交基\(U\)。这在正则化AFM/AFM*方法时失去了一些灵活性，但计算成本更低，并且具有优势：当\(K\)增大时，前导基函数不会改变。当列被充分采样时，这种QR方法等价于Gram-Schmidt正交化。

