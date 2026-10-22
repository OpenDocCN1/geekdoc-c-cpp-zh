| Implication | $g(R,w)$ | $\frac{\partial g(R,w)}{\partial R}$ | $\frac{\partial g(R,w)}{\partial w}$ |
|---|---|---|---|
| Lukasiewicz | $\frac{w}{2}(2R - R^2)$ | $\frac{w}{2}(2 - 2R)$ | $\frac{1}{2}(2R - R^2)$ |
| Fodor | $\begin{cases} \frac{w}{2}(1 - 2R + 2R^2), & \text{if } R > \frac{1}{2} \\ \frac{w}{2}(2R - 2R^2), & \text{if } R \le \frac{1}{2} \end{cases}$ | $\begin{cases} \frac{w}{2}(4R - 2), & \text{if } R > \frac{1}{2} \\ \frac{w}{2}(2 - 4R), & \text{if } R \le \frac{1}{2} \end{cases}$ | $\begin{cases} \frac{1}{2}(1 - 2R + 2R^2), & \text{if } R > \frac{1}{2} \\ \frac{1}{2}(2R - 2R^2), & \text{if } R \le \frac{1}{2} \end{cases}$ |
| Reichenbach | $\frac{w}{2}R$ | $\frac{w}{2}$ | $\frac{1}{2}R$ |
| Kleene-Dienes | $\frac{w}{2}R^2$ | $\frac{w}{2}2R$ | $\frac{1}{2}R^2$ |
| Zadeh | $\begin{cases} \frac{w}{2}(2R - 1), & \text{if } R \ge \frac{1}{2} \\ 0, & \text{if } R < \frac{1}{2} \end{cases}$ | $\begin{cases} \frac{w}{2}(2), & \text{if } R \ge \frac{1}{2} \\ 0, & \text{if } R < \frac{1}{2} \end{cases}$ | $\begin{cases} \frac{1}{2}(2R - 1), & \text{if } R \ge \frac{1}{2} \\ 0, & \text{if } R < \frac{1}{2} \end{cases}$ |

Table 11.2 Some needed derivatives for selected implications.

Another solution accelerating the convergence of the method is the estimation of parameters $\underline{p}^{(k)}; k = 1, ..., K$ by means of least squares method. The output value $y_0$ of the system in equation (11.52) may be considered to be a linear combination of unknown parameters $\underline{p}^{(k)}$. If we introduce the following notation:

```
$S^{(k)}(\underline{x}_0) = \frac{g\left[R_k(\underline{x}_0), w^{(k)}\right]}{\sum_{i=1}^{K} g\left[R_i(\underline{x}_0), w^{(i)}\right]}, \qquad (11.60)$
```

```
$\underline{D}(\underline{x}_0) = \left[ S^{(1)}x_0'^T : S^{(2)}x_0'^T : ... : S^{(K)}x_0'^T \right]^T, \qquad (11.61)$
```

```
$\underline{P} = \left[ \underline{p}^{(1)T} : \underline{p}^{(2)T} : ... : \underline{p}^{(K)T} \right]^T \qquad (11.62)$
```