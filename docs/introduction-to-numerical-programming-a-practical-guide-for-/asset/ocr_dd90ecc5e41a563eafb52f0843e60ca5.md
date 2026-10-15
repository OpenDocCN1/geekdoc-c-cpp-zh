the pth-order method provides solutions coinciding with the O(h^p) approximations of the corresponding Taylor series. The increase of the order is accompanied naturally by superior precision, yet also by increased implementation complexity.

Let us consider the generic Cauchy problem for a first-order ODE or system of ODEs:

$$y' = f(t,y), \qquad y(t_0)=y_0.$$  \tag{12.23}

The propagation of the solution y(t) from t_m to t_{m+1} may be accomplished, as discussed in Section 12.2, by applying the Taylor expansion

$$y_{m+1}=y_m+hf(t_m,y_m)+\frac{h^2}{2}\left[\frac{\partial f}{\partial t}+f\frac{\partial f}{\partial y}\right]_{t_m,y_m}+\cdots$$  \tag{12.24}

Retaining a large number of terms in this series, with a view to increasing the accuracy, is impractical, due to the rapid increase of the complexity of the involved derivatives of the right-hand-side function f(t,y). The Runge–Kutta methods follow instead another leading idea: to construct solvers depending on the values of f(t,y), but not on derivatives thereof, and whose power-series representations in h should be equivalent with the exact expansion (12.24) up to highest possible terms, irrespective of the particular function f(t,y).

We represent y_{m+1} as a linear combination:

$$y_{m+1}=y_m+\sum_{i=1}^{p}w_i k_i.$$  \tag{12.25}

where w_i are weights and k_i take values proportional to f(t,y),

$$k_i=hf(\xi_i,\eta_i),$$

for p particular argument pairs from the vicinity of t_m and y_m:

$$\begin{cases}
\xi_i=t_m+\alpha_i h,\\
\eta_i=y_m+\displaystyle\sum_{j=1}^{i-1}\beta_{ij}k_j.
\end{cases}$$  \tag{12.26}

α_i, β_ij, and w_i are adjustable parameters, which need to be determined so as to maximize the agreement between the linear combination (12.25) and the Taylor series (12.24). Without restriction of generality, one can consider in all cases:

$$\alpha_1=0,\qquad \beta_{11}=0,\qquad \xi_1=t_m,\qquad \eta_1=y_m.$$  \tag{12.27}

which guarantees that hf(t_m,y_m) is always the first term in any Runge–Kutta propagator (12.25). We then have:

$$\begin{cases}
k_1=hf(t_m,y_m),\\
k_2=hf(t_m+\alpha_2h,y_m+\beta_{21}k_1),\\
k_3=hf(t_m+\alpha_3h,y_m+\beta_{31}k_1+\beta_{32}k_2),\\
\cdots
\end{cases}$$  \tag{12.28}

The above relations reveal the explicit algorithmic character of the Runge–Kutta methods, meaning that the various quantities are calculated in a straightforward manner based only on already-available quantities.