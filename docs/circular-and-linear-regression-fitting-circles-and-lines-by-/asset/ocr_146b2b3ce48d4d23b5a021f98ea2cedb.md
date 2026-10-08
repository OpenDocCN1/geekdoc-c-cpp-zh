These requirements affect the very classes of nonlinear models used in each case.

For example, one may fit polynomials

```
$y=a_{0}+a_{1}x+\cdots+a_{k}x^{k}$
```

to observed points, which is common in the EIV context [79, 140]. Scaling of variables $S_{\alpha, \beta}$, cf. Section 1.3, transforms one polynomial to another, so the class of polynomial remains conveniently invariant.

![](bbox=[0.2, 0.24, 0.8, 0.36])

Figure 1.11 The graph of an explicit nonlinear function $y=g(x)$ (left). After rotation, the same curve (right) does not represent any explicit function.

However, a rotation $R_{\theta}$ of the coordinate plane transforms a polynomial to a different function; it becomes an implicit polynomial curve, which may not even allow an explicit representation $y=g(x)$. Thus explicit polynomials are not suited for orthogonal (geometric) fitting. The same applies to any other class of nonlinear explicit functions $y=g(x)$: the graph of a nonlinear function can always be rotated so that the resulting curve does not represent any explicit functional relation; see Fig. 1.11.

A natural class of models that remain invariant under rotations and translations consists of implicit polynomials of a certain degree $k \geq 1$. Polynomials of degree $k=1$ are given by equation

```
$Ax+By+C=0,$
```

which represents all straight lines on the plane (including vertical and horizontal lines). Polynomials of degree $k=2$ are given by equation

```
$Ax^{2}+By^{2}+Cxy+Dx+Ey+F=0,$
```

which represents all conic sections: ellipses, hyperbolas, and parabolas, in addition to straight lines. This class is large enough to cover a vast majority of the existing applications in computer vision and pattern recognition.

Implicit polynomials of higher degree $k \geq 3$ are occasionally used to describe more complex objects, see examples in [150, 176] where polynomials of degree $k=3, 4$, and even $k=6$, are mentioned. But the use of polynomials