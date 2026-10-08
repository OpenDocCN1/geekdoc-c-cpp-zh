iteration **a**. Fig. 4.1 shows the contour map (the sets of level curves) of $\mathscr{L}(\mathbf{a}+\mathbf{h})$ in the 2D case; the level curves are concentric ellipses.

![](bbox=[0.22, 0.13, 0.78, 0.28])

Figure 4.1 The level curves of $\mathscr{L}(\mathbf{a}+\mathbf{h})$ are concentric ellipses (solid ovals), the boundaries of trust regions are dashed circles around **a**.

The “pure” Gauss-Newton step (i.e., when $\lambda = 0$) lands at the minimum of $\mathscr{L}(\mathbf{a}+\mathbf{h})$, i.e., at the ellipses’ center $\mathbf{b}_0$. When $\lambda > 0$, the Levenberg-Marquardt step (the solution of (4.16)) lands at some other point, $\mathbf{b}_{\lambda} = \mathbf{a} + \mathbf{h}$, closer to **a**. At that point we have, according to (4.16),

```
$$\mathrm{grad}\ \mathscr{L}(\mathbf{a} + \mathbf{h}) = -\lambda\mathbf{h}.$$
```

Accordingly, the vector $\mathbf{h} = \mathbf{b}_{\lambda} - \mathbf{a}$ crosses the level curve of $\mathscr{L}(\mathbf{a}+\mathbf{h})$ passing through $\mathbf{b}_{\lambda}$, orthogonally. This means that $\mathbf{b}_{\lambda}$ provides the minimum of the function $\mathscr{L}(\mathbf{a}+\mathbf{h})$ *restricted* to the ball $\mathbb{B}(\mathbf{a},\Delta)$ whose center is **a** and whose radius is $\Delta = \|\mathbf{h}\|$. In other words, the Levenberg-Marquardt step with $\lambda > 0$ minimizes the restriction of the quadratic approximation $\mathscr{L}(\mathbf{a}+\mathbf{h})$ to a certain ball around the current approximation **a** whose radius $\Delta$ is determined by $\lambda$.

As $\lambda > 0$ grows, the point $\mathbf{b}_{\lambda}$ moves closer to **a**, and $\Delta$ decreases. At the same time the vector $\mathbf{h} = \mathbf{b}_{\lambda} - \mathbf{a}$ rotates and makes a larger angle with the level curves. In the limit $\lambda \rightarrow \infty$, the ball $\mathbb{B}(\mathbf{a},\Delta)$ shrinks to the point **a**, i.e., $\Delta \rightarrow 0$, and the vector $\mathbf{h}$ ultimately aligns with the direction of the steepest descent.

**Replacing the control parameter.** Therefore, there is a one-to-one correspondence between $\lambda > 0$ and $\Delta \in (0, \|\mathbf{b}_0 - \mathbf{a}\|]$, hence one can use $\Delta$, instead of $\lambda$, as a control parameter, i.e., adjust $\Delta$ from iteration to iteration. As $\Delta$ has a clear meaning (further explained below), its initialization and its update at each iteration can be done in a more sensible way than the way $\lambda$ is treated in the Levenberg-Marquardt scheme.

One benefit of dealing with $\Delta$ is that one can directly control the region in the parameter space where the quadratic approximation $\mathscr{L}(\mathbf{a}+\mathbf{h})$ is minimized. It is called the *trust region*, the idea behind it is that we minimize the approximation $\mathscr{L}(\mathbf{a}+\mathbf{h})$ where it can be *trusted* and do not go too far where the approximation is not deemed reliable.