![](bbox=[0.14, 0.11, 0.64, 0.43])

*Figure 36.13: The points in (x, z bufferValue) space that are exactly representable under fixed-point, reverse-mapped fixed-point, and floating-point schemes. Fixed-point representations result in wildly varying depth precision with respect to screen-space x (or y).*

topic. We summarize the basic ideas of the common mappings here and show Figures 36.13 and 36.14 by them to give a sense of the impact of representation on precision throughout the frustum.

Following (arbitrary) OpenGL conventions, for the following definitions let $z$ be the position on the camera-space $z$-axis of the point coloring the sample. It is always a negative value. Let the far and near clipping planes be at $z_f = -f$ and $z_n = -n$.

# **36.3.1.1 Hyperbolic**

The classic graphics choice describes a hyperbolically scaled normalized value arising from a projection matrix. This is typically called the **z-buffer** because it stores the $z$-component of points after multiplication by an API-specified perspective projection matrix and homogeneous division. This representation is also known as a **warped** $z$-buffer because it distorts world-space distances.

The OpenGL convention maps $-n$ to $0$, $-f$ to $1$, and values in between hyperbolically by

```
$$ z \rightarrow \frac{f+n}{f-n} + \frac{2fn}{f-n} \frac{1}{z} \quad (36.1) $$
```

Direct3D maps to the interval $[-1, 1]$ by

```
$$ z \rightarrow \frac{f}{n-f} - \frac{fn}{n-f} \frac{1}{z} \quad (36.2) $$
```