Since the linear stability problem for this solution has constant coefficients, we easily determine the spectrum analytically. Repeating the method outlined in the previous section, we consider perturbations of the form

```
(4.1) $$\eta(x) = \epsilon^{i\mu x + i\rho y + \lambda t} \sum_{j=-\infty}^{\infty} \hat{\eta}_j e^{ijx},$$
```

```
(4.2) $$q(x) = \epsilon^{i\mu x + i\rho y + \lambda t} \sum_{j=-\infty}^{\infty} \hat{q}_j e^{ijx},$$
```

where $\epsilon$ is a small parameter.

Substituting this solution form into the equations of motion and simplifying as before, we find that the eigenvalues $\lambda$ are purely imaginary, as expected. They are given by

```
(4.3) $$\lambda_m^s = -i c (\mu + m) + i s \sqrt{g \kappa \tanh(\kappa h)}$$
```

where $s = \pm 1$, $m \in \mathbb{Z}$, $\kappa = \sqrt{(\mu + m)^2 + \rho^2}$, and $\kappa \neq 0$. Thus, for each perturbation (parameterized by $\mu$ and $\rho$), we can determine the growth-rates $\lambda_m^s$ for all $m \in \mathbb{Z}$.

Since all eigenvalues are purely imaginary, it follows that flat water is spectrally stable. Using the results of MacKay & Saffman[MS86], we know that for an instability to arise in the water wave system, it is necessary for two eigenvalues with opposite signatures to collide, where the signature of a particular eigenvalue is given by

```
$$\operatorname{sig}(\lambda_m^s) = -\operatorname{Im}(s \lambda_m^s).$$
```

Using the signature and the form of the eigenvalues $\lambda$, we see that a necessary condition for an instability to arise is that

```
$$\lambda_m^{s_1} = \lambda_n^{s_2}, \quad -\operatorname{Im}(s_1 \lambda_m^{s_1}) = \operatorname{Im}(s_2 \lambda_n^{s_2}).$$
```

![](bbox=[0.25, 0.0013, 0.75, 0.00185])

FIGURE 3. Resonant Curves for $h = .5$. The solid lines are associated with the Class I instabilities for $m = 1$ and $m = 2$, and the dashed lines with the Class II instabilities for $m = 1$, and $m = 2$.