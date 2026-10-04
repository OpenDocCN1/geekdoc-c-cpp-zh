

# 使用 R 进行应用时间序列分析

我们的兴趣在于年度数据，在图 1.23a（数据集 ss08_tswage）中，我们绘制了 1749–2008 年的这些年平均值。对该数据建模的问题在过去一个世纪里已被许多研究者研究过。特别是，Yule（1927）提出了 AR 模型来表示数据的受扰动周期性。

图 1.23a 中的太阳黑子数据揭示了一种拟周期性，其中值得注意的是太阳黑子数据在 9 年和 11 年之间。事实上，太阳黑子并非正弦性质，其峰值的变化远大于其谷值的变化（参见 Tong, 1990）。在图 1.23b 中，我们展示了太阳黑子数据的样本自相关。图 1.23c 显示了谱密度，其中我们使用 Parzen 窗口估计 S(f)，M=2\sqrt{n}=32。在图 1.23c 中，我们注意到在大约 $f=0.09$ 处有一个相当尖锐的峰值，表明数据中存在约 11 年的主导周期。也有趣的是，在 $f=0$ 处也存在一个峰值，可能表明存在更长周期或非周期行为。

## 使用 R：图 1.23 所示的图（即时间序列实现、样本自相关和 Parzen 谱密度的图

![](img/41dcbfb9af56fa48895afde322197b0b_58_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_58_1.png)

FIGURE 1.23
Plots related to sunspot data. (a) Annual sunspot numbers. (b) Sample autocorrelations. (c) Parzen window spectral estimator.

## 平稳时间序列

估计) 可以使用 twage 命令 plot.sample.wge 获得（它还将周期图作为第四个图绘制）。参见附录 1B。

### EXAMPLE 1.14: GLOBAL TEMPERATURE DATA

人们对全球变暖的担忧在过去 25 年里引起了极大的关注。感兴趣的数据集提供了平均年温度的度量。其中一个数据集由东英吉利大学气候研究单位与气象局哈德利中心联合收集。图 1.24a 中给出的数据是 1850–2009 年的年度温度信息（基于相对于全球平均值的温度位置）。所绘制的数据（数据 hadley in twage）是温度异常值（即与 1961–1990 年期间平均值的偏差），基于陆地和海洋温度站。在数据集中，很明显在此期间温度有所上升。也有相当大的变化，但没有明显的周期性行为。在图 1.24b 中，我们看到较低滞后的自相关为正，表明例如，今年和明年的年平均温度之间存在相当大的正相关。图 1.24c 中的谱估计器（使用

![](img/41dcbfb9af56fa48895afde322197b0b_59_0.png)

FIGURE 1.24
Plots related to global temperature data. (a) Global temperature data. (b) Sample autocorrelations. (c) Parzen window spectral estimator.

Parzen 窗口平滑样本谱，使用 $M=2\sqrt{n} = 25$ 也表明缺乏周期性行为。$f=0$ 处的峰值表明存在非常长的周期或周期性行为。谱估计器中的较小峰值可能有意义也可能没有意义。

### EXAMPLE 1.15: AIRLINE DATA

图 1.25a（数据集 tswge）是 1949–1960 年国际航空旅行月度总人数（以千计）的自然对数的图。该序列由 Box et al.（2008）研究，并在该书的早期版本中讨论过，通常被分析为季节性时间序列的经典示例。由于航空旅行的季节性，预计存在强烈的季节性模式，例如夏季以及 11 月和 12 月更繁忙。对数据的检查显示夏季旅行更繁忙，12 个月年度模式，以及上升趋势。请注意，12 个月周期似乎不是正弦的，但倾向于“复制”前一年的模式。我们将在第 3 章和第 5 章讨论季节性模型。图 1.25b 显示了样本自相关。对数据中季节性和趋势行为的分析在这里很困难，简单检查这些样本自相关的图对于该分析是不够的。

![](img/41dcbfb9af56fa48895afde322197b0b_60_0.png)

![](img/41dcbfb9af56fa48895afde322197b0b_60_1.png)

FIGURE 1.25
Plots related to the airline data. (a) International airline passengers. (b) Sample autocorrelations. (c) AR spectral estimator.

## 平稳时间序列

图 1.25c 显示了 AR 谱密度估计器（参见第 7.7 节）。请注意零处的功率很高，表明数据中存在强烈的趋势（非周期）分量。此外，在 $f=1/12$ 处的高功率以及 1/12 的谐波，即 $f=i/12, i=2, 3, \dots, 6$ 非常明显。也就是说，数据中 12 个月、6 个月、...、2 个月周期被生动地显示出来。

### EXAMPLE 1.16: BAT ECHOLOCATION SIGNAL

在图 1.26a（数据 *noctula* in twos）中，我们展示了从 Nyctalus 猎蝠回声定位信号中取出的 96 个观测值，采样间隔为 $4 \times 10^{-3}$ s。乍一看，图 1.26a 中的信号似乎是周期性的，其行为类似于图 1.20a 中看到的行为，并且与图 1.23a 中的日落数据 somewhat-similar。然而，样本自相关似乎不寻常，没有像图 1.20b 和 1.23b 中那样的周期性行为。此外，图 1.26c 中谱估计的检查显示没有尖锐峰值，事实上，在 $f=0.15$ 和 $f=0.35$ 之间存在一个宽频带，与一个宽“峰值”相关联。图 1.26c 所示的此类谱被称为扩散峰值，表明信号中的行为并非集中在单一频率及其周围，而是存在一系列频率行为。更仔细地检查图 1.26a

![](img/41dcbfb9af56fa48895afde322197b0b_61_0.png)

**FIGURE 1.26**
Plots related to Nyctalus noctula hunting bat echolocation signal. (a) Echolocation signal. (b) Sample autocorrelations. (c) Parzen window spectral estimator.

显示频率行为随时间变化。更具体地说，周期长度倾向于随时间延长（频率降低）。因此，似乎数据可能是平稳的，因此出现了问题，“如果周期随时间变化，自相关函数或谱密度意味着什么？” 对这种具有时变频率的数据类型的分析将在第 12 章和第 13 章中讨论。

这些和其他时间序列将在未来章节中更详细地研究。以下章节讨论使用自相关和谱密度等工具，以及 AR 模型等模型来正确分析平稳和非平稳时间序列数据。现在，我们只是简要介绍了这些思想，以帮助读者开始理解这些概念。

## 附录 1A: Fourier Series

在定义 1.15 中，我们将离散时间序列 X 的周期图定义为

```
I(f_j) = \hat{f}_j^2 + 2 \sum_{k=1}^{n-1} \hat{f}_k \cos 2\pi f_j k,    (1A.1)
```

f_j 是基频 1/n 的谐波。具体而言，

```
f_j = \frac{\hat{j}}{n}, j=1,...,\frac{n}{2} (if n is even)
= \frac{\hat{j}}{n}, j=1,...,m, (if n is odd and n = 2m+1).
```

值得注意的是，周期图在方程 1A.1 中可以作为数据傅里叶变换模平方的 1/n 倍得到，如方程 1A.2 所示。

```
I(f_j) = \frac{1}{n} \sum_{i=1}^{n} x_i e^{(-2\pi i tj/n)}^2    (1A.2)
```

方程 1A.1 和 1A.2 相等性的证明留作问题 1.20。

周期图的第三种形式涉及傅里叶级数。在本附录中，我们讨论将傅里叶级数拟合到离散时间序列实现 $x_t, t=1, \dots, n$ 的主题，我们假设 $n=2m+1$ 为奇数。也就是说，我们使用有限傅里叶近似 $x_t$

```
$$\sum_{j=1}^{m} \left[ a_j \cos\left(\frac{2\pi jt}{n}\right) + b_j \sin\left(\frac{2\pi jt}{n}\right) \right]$
```

系数 $a_j$ 和 $b_j$ 使用最小二乘法估计，以便找到使

```
$Q = \sum_{t=1}^{n} \left[ x_t - \sum_{j=1}^{m} \left( a_j \cos\left(\frac{2\pi jt}{n}\right) + b_j \sin\left(\frac{2\pi jt}{n}\right) \right) \right]^2 \quad (1A.3)$
```

最小的 $a_j$ 和 $b_j$。使方程 1A.3 中的 $Q$ 最小的 $a_j$ 和 $b_j=1, \dots, m$ 为

```
$a_j = \frac{2}{n} \sum_{t=1}^{n} x_t \cos\left(\frac{2\pi jt}{n}\right) = \frac{2}{n} \sum_{t=1}^{n} (x_t - \bar{x}) \cos\left(\frac{2\pi jt}{n}\right)\nb_j = \frac{2}{n} \sum_{t=1}^{n} x_t \sin\left(\frac{2\pi jt}{n}\right) = \frac{2}{n} \sum_{t=1}^{n} (x_t - \bar{x}) \sin\left(\frac{2\pi jt}{n}\right)$
```

每个表达式中的第二个等式遵循以下事实

```
$$\sum_{t=1}^{n} \cos\left(\frac{2\pi jt}{n}\right) = \sum_{t=1}^{n} \sin\left(\frac{2\pi jt}{n}\right) = 0,$$
```

对于每个 $j$。使用这种术语，周期图的第三种形式由下式给出

```
$III. $I(f_j) = \frac{n}{4}(a_j^2 + b_j^2), \ j=1, \dots, m. \quad (1A.4)$
```

使用 Parseval 等式（参见 Jenkins and Watts, 1968），我们得到

```
$$\sum_{t=1}^{n} (x_t - \bar{x})^2 = \frac{1}{2} \sum_{j=1}^{m} (a_j^2 + b_j^2), \ j=1, \dots, m. \quad (1A.5)$$
```

方程 1A.5 中的结果给出了方差分析分解，显示每个谐波对样本方差的贡献。也就是说，大

