**Main term.** The main term is

```
$f_0 = \bar{uu} - \bar{u}^2$
$\quad = s_{xx} \cos^2 \varphi + 2 s_{xy} \cos \varphi \sin \varphi + s_{yy} \sin^2 \varphi,$
```

where $s_{xx}$, $s_{xy}$, $s_{yy}$ are the components of the scatter matrix $\mathbf{S}$ introduced in (1.5). In matrix form, we have

```
$f_0 = \mathbf{A}^{T} \mathbf{S} \mathbf{A}$,
```

where $\mathbf{A} = (\cos \varphi, \sin \varphi)^T$, again as in Section 2.3, so we can use the results of that section.

Let $0 \leq \lambda_1 \leq \lambda_2$ denote the eigenvalues of $\mathbf{S}$ and $\mathbf{A}_1$, and $\mathbf{A}_2$ the corresponding eigenvectors. If $\lambda_1 = \lambda_2$, then $f_0$ (as a function of $\varphi$) is constant, but this only occurs when the data set admits infinitely many orthogonal fitting lines (Section 2.3). This constitutes an exceptional event (to which our theorem does not apply).

Setting the exceptional case aside, we assume that $\lambda_1 < \lambda_2$. Then $f_0$ is a nonconstant function of $\varphi$ that has two properties:

+   (a) $f_0(\varphi)$ is a periodic function with period $\pi$;

+   (b) $f_0(\varphi)$ takes values in the interval $[\lambda_1, \lambda_2]$; its minimum value is $\lambda_1$ taken on $\mathbf{A} = \mathbf{A}_1$ and its maximum value is $\lambda_2$ taken on $\mathbf{A} = \mathbf{A}_2$.

See Fig. 3.11. By the way, the boundedness of $f_0$ demonstrates that $\mathscr{F}(a,b)$ is a bounded function, as we have mentioned earlier.

Since $f_0$ has period $\pi$, it takes its minimum on the interval $[0, 2\pi]$ twice: at a point $\varphi_1$ corresponding to the vector $\mathbf{A}_1$ and at $\varphi_1 + \pi$ corresponding to the opposite vector $-\mathbf{A}_1$. Thus there are two valleys on the graph of $\mathscr{F}$, they stretch in opposite directions ($\mathbf{A}_1$ and $-\mathbf{A}_1$); both valleys are parallel to the vector $\mathbf{A}_1$, i.e., they are orthogonal to the best fitting line (as $\varphi$ is the direction of its normal, see Section 2.1).

**Second order term.** To examine the declination (direction of decrease) of those valleys, we need to analyze the behavior of the function $\mathscr{F}$ in their bottoms, which due to (3.19) is given by

```
$\frac{1}{n} \mathscr{F} = \lambda_1 + f_1(\varphi)\delta + \ell(\delta^2)$ $\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad$ (3.20)
```

with $\varphi = \varphi_1$ for one valley and $\varphi = \varphi_1 + \pi$ for the other valley.

To simplify our formulas, we assume that the coordinate system is chosen so that its origin coincides with the centroid of the data, i.e., $\bar{x} = \bar{y} = 0$. In that case also $\bar{u} = \bar{v} = 0$, and we arrive at

```
$f_1(\varphi) = -\bar{uvv}$
$\quad = -\frac{\overline{xvv}}{2}\cos^3\varphi - (\overline{yy} - \frac{\overline{xx}}{2})\cos^2\varphi\sin\varphi$
$\quad \quad \frac{}{} - \overline{\frac{xx}{2}}\sin^3\varphi - (\frac{\overline{xx}}{2} - \frac{\overline{xyy}}{2})\cos\varphi\sin^2\varphi.$
```