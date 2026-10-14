

![](img/66c45bbed85bb7ba7f7b05dff49b5060_59_0.png)

**图 3.6.** 该图展示了 1D 盒滤波器扩展到 2D 的过程。

size with a value of \(\frac{1}{5}\) at every pixel as shown in **Figure 3.5(c)**. Notice the analog representations of these filters in (d) and (e). Since they look like boxes, these are most commonly referred to as *box filters*.

However, there are multiple ways to maintain the same energy as the \(\delta\) of which only one is to assign the same value at every pixel. Therefore, conceptually, the shape of the filter can change and still remain a blurring filter as long as the support of the kernel increases. It is indeed true that many such blurring filters exist and we will revisit this issue in the next chapter where we will find that though box filter is the easiest to implement, it is not the best for blurring.

Now the next question is how do we extend this blurring filter to 2D. In this case, the energy of the \(\delta\) should be spread around a 2D box around the surrounding of origin. So, the extension of the three pixel 1D box filter to 2D will be a \(3 \times 3\) filter with each value as \(\frac{1}{9}\) and that of the wider box filter will be a \(5 \times 5\) array with each value as \(\frac{1}{25}\) (**Figure 3.6**).

![](img/66c45bbed85bb7ba7f7b05dff49b5060_59_1.png)

**图 3.7.** 卷积的对偶性体现在空间域中两个函数的卷积在频域中是它们频率响应的乘积，反之亦然。这里的 \(F\) 表示将时域函数转换为频域的操作。

## 3.2.1 全通、低通、带通和高通滤波器

有趣的是你会发现盒滤波器通常被称为 *低通滤波器*。为了理解原因，回顾一下 **第 1 章** 中讨论的频域表示可能是有价值的。在本章中我们将非常非正式和直观地理解这一概念，并在下一章中更正式地重新审视它。

![](img/66c45bbed85bb7ba7f7b05dff49b5060_60_0.png)

**图 3.8.** 这展示了全通滤波器的概念。δ 函数的频率响应是一个常数。因此，一般函数与常数相乘后的频率响应不会削减任何频率。由于它通过了所有频率，因此被称为全通滤波器。

让我们再次从 1D 中的 delta 函数开始。这可以被视为原点处的一个非常尖锐的尖峰。现在，直观地说，你会期望 δ 函数的频域表示是什么？记住，形成尖锐特征需要非常高的频率信号。这一事实可能让你相信，像 δ 这样最尖锐的数字函数会涉及所有高频。事实上，可以正式证明，创建 δ 需要所有频率的等强度。因此，δ 函数的频域响应（我们这里只考虑幅度）是一个常数。现在，让我们问一下常数函数的频域响应会是什么，即时域中保持恒定值的函数。很显然可以看出，这种函数由零频率余弦波表示。因此，该常数函数的频域响应在频域中原点处有一个单一值，即频域中的 δ 函数。

你可能注意到了这里的一个有趣模式。时域中的 δ 是频域中的常数，而时域中的常数是频域中的 δ。这真的是巧合吗？事实证明不是！这被称为对偶性，我们将在下一章中更正式地探讨它。但我们将利用这一概念来理解本章中的一些内容。

对偶性的概念产生了一个重要的卷积性质，即如下所示。如果空间域中两个函数 \(a[t]\) 和 \(b[t]\) 的频域响应分别为 \(A[f]\) 和 \(B[f]\)，则它们在时域中的卷积的频域响应由它们的频域响应的乘积给出，反之亦然（图 3.7）。

这为我们理解全通、低通、高通和带通滤波器提供了背景。让我们首先重新审视方程 3.4。我们提到，任何函数 \(x[t]\) 与 delta 的卷积被称为全通系统。让我们看看是否可以用我们刚刚学到的关于对偶性的知识来解释这一点。首先，δ 的频率响应是一个常数。因此，\(x[t] \star \delta[t]\)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_63_0.png)

**图 3.11.** 该图像显示了增大盒滤波器尺寸并与图像卷积的效果。从左到右：原始图像以及与 \(3 \times 3\)、\(5 \times 5\) 和 \(15 \times 15\) 盒滤波器卷积后的同一图像。

Frequencies — essentially everything above f2 where f2 < f1 — are thrown away, thereby creating an even blurrier signal in Figure 3.10(c). Since higher frequencies are thrown away as a result of convolution with box filters while the lower frequencies are passed, these are called low pass filters. However, note that box filters are only one kind of low-pass filter. The shape of the filter need not be an exact box to spread the energy of the delta from a single pixel to multiple ones. For example, a triangular shaped filter can also be used for this purpose. The difference between these filters will be in the way they spread the energy which is defined by their shape. In a box filter, the energy is spread equally to all the pixels while in a triangular filter the amount of the energy reduces from the center towards the periphery. Another important thing to note in this context is that all the frequencies that are passed by the low-pass filter are not passed unchanged. In fact, different frequencies are attenuated differently, with the higher of the passed frequencies getting more severely attenuated. The figures in this chapter focuses on the frequency content (the range of frequencies passed) rather than the exact shape of the frequency response of the filters so that your attention is not distracted from the most important aspect of frequency domain analysis, the frequency content. The exact shape of the frequency response of the filter will only affect the amount of attenuation of the passed frequencies and will be discussed in details in the next chapter.

Now consider this same situation in 2D. Consider an image which is being progressively convolved with filters of larger and larger size (3, 5, 7 and so forth). The images that would be created would be progressively blurrier (Figure 3.11) with the final one being a flat gray colored image where the gray color is given by the average of all the pixels in the original image. In the frequency domain, we know that the cut-off frequency for each of these images will be progressively reducing. In 2D, different frequencies are represented as concentric circles with the length of the radius representing the frequency. Figure 3.12 illustrates the cut-off frequency of low pass filters beyond which all frequencies are blocked. With larger kernel size, this cut-off frequency gets smaller.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_64_0.png)

**图 3.12.** 该图像显示了在频域中与图像卷积时增大盒滤波器尺寸的效果。频率响应被可视化为灰度图像。从左到右：原始图像的频率响应以及与尺寸越来越大的滤波器卷积后的同一图像的频率响应。请注意，截止频率由一个圆表示，超出该圆的每个频率的贡献都为零，因此为黑色。随着滤波器尺寸的增大，该圆的半径减小，表明更多的高频被切除。

### 采样问题

让我们现在考虑对图像进行低通滤波的采样后果。奈奎斯特采样准则指出，采样图像所需的最小采样数是图像中包含的最高频率的两倍。随着图像经过低通滤波，其频率含量会降低（图 3.12 中 \(f3 < f2 < f1\)）。这意味着充分采样低通滤波后图像所需的最小采样数也会下降。这表明低通滤波后的图像可以比原始图像尺寸更小。或者，随着我们逐步增大低通滤波器的尺寸，我们不需要以原始尺寸保存图像，而是可以重新采样并以更小的尺寸存储，只要足够大以采样其中的最高频率即可。

这一特性被用来构建一个由逐步低通滤波的图像组成的金字塔，称为高斯金字塔。为此，我们将原始图像重新采样为 \(2^n \times 2^n\) 的尺寸。这构成了金字塔的第 0 层。将该图像的 \(2 \times 2\) 像素块进行低通滤波以创建下一层层次结构中的单个像素，从而得到一个 \(2^{n-1} \times 2^{n-1}\) 的图像。使用盒滤波器时，这相当于将第 n 层的每个 \(2 \times 2\) 像素块的像素取平均值来创建第 \(n+1\) 层的每个像素。请注意，由于第 \(i+1\) 层的图像是从第 i 层的图像低通滤波得到的，因此较低的分辨率足以采样频率含量较低的该图像。如果逐步继续这一过程，将创建金字塔的 n 个层级，最后一个层级为单个像素，可以被视为 \(2^{n-n} \times 2^{n-n} = 1 \times 1\) 的图像。这在图 3.13 中有所说明。

