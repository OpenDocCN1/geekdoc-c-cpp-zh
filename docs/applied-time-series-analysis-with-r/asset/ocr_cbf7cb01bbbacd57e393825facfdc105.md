# ARMA Time Series Models

$k \in l$, where $b_1, b_2, b_m$ are constants. Thus, from Equation 3.37, it follows that $ho_k$ satisfies a $pth$-order linear homogeneous difference equation with constant coefficients for $k > 0$. The general solution to the difference equation in Equation 3.44 is well known (see Brock and Davis, 1991). Specifically, if $g_k$ satisfies Equation 3.44 for $k > 0$,

```
$g_k = \sum_{i=1}^{v} \sum_{j=0}^{m_i} C_{ij}r_i^{-k}$
```

where the $r_i$ are the roots of the characteristic equation

```
$1 - b_1z - b_2z^2 - \dots - b_mz^m = 0,$
```

$v$ is the number of distinct roots, $m_i$ is the multiplicity of $r_i$ (i.e., if $r_i$ is repeated once, $m_i=2$, and if $r_i$ is not repeated, then $m_i=1$), $\sum_{i=1}^v m_i = m$, and $C_{ij}$ are uniquely determined by the initial conditions

```
$g_1 = h_1\ng_2 = h_2\nvdots\ng_m = h_m,$
```

where the $h_i$ are constants. When there are no repeated roots, Equation 3.37 simplifies to

```
$g_k = C_1r_1^{-k} + C_2r_2^{-k} + \dots + C_mr_m^{-k}.
```

From Equations 3.38 and 3.45, it follows that for an AR($p$) model,

```
$ho_k = \sum_{i=1}^{v} \sum_{j=0}^{m_i-1} C_{ij}r_i^{-k},$
```

where

```
$$\sum_{i=1}^{v} m_i = p,$
```

and the initial conditions are given by

```
$ho_k = \phi_1\rho_{k-1} + \dots + \phi_p\rho_{k-p},$
```