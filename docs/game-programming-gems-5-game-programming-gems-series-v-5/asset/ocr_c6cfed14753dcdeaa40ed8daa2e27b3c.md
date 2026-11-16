and so forth, and finally we get Equation 2.2.17

```
\frac{\partial}{\partial \alpha_{k+1}} \int_0^1 \|k(u)\|^2 du = 4\alpha_k \mathbf{t}_k \cdot \mathbf{t}_{k+1} + 8\alpha_{k+1}^2 - 12\mathbf{p}_{k,k+1} \cdot \mathbf{t}_{k+1}. (2.2.17)
```

Once again we divide Equations 2.2.14 through 2.2.17 by four and rewrite them into matrix form, just as we did for Equation 2.2.8 to get the matrix in Equation 2.2.10. Note that if the tangents are normalized prior to solving the system, then \(t^2 = 1\). This makes the matrix even simpler, but this is not done here. The system that needs to be solved looks like Equation 2.2.18

```
\begin{bmatrix} 2t_1^2 & \mathbf{t}_1 \cdot \mathbf{t}_2 & 0 & 0 & \cdots & 0 & 0 \\ \mathbf{t}_1 \cdot \mathbf{t}_2 & 4t_2^2 & \mathbf{t}_2 \cdot \mathbf{t}_3 & 0 & \cdots & 0 & 0 \\ 0 & \mathbf{t}_2 \cdot \mathbf{t}_3 & 4t_3^2 & \mathbf{t}_3 \cdot \mathbf{t}_4 & \cdots & 0 & 0 \\ \vdots & \vdots & \vdots & \vdots & \ddots & \vdots & \vdots \\ 0 & 0 & 0 & 0 & \cdots & \mathbf{t}_k \cdot \mathbf{t}_{k+1} & 2t_{k+1}^2 \end{bmatrix} \begin{bmatrix} \alpha_1 \\ \alpha_2 \\ \alpha_3 \\ \vdots \\ \alpha_{k+1} \end{bmatrix} = \begin{bmatrix} 3\mathbf{t}_1 \cdot \mathbf{p}_{12} \\ 3\mathbf{t}_2 \cdot (\mathbf{p}_{12} + \mathbf{p}_{23}) \\ 3\mathbf{t}_3 \cdot (\mathbf{p}_{23} + \mathbf{p}_{34}) \\ \vdots \\ 3\mathbf{t}_{k+1} \cdot \mathbf{p}_{k,k+1} \end{bmatrix}. (2.2.18)
```

Note that nonzero entries appear only on the main diagonal and immediately above and below it. A system involving a matrix of this form is called a tridiagonal system and can be solved very efficiently using a specialized algorithm [Lengyel04].

![](bbox=[0.3, 0.58, 0.7, 0.82])

FIGURE 2.2.2 Three connected minimal bending Hermite curves.