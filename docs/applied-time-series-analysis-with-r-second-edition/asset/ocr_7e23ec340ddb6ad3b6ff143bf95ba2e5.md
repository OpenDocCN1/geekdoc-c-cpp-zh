Let $Y_t$ be a stationary univariate, zero-mean AR($p$) process given by $Y_t = \phi_1 Y_{t-1} + \cdots \phi_p Y_{t-p} + a_t$. A state-space representation is obtained using the (vector) equations

$X_t = \Phi X_{t-1} + V_t$  (state equation),
$Y_t = (0\ 0\ \dots\ 1) X_t$  (observation equation),

![](bbox=[0.22, 0.27, 0.75, 0.57])

# FIGURE 10.11

Realization of length $n = 75$ from the AR(1) model for $X_t$ in Example 10.9 (solid line) along with the corresponding realization (dashed line) from the AR(1)-plus-noise model $Y_t$.

where

$X_t = \begin{pmatrix} Y_{t-p+1} \\ Y_{t-p+2} \\ \vdots \\ Y_t \end{pmatrix},\quad \Phi = \begin{pmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & \vdots & \vdots & & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ \phi_p & \phi_{p-1} & \phi_{p-2} & \cdots & \phi_1 \end{pmatrix},\quad V_t = \begin{pmatrix} 0 \\ 0 \\ \vdots \\ a_t \\ 0 \\ 1 \end{pmatrix}$

Note that in this case, $v = p$, $w = 1$, and $W_t = 0$. This example illustrates the fact that the AR(1)-type form of the state equation does not place the limitations on the applicable settings that might be expected.

If $Y_t$ satisfies the zero-mean VAR($p$) model $Y_t = \Phi_1 Y_{t-1} + \cdots \Phi_p Y_{t-p} + a_t$, then a state-space formulation is obtained using the following equations