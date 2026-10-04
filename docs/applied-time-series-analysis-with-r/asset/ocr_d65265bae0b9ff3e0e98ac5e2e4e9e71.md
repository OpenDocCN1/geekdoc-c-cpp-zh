# Vector-Valued (Multivariate) Time Series 441

$1/r_i$ can be chosen to be $\mathbf{u}_i' = (r^{i-1} r^{i-2} \dots r_1)$, and we have $\Phi = \mathbf{UDU}^{-1}$ where $\mathbf{U} = [\mathbf{u}_1 \mathbf{u}_2 \dots \mathbf{u}_p]$ and

```
$\mathbf{D} = \text{diag} \left( \begin{matrix} \frac{1}{r_1} & & \ & \frac{1}{r_2} & \ & & \frac{1}{r_p} \end{matrix} \right)$
```

that is, a diagonal matrix with the listed elements along the diagonal. Note that due to the choice of eigenvectors, the last row of $\mathbf{U}$ is a vector of 1s. For our purposes, we arrange $\mathbf{D}$ and $(\mathbf{U})$ such that $|\eta_1| \geq |r_2| \geq \dots$

Defining $\Psi_t = \mathbf{U}^{-1}\mathbf{X}_t$ (i.e., $\mathbf{X}_t = \mathbf{U}\Psi_t$), the state-space model can be rewritten so that the rows of $\mathbf{U}^{-1}$ provide the filter coefficients needed to calculate the components.

# 10.6.7.1 Revised State-Space Model

State Equation: $\mathbf{X}_t = \Phi\mathbf{X}_{t-1} + \mathbf{V}_t$, becomes $\mathbf{X}_t = \mathbf{UDU}^{-1}(\mathbf{U}\Psi_{t-1}) + \mathbf{V}_t$, where $\mathbf{U}\Psi_t = \mathbf{UD}\Psi_{t-1} + \mathbf{U}\mathbf{V}_t$,

```
$\Psi_t = \mathbf{D}\Psi_{t-1} + \mathbf{U}^{-1}\mathbf{V}_t$ (new state equation). (10.63)
```

Observation: In this case $Y_t = (0 \ 0 \dots 0 \ 1) \mathbf{X}_t$, becomes $Y_t = (0 \ 0 \dots 0 \ 1) \Psi_t$, that

```
$\Y_t = (11 \dots 1) \Psi_t = \sum_{j=1}^p \Psi_j$ (new observation equation). (10.64)
```

Each additive component of $\Psi_t$ can be thought of as a "state variable" that is unobserved. The $\psi_j$ are the desired additive components except for the fact that some of the $\psi_{ij}$ may be complex. We consider two cases.

# 10.6.7.2 $\Psi_t$ Real

If a root of the characteristic equation, $r_{ij}$, is real, then the corresponding $\psi_{ij}$ $t=1, \dots, n$ is a sequence of real. From Equation 10.63, it follows in this case

```
$\Psi_j = \frac{1}{r_j}\Psi_{t-1,j} + c_j a_t$,
```

where $c_j$ is the last value in the $j$th row of $\mathbf{U}^{-1}$. Thus, $\psi_j$ follows an AR(1) model, and the corresponding system frequency is 0 or 0.5 depending on whether $r_j$ is positive or negative, respectively. Since $\Psi_t = \mathbf{U}^{-1}\mathbf{X}_t$, the additive component associated with the current realization can be obtained numerically by multiplying the $j$th row of $\mathbf{U}^{-1}$ by $\mathbf{x}_t$, where $\mathbf{x}_t$ is the realization written