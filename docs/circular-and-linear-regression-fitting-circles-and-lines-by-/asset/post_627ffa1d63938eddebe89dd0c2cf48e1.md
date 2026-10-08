
Späth, Landau) to obtain a full working scheme. Its performance may depend on the quality of the algebraic pref, on the quality of the geometric fit, and on how they blend together.

**Previous tests.** Chernov and Lesort [43] explored various combinations of algebraic and geometric circle fits in an extensive experimental tests. Their results demonstrate that each combination is nearly 100% reliable and efficient when the data are sampled along a full circle or a large arc; this situation remains quite stable for arcs between $360^{\circ}$ and about $90^{\circ}$.

On smaller arcs (below $90^{\circ}$), the Kåsa fit returns a heavily biased estimate that lies quite far from the global minimum of the objective function $\mathscr{F}$. Then the Späth and Landau methods would crawl to the minimum of $\mathscr{F}$ at such a slow pace that for all practical purposes they would fail to converge. The Levenberg-Marquardt fits still converge fast, within 10-20 iterations. If the initial guess is provided by the Pratt or Taubin fit, then all the geometric methods manage to converge, though again the Levenberg-Marquardt schemes are far more efficient than others.

We refer the reader to [43] for more detailed results presented by easy-to-read plots and diagrams.

**Another test.** We include another numerical test here similar to the one described in Section 5.8. For each $\alpha=360^{\circ}, \ldots, 30^{\circ}$ we again generate $10^{6}$ random samples of $n=20$ points located (equally spaced) on an arc of angle $\alpha$ of the unit circle $x^{2}+y^{2}=1$ and corrupted by Gaussian noise at level $\sigma=0.05$. As in Section 5.8, we started with a full circle ($\alpha=360^{\circ}$) and wend down to rather small arcs ($\alpha=30^{\circ}$).

For every generated random sample we determined the distance $d$ from the circle center estimated by the algebraic fit (Kåsa, Pratt, or Taubin) and the one found by the subsequent geometric fit (Levenberg-Marquardt). This distance shows how well the algebraic fit approximates the minimum of the objective function. We also record the number of iterations $i$ the geometric procedure took to converge.

Table 5.6 shows the medians of $d$ and $i$ for each algebraic fit and for each $\alpha$. We see that for large arcs all the algebraic fits provide accurate initial guesses (in one case, for the full circle, Kåsa is actually the most accurate!). On smaller arcs, the Kåsa fit falls behind the other two, due to its heavy bias, which results in a larger number of iterations the Levenberg-Marquardt has to take to recover. The Taubin fit again slightly outperforms the Pratt fit.

| $\alpha$ | Kåsa ($d$) | Kåsa ($i$) | Pratt ($d$) | Pratt ($i$) | Taubin ($d$) | Taubin ($i$) |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 360 | 0.00158 | 3 | 0.00159 | 3 | 0.00159 | 3 |
| 300 | 0.00190 | 3 | 0.00164 | 3 | 0.00164 | 3 |
| 240 | 0.00413 | 3 | 0.00188 | 3 | 0.00187 | 3 |
| 180 | 0.01404 | 4 | 0.00257 | 3 | 0.00256 | 3 |
| 120 | 0.06969 | 5 | 0.00478 | 4 | 0.00473 | 4 |
| 90 | 0.19039 | 6 | 0.00815 | 4 | 0.00800 | 4 |
| 60 | 0.53087 | 9 | 0.02010 | 6 | 0.01929 | 6 |
| 45 | 0.75537 | 12 | 0.04536 | 8 | 0.04265 | 8 |
| 30 | 0.58054 | 17 | 0.11519 | 12 | 0.10609 | 12 |

*Table 5.6 The median distance $d$ from the circle center estimate provided by an algebraic fit (Kåsa, Pratt, or Taubin) and the one found by the subsequent geometric fit. In addition, $i$ is the median number of iterations the geometric fit took to converge.*

**Initialization in nearly singular cases.** To this rosy picture we must add a final, somewhat spicy remark. It concerns the singular case where the data are sampled along a very small arc, so that the best fitting circle would look nearly flat; see an example in Fig. 3.1. In that case it is crucial that the initial guess is selected on the right side of the data set, i.e., inside the best fitting circle. If the initial guess were selected outside the best circle, it would fall into the escape valley from which geometric fitting procedures would never recover, cf. Sections 3.7 and 3.9.

According to our analysis in Section 3.9, the right side of the data set (i.e., the side on which the center of the best fitting circle lies) is determined by the sign of

$$\overline{xxy} = \frac{1}{n} \sum_{i=1}^{n} x_{i}^{2} y_{i},$$

which we called the *signature* of the data set. It is assumed here that the data set is properly aligned, i.e., it is centered so that $\bar{x} = \bar{y} = 0$ and rotated so that

$$\overline{xy} = 0 \quad \text{and} \quad \overline{xx} > \overline{yy}.$$

In Section 3.9 we established the following rules:

- (a) if $\overline{xxy} > 0$, then the center of the best fitting circle lies *above* the $x$ axis; the wrong valley lies below the $x$ axis;
- (b) if $\overline{xxy} < 0$, then the center of the best fitting circle lies *below* the $x$ axis; the wrong valley lies above the $x$ axis.

Let us see if our algebraic circle fits abide by these rules, i.e., place the center on the correct side of the data set. For the Kåsa fit, the second equation in (5.5) yields

$$b = -\frac{C}{2} = \frac{\overline{yz}}{2\overline{yy}} = \frac{\overline{xxy} + \overline{yyy}}{2\overline{yy}}.$$

Since the denominator is positive, the sign of $b$ coincides with that of $\overline{xxy}+\overline{yyy}$. If this expression has the same sign as $\overline{xxy}$, the center is placed on the right side, otherwise it ends up on the wrong side (in the escape valley).

Usually, in accordance with (5.73), $x_i$'s are larger than $y_i$'s, so $\overline{xx}$ is very likely to be greater than $\overline{yy}$, in which case the Kåsa fit will make the right choice. However, the wrong side may be selected, too (see an example below), hence the Kåsa fit may completely distract the subsequent geometric fitting procedure.

The Pratt and Taubin fits can be analyzed similarly. In the Taubin case, we have

$\mathbf{X}_0^T \mathbf{X}_0 \mathbf{A}_0 = \eta \mathbf{A}_0$,

where $\eta \geq 0$ is the smallest eigenvalue of $\mathbf{X}_0^T \mathbf{X}_0$, cf. Section 5.10. Now the second equation in the above $3 \times 3$ system gives

$b = - \frac{C}{2A} = \frac{\overline{yz}}{2(\overline{yy} - \eta)} = \frac{\overline{xx} + \overline{yy}}{2(\overline{yy} - \eta)}$.

We also note that $\eta < \overline{yy}$, because the vector $\mathbf{A}_1 = (0,0,1)^T$ has Rayleigh quotient $\mathbf{A}_1^T \mathbf{X}_0^T \mathbf{X}_0 \mathbf{A}_1 = \overline{yy}$, which of course cannot be smaller than the minimal eigenvalue $\eta$. Thus again, as in the Kåsa case, the sign of $b$ coincides with that of $\overline{xx} + \overline{yy}$.

In the Pratt case, the parameter vector $\mathbf{A}$ satisfies

$\mathbf{X}^T \mathbf{X} \mathbf{A} = \eta \mathbf{B}\mathbf{A}$,

see Section 5.5, and the third equation of this $4 \times 4$ system gives

$b = - \frac{C}{2A} = \frac{\overline{yz}}{2(\overline{yy} - \eta)} = \frac{\overline{xx} + \overline{yy}}{2(\overline{yy} - \eta)}$,

which coincides with (5.75), except here $\eta$ is an eigenvalue of a different matrix. But again one can easily check that $\eta < \overline{yy}$ (we omit details), hence the sign of $b$ coincides with that of $\overline{xx} + \overline{yy}$.

*Remark.* Comparing (5.74) and (5.75) reveals why the Kåsa fit consistently returns smaller circles than the Pratt or Taubin fit in the nearly singular case: it happens because the corrective term $\eta > 0$ always decreases the denominator of (5.75).

Returning to our main issue, we see that all the three algebraic fitting algorithms follow the same rule: they place the circle center in accordance with the sign of $\overline{xx} + \overline{yy}$. And the correct choice should be based on the sign of $\overline{xx}$ alone. The question is: are these two rules equivalent? The following example shows that they are not, i.e., all the algebraic algorithms can actually make the wrong choice.

- **Counter-example.** Consider a set of $n = 5$ points: $(0, 2), \quad (1, -1 - \varepsilon), \quad (-1, -1 - \varepsilon), \quad (2, \varepsilon), \quad (-2, \varepsilon)$
