
In Chapter 14 we saw how to import a PGM or PPM image as a matrix of pixels. In Chapter 13 we saw how to apply the Haar transform to express a matrix in terms of the wavelet basis. In this chapter we bring these techniques to their natural construction by applying the wavelet transform to an image. This decomposes the image into a sum of progressively finer wavelets. The very fine wavelets tend to have small coefficients because they measure the differences between nearby pixels. In an ordinary photograph, say of a person's face, the differences between adjacent pixels are small, in general, because the texture and color vary smoothly. There are exceptions: for instance, a finely knitted sweater or distinctly hair may exhibit significant variations even at the pixel scale. In any case, even in images containing textures, the coefficients of the finer wavelets tend to be very small. Figure 15.1 shows a $512 \times 512$ grayscale image on the right. The two graphs on the left show the absolute values of the image's wavelet coefficients, sorted in decreasing order. Thus the horizontal axis enumerates these coefficients (from 1 to $512 \times 512 = 262,144$) and the vertical axis is their magnitudes. The graph on the top shows the full range of pixels. Because essentially all the coefficients are practically zero, and thus the graph coincides with the horizontal axis. If you look *closely*, you may discern a slight rounding near the origin. That is all there is to see of the graph. In the bottom graph I have expanded the horizontal range 1 to 80 to zoom up to the details near the origin. The very first coefficient is approximately 15. The next few are approximately 42, 41, 21, 14, and they drop rapidly after that. This raises an intriguing question: what if we keep the first few thousand wavelet coefficients and discard the rest? Reconstructing the image from the retained coefficients should yield a relatively faithful representation of the image since the discarded ones are too small to matter.

In this chapter we investigate this. Experiment experimenting with images of human faces, we find that retaining around 5 percent of the largest wavelet coefficients suffices to recreate an image which is hardly distinguishable from the original. This observation has practical implications. For one, we may save a good deal of storage space by storing a small fraction of the wavelet coefficients instead of a full image. More importantly, if we are willing to accept a slightly deteriorated image, we may save substantially in network transmission time and broadcast bandwidth if we send only the significant wavelet coefficients. All that is needed is a wavelet transformation and truncation at the sending end and an inverse wavelet transformation to the receiving end. Most videos that you watch on the Internet are brought to you this way.

This program reads a PGM or PPM image, applies the Haar transform and discards as many of the smallest wavelet coefficients as possible, keeping the truncation error below a prescribed threshold. Then it reconstructs the image from the remaining wavelets and writes it to a file. Since the wavelet we developed in Chapter 13 work with matrices whose dimensions are powers of 2, this chapter handles images whose dimensions are powers of 2. Images of arbitrary size may be cropped or padded to make them conform to this requirement.

**Remark 15.1.** The word "discard" can be somewhat ambiguous in this context, so let us clarify. By "discarding a coefficient" I mean setting it to zero. Afterward, when the image is reconstructed as a sum of the products of the coefficients and the corresponding wavelets, a zeroed coefficient does not contribute to the sum; therefore in effect it is "discarded".

**Remark 15.2.** Applying the wavelet transform to an image's matrix and discarding the small entries leaves us with a *sparse matrix*, that is, a matrix whose vast majority of entries are zero. The sparse matrix storage techniques of Chapter 11 may be applied profitably to store such truncated images, but I will not pursue that issue. You may find it instructive to explore the idea on your own.

## 15.2 The truncation error in a grayscale image

We saw in Chapter 13 that the wavelet bases are orthogonal sets; therefore, if `a = (a_{ij})` are the entries of a grayscale image's wavelet coefficients, `||a|| = (sum a_{ij}^2)^{1/2}` is a norm on the space of grayscale images. Our program receives a grayscale image and a user-specified relative error `e_rel`. It proceeds to determine the cut-off threshold `t` so that

```
abs(t)/||a|| < e_rel
```

The most obvious way of finding `t` is through the bisection algorithm (see, [33]). Here is how:

- Sweep through the matrix `a` to find the largest and smallest values of `|a_{ij}|`. Call them `max` and `min`. While you are at it, also compute `||a||`.

- The cut-off threshold `t` lies somewhere in the interval `[min, max]`. As an initial guess, pick `t` at the midpoint, that is, `t = (max+min)/2`.

- Evaluate the truncation error `abs(t) = (sum a_{ij}^2)^{1/2}` corresponding to that value.

- There are three cases:

  - (a) `abs(t) = e_rel`: We have found the right `t`. Stop.

  - (b) `abs(t) > e_rel`: We are truncating too much. Set `max = t`, and go to step 2.

  - (c) `abs(t) < e_rel`: We are truncating too little. Set `min = t`, and go to step 2.

In each iteration unfortunately, chances that the criterion will never terminate. The problem lies in the stopping criterion in 4(a). There are actually two problems with floating point numbers for equality is inherently problematic since most numbers have no representation exactly. A minuscule floating point rounding here and may throw off the equality. Second, *even in the base* of floating point rounding, we don't expect the equality `abs(t) = e_rel` ever to be satisfied in general. The `abs(t)` is computed as a discrete sum of terms. Adding or taking an extra term is likely to move the sum from just below `e_rel` to just above it.

the northwest to the southeast is given by

$$D_l=\{(i,j): \quad i=0, \dots, b-1, \quad j=i(w-1)/(b-1)\}$$

Observe that when `i=0`, we get `j=0`, and when `i=b-1`, we get `j=w-1`, as expected. Note, however, since `i, b,` and `w` are integers, the proper `C` encoding of the formula is

```c
int j = 0.5 + (double)i*(w-1)/(h-1);
```

You figure out how to do the other diagonal. See Part 14.4 for an explanation of the extra 0.5.

**Figure 15.1:** On the right a $512 \times 512$ grayscale image. The graphs on the left show the absolute values of the image's wavelet coefficients, sorted in decreasing order. The upper graph shows all of the $512 \times 512 = 262,144$ coefficients, while the lower graph zooms into the first 80. There is hardly visible in the upper graph because the points coincide with the coordinate axes. In the zoomed graph we see the largest coefficient, which is approximately 15, as an isolated dot at the top of the vertical axis. The next few are approximately 42, 41, 21, and 14. *Photograph courtesy of Stockhaus*

^47 Actually the image that you see in the book has been reduced to fit the page. The actual image I analyzed was $512 \times 512$.

步骤，因此如果该长度小于图像范数的一个极小比例，则停止，即满足 `max-min < epsilon||a||`，并根据 `epsilon` 任意设置为一个较小的值，例如 `10^{-6}`。总而言之，将步骤 4(a) 中的停止条件更改为：

`4(a)': 如果 max-min < epsilon||a|| 则停止`

**备注 15.3。** 尽管定义了范数和绝对值倒平方根，但在上述描述的算法中完全不需要计算根号。例如，条件 `e_abs(t) > ||\hat{a}||rel` 等于 `e_abs(t)^2 > ||a||^2_rel`，这不涉及任何根号。

## 15.3 彩色图像中的截断误差

在第 14 章中，我们将一个 PPM 图像编码为图像红、绿、蓝强度的叠加。因此，我们可以对这三个矩阵中的每一个应用哈尔变换，根据预设的相对误差 `epsilon_rel` 对其进行截断，并从剩余的小波系数集合中重建近似图像。相应的，颜色系数没有带来新的挑战，但有一个细微的问题需要考虑。
