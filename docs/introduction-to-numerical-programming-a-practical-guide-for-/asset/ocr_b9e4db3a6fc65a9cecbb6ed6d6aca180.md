The completeness and orthonormalization guarantee that any function $f \in \mathcal{L}_2(S_1)$ can be expanded uniquely in a converging Fourier series with respect to the spherical harmonics:

```
$$f(\theta,\varphi)=\sum_{l=0}^{\infty}\sum_{m=-l}^{l}a_{lm}Y_{lm}(\theta,\varphi).\tag{5.38}$$
```

The associated Legendre functions $P_l^m(x)$ satisfy the differential equation

```
$$\left(1-x^2\right)\frac{d^2P_l^m}{dx^2}-2x\frac{dP_l^m}{dx}+\left[l(l+1)-\frac{m^2}{1-x^2}\right]P_l^m=0,\tag{5.39}$$
```

which can be shown to result by replacing the spherical harmonics (5.35) in Equation 5.34 and noting $x=\cos\theta$. For $m\ge0$, the associated Legendre functions can be expressed in terms of the derivatives of the basic Legendre polynomials $P_l(x)$:

```
$$P_l^m(x)=(-1)^m\left(1-x^2\right)^{m/2}\frac{d^m}{dx^m}P_l(x).\tag{5.40}$$
```

The corresponding orthogonality relation reads:

```
$$\int_{-1}^{1}P_{l'}^m(x)P_l^m(x)dx=\frac{2}{(2l+1)}\frac{(l+m)!}{(l-m)!}\delta_{l'l}.\tag{5.41}$$
```

For negative upper indexes, the convenient way to evaluate the associated Legendre functions is provided by the relation:

```
$$P_l^{-m}(x)=(-1)^m\frac{(l-m)!}{(l+m)!}P_l^m(x),\quad m=0,1,\dots,l.\tag{5.42}$$
```

The associated Legendre functions form a complete orthonormal basis set in the space $\mathcal{L}_2[-1,1]$ of the square integrable functions defined on interval $[-1,1]$, having as a direct consequence the fact that any function $f\in\mathcal{L}_2[-1,1]$ may be uniquely expanded in a converging Fourier series in terms of these functions:

```
$$f(x)=\sum_{l=0}^{\infty}\sum_{m=-l}^{l}a_{lm}P_l^m(x).\tag{5.43}$$
```

The efficient and stable method to evaluate the associated Legendre functions is based on the recurrence relation with respect to their lower order:

```
$$(i-m)P_i^m(x)=(2i-1)xP_{i-1}^m(x)-(i+m-1)P_{i-2}^m(x).\tag{5.44}$$
```

The complication arisen from the necessity of starting the recurrence from two values corresponding to functions of given superior index $m$ can be overcome by considering the particularly simple expressions of $P_{m-1}^m(x)$ and $P_m^m(x)$ resulting from their definition (5.40). Indeed, by setting $l=m-1$, we have

```
$$P_{m-1}^m=0,\tag{5.45}$$
```