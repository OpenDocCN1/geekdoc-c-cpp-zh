![](bbox=[0.12, 0.12, 0.88, 0.31])

FIGURE 4. Evolution of the magnitude of the first Fourier mode of the spectral scheme (3.1), with δ = .022, N = 128 and single-mode initial condition (1.5), showing repeated, approximate recurrences at regular time intervals with rapid decay of the recurrence strength.

We recall that KdV (1.1) is equivalent to the to the zero-curvature condtion,

```
(4.1)    S_t = T_x + T S - S T ,
```

where

```
S = ( i k   u ; -1/(6δ²)  -i k ),    T = ( -1/6 u_x - i/3 u k   1/3 u² - δ² u_xx - 2 i δ² u_x k + 4 δ² u k² ; 1/(18δ²) u - i/3 k²   1/6 u_x + i/3 u k - 8 i δ² k³ ) ,
```

and k is a space- and time-independent parameter. The zero-curvature condition (4.1) is equivalent to the equality of mixed derivatives (ψ_xt = ψ_tx) for simultaneous solutions of

```
ψ_x = S ψ ,      ψ_t = T ψ .
```

These two linear equations are used to construct the Inverse-Scattering Transform, which makes integrability operational, but we do not discuss this here.

The spatially discrete equation

```
(4.2)    ψ_{n+1} = S_n ψ_n , where   S_n = ( z   U_n ; α   z^{-1} ) ψ_n ,
```

with

```
(4.3)    U_n = h u_n , α = h/(6δ²) , z = 1 + i k h + O(h²) = e^{i k h} ,
```

is a forward-difference discretization of the linear differential equation (in x) above. With the time-dependence equation

```
(4.4)    d/dτ ψ_n = T_n ψ_n ,
```