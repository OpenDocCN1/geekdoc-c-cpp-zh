
where $d_i$'s are the distances from the data points to the fitted circle and $k$ is the number of unknown parameters ($k = 3$ for circles); then one can reduce the bias using $\hat{\sigma}^2$ in place of $\sigma^2$.

This does not seem to be a perfect solution, though, as the estimate $\hat{\sigma}^2$ is computed from some initial fit, which may be essentially biased and inconsistent, thus $\hat{\sigma}^2$ may not be very accurate. Then, after one refits the circle by using an essentially unbiased and consistent fitting algorithm, it is tempting to reestimate $\hat{\sigma}^2$ (using the distances from the data points to the new circle) and then recompute the fit accordingly. Obviously, one can continue these adjustments recursively, hoping that the process would converge, and the limit circle would be indeed essentially unbiased and consistent.

The above iterative procedure is rather time consuming, and its convergence cannot be guaranteed. A better alternative would be to incorporate the estimation of $\sigma^2$ into the construction of the essentially unbiased and consistent fit. Such schemes have been designed by several authors independently, and we describe them next.

## 7.10 Kukush-Markovsky-van Huffel method

**KMvH consistent estimator.** In the early 2000s Kukush, Markovsky, and van Huffel proposed a consistent estimator for the parameters of quadratic curves (and surfaces) that are fitted to observed data. They started with ellipses whose center was known [115], then went on to ellipsoids [130] and general quadratic surfaces [114]; lastly, they provided complete and detailed mathematical proofs in [167]. Though they never treated the problem of fitting circles, we will adapt their approach to this task here. We abbreviate their algorithm as KMvH (after Kukush, Markovsky, and van Huffel).

Their basic observation is that, as $n \to \infty$, the matrix $\mathbf{M}_{\text{unbiased}}$ converges to its true (noise-free) value $\bar{\mathbf{M}}$; in fact,

$$\mathbf{M}_{\text{unbiased}} = \bar{\mathbf{M}} + \mathcal{O}_p(n^{-1/2}),$$

according to the classical central limit theorem. The true matrix $\bar{\mathbf{M}}$ is positive semi-definite and singular; its only zero eigenvalue corresponds to the true parameter vector $\bar{\mathbf{A}}$, because $\bar{\mathbf{M}}\bar{\mathbf{A}} = \mathbf{0}$, cf. Section 7.3.

Thus Kukush, Markovsky, and van Huffel estimate the unknown variance $V = \sigma^2$ by a value $\hat{V}$ that makes the variable matrix

$$\mathbf{M}_{\text{unbiased}}(V) = \mathbf{M} - V\mathbf{H} + 8V^2\mathbf{I}_1 \quad (7.65)$$

positive semi-definite and singular, i.e., they find $\hat{V}$ such that

$$\mathbf{M}_{\text{unbiased}}(\hat{V}) \geq \mathbf{0} \quad \text{and} \quad \det \mathbf{M}_{\text{unbiased}}(\hat{V}) = 0. \quad (7.66)$$

Then the eigenvector of $\mathbf{M}_{\text{unbiased}}(\hat{V})$ corresponding to its zero eigenvalue would be the desired estimate $\hat{\mathbf{A}}$ of the parameter vector, i.e., $\hat{\mathbf{A}}$ satisfies

$\mathbf{M}_{\text{unbiased}}(\hat{V}) \hat{\mathbf{A}}=\mathbf{0}. \quad (7.67)$

Note that in this way one estimates $\sigma^2$ and $\mathbf{A}$ simultaneously, thus eliminating the need for further adjustments that were mentioned in Section 7.9.

Of course it is not immediately clear whether the value $\hat{V}$ satisfying (7.66) exists, or if it is unique. To this end Shklyar, Kukush, Markovsky, and van Huffel [167] prove the following:

**Theorem 14 ([167])** *There is a unique value $\hat{V} \geq 0$ that satisfies (7.66). For all $V<\hat{V}$ the matrix $\mathbf{M}_{\text{unbiased}}(V)$ is positive definite, and for all $V>\hat{V}$ that matrix is indefinite, i.e., it has at least one negative eigenvalue.*

They actually proved that the minimal eigenvalue of the variable matrix $\mathbf{M}_{\text{unbiased}}(V)$, let us call it $\lambda_{\min}(V)$, is a continuous function of $V$ which is strictly positive for $V<\hat{V}$ and strictly negative for $V>\hat{V}$. Based on this theorem, Shklyar, Kukush, Markovsky, and van Huffel [167] propose to simultaneously estimate $\mathbf{A}$ and $V$ via the bisection method as follows:

- **Step 1.** Set $V_{\mathrm{L}}=0$ so that $\lambda_{\min}(V_{\mathrm{L}}) \geq 0$. If $\lambda_{\min}(V_{\mathrm{L}})=0$, go to Step 4. Set $V_{\mathrm{R}}$ to a large enough value such that $\lambda_{\min}(V_{\mathrm{R}})<0$. (It is shown in [167] that $V_{\mathrm{R}}$ may always be set to the minimum eigenvalue of the scatter matrix $\mathbf{S}$ defined by (1.5).)
- **Step 2.** Compute $V_{\mathrm{M}}=\frac{1}{2}(V_{\mathrm{L}}+V_{\mathrm{R}})$.
- **Step 3.** If $\lambda_{\min}(V_{\mathrm{M}}) \geq 0$, reset $V_{\mathrm{L}}=V_{\mathrm{M}}$, otherwise reset $V_{\mathrm{R}}=V_{\mathrm{M}}$. If $\lambda_{\min}(V_{\mathrm{L}})=0$ or $V_{\mathrm{R}}-V_{\mathrm{L}}<\text{tolerance}$, go to Step 4. Otherwise return to Step 2.
- **Step 4.** Set $\hat{V}=V_{\mathrm{L}}$ and compute $\hat{\mathbf{A}}$ as an eigenvector of $\mathbf{M}_{\text{unbiased}}(\hat{V})$ corresponding to its smallest eigenvalue.

The advantage of this bisection scheme is that it is guaranteed to converge, though its convergence is slow (linear). We will see in Section 7.12 that one can accelerate the procedure by using (approximate) derivatives of $\lambda_{\min}(V)$ and Newton's iterations; this was done by Kanatani. For the task of fitting circles, a much faster noniterative solution will be presented in Section 7.12.

**Advantages of the KMvH estimator.** Kukush, Markovsky, and van Huffel [114, 167] derive many statistical and geometric properties of their estimators $\hat{\mathbf{A}}$ and $\hat{V}$. First, both are strongly consistent, i.e.

$\hat{\mathbf{A}} \rightarrow \overline{\mathbf{A}} \quad \text{and} \quad \hat{V} \rightarrow \overline{\sigma}^{2} \quad \text{as} \quad n \rightarrow \infty,$

with probability one. In addition, $\hat{\mathbf{A}}=\overline{\mathbf{A}}+\mathcal{O}_{P}(n^{-1/2})$, in accordance with the central limit theorem (see Remark 12 in [167]).

Second, they proved that their estimators $\hat{\mathbf{A}}$ and $\hat{V}$ are invariant under translations and rotations, thus the fitted curve and $\hat{\sigma}^{2}$ do not depend on the choice of the coordinate system; see Theorems 30 and 31 in [167]. Of course, if one rescales $x$ and $y$ by $x \mapsto cx$ and $y \mapsto cy$ with some constant $c > 0$, then $\hat{\sigma}^{2}$ is replaced by $c^{2}\hat{\sigma}^{2}$, as required.

**A real data example.** We have tested the KMvH estimator on the real data example described in Section 5.12. That fit returned a circle with

center $= (7.3857, 22.6688), \quad \text{radius} = 13.8164,$

which is very close to the circles returned by the Pratt and Taubin fits (Section 5.12) and the Hyper fit (Section 7.6). Actually, it is closer to the ideal circle (5.71) than circles returned by other fits.

**Back to the known $\sigma^{2}$ case.** We note that choosing $\hat{\mathbf{A}}$ as an eigenvector of $\mathbf{M}_{\text{unbiased}}(\hat{V})$ corresponding to its minimal (i.e., zero) eigenvalue is equivalent to minimizing $\mathbf{A}^{T}\mathbf{M}_{\text{unbiased}}(\hat{V})\mathbf{A}$ subject to $\|\mathbf{A}\|=1$. This may suggest that in the case of *known* $V=\sigma^{2}$, one could also minimize $\mathbf{A}^{T}\mathbf{M}_{\text{unbiased}}(V)\mathbf{A}$ subject to $\|\mathbf{A}\|=1$, where the known $V$ is used, instead of its estimate $\hat{V}$. One might expect that using the exact true value of $V$, rather than statistically imprecise estimate $\hat{V}$, will improve the accuracy of the resulting fit.

Surprisingly, the substitution of the known $V$ for its estimate $\hat{V}$ can only lead to complications, as Shklyar and others [167] discover. First, the resulting estimate $\hat{\mathbf{A}}$ will *not* be translation invariant (though it remains rotation invariant); see [167]. To remedy the situation, Shklyar and others [167] propose, if one wants to use the known $V$, another constraint that ensures translation invariance. In the case of circles, it coincides with the Kása constraint, i.e., we need to minimize $\mathbf{A}^{T}\mathbf{M}_{\text{unbiased}}(V)\mathbf{A}$ subject to $\mathbf{A}^{T}\mathbf{K}\mathbf{A} = 1$, where $\mathbf{K}$ was introduced in (7.19) and $V$ is the known variance. This method guarantees translation invariance.

Furthermore, even with the right constraint, the use of the known value of $V=\sigma^{2}$, instead of its estimate $\hat{V}$, may not improve the accuracy. Kukush, Markovsky, and van Huffel [114, 115] experimentally compared two estimation procedures for fitting ellipses. One uses the known value of $V=\sigma^{2}$ and computes a translation invariant ellipse fit, as mentioned above. The other ignores the known $V$ and estimates it, according to Steps 1–4 described earlier in this section. Rather surprisingly, the second method consistently demonstrated the better performance, i.e., produced more accurate ellipse fits.

This may appear rather illogical. The authors of [114, 115] do not offer any explanation for their paradoxical observations. One may speculate that estimating $\sigma^{2}$ allows the algorithm to "adapt" to the data better, while trying to use the fixed value of $\sigma^{2}$ for every sample may be destructive. Perhaps, this phenomenon requires further investigation.
