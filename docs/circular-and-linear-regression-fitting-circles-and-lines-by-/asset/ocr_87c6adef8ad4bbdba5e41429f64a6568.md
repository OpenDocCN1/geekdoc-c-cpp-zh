**The RTKD inversion-based fit.** The numerical implementation of the RTKD fit is quite straightforward. One precomputes the weights

```
w_i = (x_i'^2 + y_i'^2)^2
```

and then solves the linear weighted least squares problem by minimizing

```
$\mathscr{F}_{\text{RTKD}}(\alpha, \beta, c) = \sum_{i=1}^n w_i(\alpha x_i' + \beta y_i' + c)^2$
```

subject to the constraint $\alpha^2 + \beta^2 = 1$. The solution $(\alpha, \beta)$ minimizing (8.26) must be the eigenvector of the $2 \times 2$ weighted scatter matrix $\mathbf{S}_w$ corresponding to its smallest eigenvalue. The weighted scatter matrix $\mathbf{S}_w$ is defined by

```
$\mathbf{S}_w = \frac{1}{\sum w_i} \sum_{i=1}^n w_i(\mathbf{r}_i - \bar{\mathbf{r}})(\mathbf{r}_i - \bar{\mathbf{r}})^T,$
```

where $\mathbf{r}_i = (x_i', y_i')^T$ is the ith “data vector” and $\bar{\mathbf{r}} = (\sum w_i \mathbf{r}_i)/(\sum w_i)$; compare this to (1.7). Note that the factor $1/(\sum w_i)$ in (8.27) is irrelevant and can be dropped. The last parameter $c$ is determined from the equation

```
$\alpha \sum w_i x_i' + \beta \sum w_i y_i' + c \sum w_i = 0.$
```

This concludes our description of the RTKD circle fit.

We remark that the authors of [159] implement the above procedure slightly differently. They describe the line by equation $y' = a + bx'$, instead of our (8.21), and then propose to compute $a$ and $b$ by the classical formulas (1.14)\u2212(1.16) (with extra weights). This approach, however, excludes vertical lines and becomes numerically unstable when the line is close to vertical. The above eigenvalue method, using standard matrix software, ensures numerical stability and handles all lines without exception.

**Analysis of the RTKD inversion-based fit.** The authors of [159] do not provide a statistical analysis of their fit. We just indicate its relation to another fit here.

First, we use (8.20) to express the objective function (8.24) in the original coordinates $(x_i, y_i)$:

```
$\mathscr{F}_{\text{RTKD}}(\alpha, \beta, c) = \sum_{i=1}^n \frac{[\alpha x_i + \beta y_i + c(x_i^2 + y_i^2)]^2}{\alpha^2 + \beta^2}$.
```

Second, we use our old notation $z_i = x_i^2 + y_i^2$ and change parameters as

```
$A = c$, $B = \alpha$, $C = \beta$,$
```