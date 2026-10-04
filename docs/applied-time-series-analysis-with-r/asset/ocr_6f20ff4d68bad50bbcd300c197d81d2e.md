# Vector-Valued (Multivariate) Time Series 447

First, we define

```
$$x_t^{(j)} = \left( \begin{array}{c} \Psi_{t-1,j} + \Psi_{t-1,j}^* \ \Psi_{ij} + \Psi_{ij}^* \end{array} \right), \quad (10A.4)$
```

and note from Equation 10.63 that $\Psi_{ij}$ and $\Psi_{ij}^*$ are both complex-valued AR(1) realizations, that is,

```
$$ \Psi_{ij} = \frac{1}{r_j}\Psi_{t-1,j} + c_j a_t \n \Psi_{ij}^* = \frac{1}{r_j}\Psi_{t-1,j}^* + c_j^* a_t \quad (10A.5)$ $$
```

where $c_j$ and $c_j^*$ are the last values in the $j$th row and $(j+1)$st row, respectively, of $\mathbf{U}^{-1}$. From Equations 10A.4 and 10A.5.

```
$$x_t^{(i)} = \left( \begin{array}{c} \Psi_{t-1,j} + \Psi_{t-1,j}^* \ \Psi_{ij} + \Psi_{ij}^* \end{array} \right)$ \n = \Psi_{t-1,j} + \Psi_{t-1,j}^* \n = \frac{1}{r_j}\Psi_{t-1,j} + \frac{1}{r_j}\Psi_{t-1,j}^* + (c_j + c_j^*)a_t \n = \left( \begin{array}{cc} 1 & 1 \ \frac{1}{r_j} & \frac{1}{r_j} \end{array} \right) \Psi_{t-1,j} + \left( \begin{array}{c} 0 \ 1 \end{array} \right)ca_t \n = \mathbf{C}\Psi_{t-1,j} + \left( \begin{array}{c} 0 \ 1 \end{array} \right)ca_t$ $$
```

where

```
$$ \mathbf{C} = \left( \begin{array}{cc} 1 & 1 \ \frac{1}{r_j} & \frac{1}{r_j^*} \end{array} \right), $$
```

```
$$ \Psi_{t-1,j} = \left( \begin{array}{c} \Psi_{t-1,j} \ \Psi_{t-1,j}^* \end{array} \right),$ $$
```