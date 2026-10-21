Use the solutions $f_+$ and $g_+$ to define a matrix

```
$$\mathbf{T}_+ = \begin{bmatrix} 0 & 0 & e^{p_3 M} & 0 & 0 \\ 0 & 0 & p_3 e^{p_3 M} & 0 & 0 \\ 0 & 0 & p_3^2 e^{p_3 M} & 0 & 0 \\ 0 & 0 & \frac{p_3^2 + k^2}{p_3^2 - k^2} e^{p_3 M} & 0 & e^{-k M} \\ 0 & 0 & \frac{(p_3^2 + k^2) p_3}{p_3^2 - k^2} e^{p_3 M} & 0 & -k e^{-k M} \end{bmatrix}$$
```

with

```
$$\mathbf{T}_+ \begin{pmatrix} c_1 \\ c_2 \\ c_3 \\ \beta_1 \\ \beta_2 \end{pmatrix} = \begin{pmatrix} f(+M) \\ f'(+M) \\ f''(+M) \\ g(+M) \\ g'(+M) \end{pmatrix}$$
```

Then use an ODE solver to examine the system (4.14)-(4.15) on the interval $[-M, M]$ as an initial value problem. This leads to a matrix $\mathbf{T}$ such that

```
$$\mathbf{T} \begin{pmatrix} f(-M) \\ f'(-M) \\ f''(-M) \\ g(-M) \\ g'(-M) \end{pmatrix} = \begin{pmatrix} f(+M) \\ f'(+M) \\ f''(+M) \\ g(+M) \\ g'(+M) \end{pmatrix}$$
```

Now we have two methods to compute the values of the solution at $x = +M$, and the system (4.14)-(4.15) has a nonzero solution if and only if

```
$(4.23)\qquad D(k,\gamma) = \det(\mathbf{M}(k,\gamma)) = \det(\mathbf{T} \cdot \mathbf{T}_- - \mathbf{T}_+) = 0$
```

Thus we examine solutions of this equation as function of the parameters $k$ and $\gamma$.

# 4.4. The special case $k = 0$. For $k = 0$, equation (4.15) reads as $g''(x) = f''(x)$ and the only solution satisfying $g(\pm\infty) = f(\pm\infty)$ is $g(x) = f(x)$. Then (4.14) leads to

```
$(4.24)\qquad \frac{d}{dx} \begin{pmatrix} f \\ f' \\ f'' \end{pmatrix} = \begin{bmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ -4\gamma + 6 u_0' & 4 + 6 u_0 & 0 \end{bmatrix} \begin{pmatrix} f \\ f' \\ f'' \end{pmatrix}$
```

Using the same approach as in the previous section we define

```
$$\mathbf{T}_- \begin{pmatrix} c_1 \\ c_2 \\ c_3 \end{pmatrix} = \begin{pmatrix} f(-M) \\ f'(-M) \\ f''(-M) \end{pmatrix} = \begin{bmatrix} e^{-p_1 M} & e^{-p_2 M} & 0 \\ p_1 e^{-p_1 M} & p_2 e^{-p_2 M} & 0 \\ p_1^2 e^{-p_1 M} & p_2^2 e^{-p_2 M} & 0 \end{bmatrix} \begin{pmatrix} c_1 \\ c_2 \\ c_3 \end{pmatrix}$$
```

```
$$\mathbf{T}_+ \begin{pmatrix} c_1 \\ c_2 \\ c_3 \end{pmatrix} = \begin{pmatrix} f(+M) \\ f'(+M) \\ f''(+M) \end{pmatrix} = \begin{bmatrix} 0 & 0 & e^{p_3 M} \\ 0 & 0 & p_3 e^{p_3 M} \\ 0 & 0 & p_3^2 e^{p_3 M} \end{bmatrix} \begin{pmatrix} c_1 \\ c_2 \\ c_3 \end{pmatrix}$$
```

```
$$\mathbf{T}_0 \begin{pmatrix} f(-M) \\ f'(-M) \\ f''(-M) \end{pmatrix} = \begin{pmatrix} f(+M) \\ f'(+M) \\ f''(+M) \end{pmatrix}$$
```

where $\mathbf{T}_0$ is constructed using an ODE solver for (4.24). Then the system (4.14)-(4.15) has a nonzero solution for $k = 0$ if and only if

```
$(4.25)\qquad D_0(\gamma) = \det(\mathbf{M}_0(\gamma)) = \det(\mathbf{T}_0 \cdot \mathbf{T}_- - \mathbf{T}_+) = 0$
```