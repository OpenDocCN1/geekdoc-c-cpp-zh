An important special case of a scaling transformation is $\alpha = \beta$; it is called a similarity (or sometimes a dilation; in formal mathematics it is known as a homotopy). We will denote it by

```
$S_{\alpha} = S_{\alpha, \alpha}: (x, y) \mapsto (\alpha x, \alpha y).\qquad\qquad (1.21)$
```

It takes little effort to verify that the orthogonal fitting line is invariant under $T_{c,d}$ and $R_{\theta}$, as well as $S_{\alpha}$, but *not* invariant under general scaling transformations $S_{\alpha, \beta}$ with $\alpha \ne \beta$. We leave the verification of these facts to the reader.

The orthogonal fit has a clear appeal when applied to regular geometric patterns. Fig. 1.4 shows four data points placed at vertices of a rectangle. While classical regression lines are skewed upward or downward (the first and second panels of Fig. 1.4), the orthogonal regression line cuts right through the middle of the rectangle and lies on its axis of symmetry. Arguably, the orthogonal fitting line would “please the eye” more than any other line.

However, the orthogonal fit leads to an inconsistency if one applies it to a more general EIV model, where $\sigma_x^2 \ne \sigma_y^2$. This inconsistency stems from the noninvariance of the orthogonal fitting line under scaling transformations $S_{\alpha, \beta}$.

For example, let us again consider the task of determining the iron density by using (1.8) and measuring volumes $x_i$'s and masses $y_i$'s of some iron pieces, cf. the previous section. If we employ the orthogonal fit to the measurements $(x_1, y_1), \ldots, (x_n, y_n)$, then the fitting line $y = bx$, and the resulting estimate of the iron density $\rho = b$, would depend on the choice of units in which the measurements $x_i$'s and $y_i$'s are recorded. That is, if we rescale the variables by $(x, y) \mapsto (\alpha x, \beta y)$, the equation of the orthogonal fitting line in the new coordinate system would be $\beta y = b'(\alpha x)$, where $b' \ne b$. In other words, a different density would be obtained if we change pounds to kilograms or tons, and similarly liters to bushels or cubic meters.

This objection was raised in 1937 by Roos [156] and further discussed in the statistics literature in the 1940s [89, 187]. Thus the orthogonal fit has its limitations, it is essentially restricted to the special case $\sigma_x^2 = \sigma_y^2$ of the EIV model. Some modern books, see e.g., [28], strongly warn against the use of orthogonal fitting line in EIV applications with $\sigma_x^2 \ne \sigma_y^2$, and more generally, against the use of other techniques that are based on any unreliable assumptions about $\sigma_x^2$ and $\sigma_y^2$.

We briefly overview basic features of the general EIV model in the next section (though not attempting anything close to a comprehensive coverage).

# **1.4 Solving a general EIV problem**

Let us turn back to the EIV model (1.9)–(1.10) without assuming (1.11), i.e., leaving $\sigma_x^2$ and $\sigma_y^2$ unconstrained.

Kumell [117] was perhaps the first who examined, in 1879, the task of