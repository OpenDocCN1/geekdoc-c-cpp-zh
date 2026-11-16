![](bbox=[0.092, 0.118, 0.882, 0.332])

Figure 6.6 (left-to-right) Using a random color map to show noise: A cartoon scanned by a grayscale camera, a noisy grayscale image, and an angiogram.

many times in previous chapters. The difference here is that the weights of the filter vary according to the image data where they are applied. You may have encountered similar systems in your signal processing courses, where you encountered “linear, time-invariant systems,” and learned about the Fourier transform. Here, in the signal processing analogy, this would be a time-variant system. Of course, in image processing, we think of space-variant rather than time-variant, but the mathematics is the same.

The idea is this: at every point in the image, we compute a weighted sum of the neighbors of that point, just as we do with a regular kernel operator. However, if the neighbor is far away, we do not consider it very strongly, and similarly, if the brightness of the neighbor is very different from the center pixel, it is also not strongly considered. Paris [6.22] summarizes it nicely, saying “two pixels are close to each other not only if they occupy nearby spatial locations but also if they have some similarity in the photometric range.” This is accomplished at a point \(\mathbf{x} = [x, y]\) by computing a new value for \(f(\mathbf{x})\) using

```
\(f(\mathbf{x}) = \sum_i f(\mathbf{x}_i) G_{\sigma_s}(\|\mathbf{x} - \mathbf{x}_i\|) G_{\sigma_r}(f(\mathbf{x}) - f(\mathbf{x}_i)),\) (6.3)
```

where \(G_\sigma(t)\) is a 2D Gaussian with width parameter (standard deviation) \(\sigma\), and

```
\(G_\sigma(t) = \frac{1}{2\pi\sigma} \exp\left(-\frac{t^2}{2\sigma^2}\right).\)
```

The norm \(\|.\|\) denotes the 2-norm, the Euclidean distance from point \(\mathbf{x}\) to each of the neighboring points \(\mathbf{x}_i\).

The product of the two Gaussians will be small if either is small, that is, if the point \(\mathbf{x}_i\) is far from \(\mathbf{x}\), or if the two points differ significantly in brightness. The two \(\sigma\) parameters control what is considered a reasonable distance in the image or difference in brightness for a particular application.

Equation 6.3 adds up weights that are data dependent, and therefore must be normalized for the result to make sense. Normalization proceeds by computing a normalization term

```
\(Z = \sum_i G_{\sigma_s}(\|\mathbf{x} - \mathbf{x}_i\|) G_{\sigma_r}(f(\mathbf{x}) - f(\mathbf{x}_i)),\)
```