We assume the solution to exist, to be unique, finite, and expandable in a Taylor series in the vicinity of the initial point $t_0$:

$$y(t)=y(t_0)+\frac{t-t_0}{1!}y'(t_0)+\frac{(t-t_0)^2}{2!}y''(t_0)+\cdots.$$ \tag{12.13}

The Taylor expansion (12.13) provides a step-by-step procedure for evaluating the solution $y(t)$ at given mesh points $t_0,t_1,\ldots,t_m,\ldots$ as a sequence of solutions of elementary Cauchy problems. Specifically, propagating the solution from $t_m$ to $t_{m+1}$ is equivalent to solving the differential equation (12.11) subject to the initial condition

$$y(t_m)=y_m,$$

and it is accomplished based on the expansion

$$y_{m+1}=y_m+hy'_m+\frac{h^2}{2}y''_m+\cdots, \tag{12.14}$$

where $y_m\equiv y(t_m)$, $y'_m\equiv y'(t_m)$, $y''_m\equiv y''(t_m)$, and the mesh spacing is given by

$$h=t_{m+1}-t_m.$$

The smaller the mesh spacing $h$ in comparison to the convergence radius of the series, and the larger the number of terms kept in series (12.14), the closer the estimate $y_{m+1}$ to the exact solution $y(t_{m+1})$.

Determining the propagated solution $y_{m+1}$ requires the derivatives at $t_m$, namely $y'_m,y''_m,\ldots$. As a matter of fact, the first derivative is already available from ODE (12.11) itself and it just needs to be evaluated at $t_m$:

$$y'_m=f(t_m,y_m).$$

On the other hand, by taking the derivatives of both members of Equation 12.11 with respect to $t$ (bearing in mind that $f$ is a function of $t$ both explicitly and through $y$), one finds for the second derivative at $t_m$:

$$y''_m=\left[\frac{\partial f}{\partial t}+\frac{\partial f}{\partial y}\frac{\partial y}{\partial t}\right]_{t_m,y_m}=\left[\frac{\partial f}{\partial t}+\frac{\partial f}{\partial y}f\right]_{t_m,y_m}.$$

Now, plugging the expressions of $y'_m$ and $y''_m$ into Expansion 12.14, we get the propagation relation:

$$y_{m+1}=y_m+hf(t_m,y_m)+\frac{h^2}{2}\left[\frac{\partial f}{\partial t}+f\frac{\partial f}{\partial y}\right]_{t_m,y_m}+O(h^3). \tag{12.15}$$

The notation $O(h^3)$ indicates that the remainder (truncation error) is of the order $h^3$, that is, all the neglected terms involve $h$ at powers greater or equal to three, while the retained terms imply at most $h^2$. The Taylor series method is obviously a *one-step method*, since determining $y_{m+1}$ requires only information from the preceding point $t_m$.

For higher-order approximations of the solution, one needs to consider additional terms in series (12.14). Anyhow, the implied higher-order derivatives become more and more intricate, both to derive and to program, leading to inefficient propagation formulas. In certain situations, the bare evaluation of the derivatives becomes impossible.

Notwithstanding the practical deficiencies, the Taylor series method retains, as already mentioned, a special theoretical importance, since it provides a unifying criterion for assessing the accuracy of other methods for Cauchy problems. The criterion refers to the degree in which the approximate solution coincides with the Taylor series expansion of the exact solution. More precisely, a method is said to be of order $p$ if the approximate solution is equivalent with the exact Taylor series up to terms of the order