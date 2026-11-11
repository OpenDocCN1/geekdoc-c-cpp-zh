**Inline Exercise 18.2:** Consider convolving a grayscale image $f$ with a filter $g$ that's defined by $g(-1, -1) = g(-1, 0) = g(-1, 1) = -1$, $g(1, -1) = g(1, 0) = g(1, 1) = 1$, and $g(0, 0)$ is 0 otherwise.
(a) Draw a plot of $g$.
(b) Describe intuitively where $f * g$ will be negative, positive, and zero. You might want to start out with some simple examples for $f$, like an all-gray image, or an image that's white on its bottom half and black on the top, or white on the left half and black on the right, etc. Then generalize.

We've defined convolution for two continuous functions (i.e., functions defined on $\mathbf{R}$) and for two discrete functions (i.e., defined on $\mathbf{Z}$). There's a third class of convolution that comes up in graphics: the discrete-continuum convolution. A familiar instance of this is displayed on a grayscale LCD monitor. Recall that for this chapter, the display pixel $(i, j)$ is a small box *centered* at $(i, j)$. Figure 18.19 shows the result of displaying a $2 \times 2$ image $f$ (shown as a stem plot) with a "box" function $b$ defined on $\mathbf{R}^2$ to produce a piecewise constant function on $\mathbf{R}^2$ representing emitted light intensity.

The emitted light at location $(x, y)$ is given by

```
$$ light(x, y) = f(i, j)box(x - i, y - j). \quad (18.12) $$
```

This doesn't quite look like a convolution, because there's no summation. But we can insert the summation without changing anything:

```
$$ light(x, y) = \sum_{i, j} f(i, j)box(x - i, y - j). \quad (18.13) $$
```

There's no change because the box function is zero outside the unit box. In the early days of graphics, when CRT displays were common, turning on a single pixel didn't produce a little square of light, it produced a bright spot of light whose intensity faded off gradually with distance. That meant that turning on pixel $(4, 7)$ might cause a tiny bit of light to appear even at the area of the display we'd normally associate with coordinates $(12, 23)$, for instance, or anywhere else. In that case, the summation in the formula for the light at position $(x, y)$ was essential.

The general definition for the convolution of a discrete function $f : \mathbf{Z} \rightarrow \mathbf{R}$ and a continuum function $g : \mathbf{R} \rightarrow \mathbf{R}$ is

```
$$ (f * g)(x) = \sum_{i = -\infty}^{\infty} f(i)g(x - i) \quad \text{for } x \in \mathbf{R}. \quad (18.14) $$
```

The result is a continuum function. We leave it to you to define continuous-discrete convolution, and to extend both definitions to the plane.

# 18.4 Properties of Convolution

As mentioned in Section 18.2, convolution has several nice mathematical properties. First, for all forms of convolution (discrete, continuous, or mixed) it's linear in each factor, that is,

```
$$ (f_1 + c f_2) * g = (f_1 * g) + c(f_2 * g) \text{ for any } c \in \mathbf{R}, \text{ and } \quad (18.15) $$
$$ f * (g_1 + c g_2) = (f * g_1) + c(f * g_2). \quad (18.16) $$
```

![](bbox=[0.7, 0.13, 0.97, 0.31])

![](bbox=[0.7, 0.32, 0.97, 0.48])

![](bbox=[0.7, 0.49, 0.97, 0.65])

![](bbox=[0.7, 0.68, 0.97, 0.78])

*Figure 18.19: The values in a $2 \times 2$ grayscale image are convolved with a box function to get a piecewise constant function on a $2 \times 2$ square.*