If the estimated truncation error err exceeds the target value eps, the routine iteratively reduces ht according to Equation 12.48 and takes repeated propagation steps from the same initial condition until the precision criterion is met. The relative truncation error err is evaluated as maximum relative difference between the components of the solutions yt and yt2. Once err drops below eps, the trial propagation is accepted and the process exits from the step size scaling loop. Along with the effectively used step size ht, the routine also returns via ht1 a guess for the step size to be used at the next propagation step. In any case, an increase of more than 5 times of the step size is explicitly prevented.

A significantly improved efficiency is achieved in practice by using, instead of step halving for a single ODE solver, rather two embedded solvers of consecutive orders, p and p + 1, sharing the same defining coefficients and enabling the estimation of the truncation error in a single process. Such a scheme is the Runge–Kutta–Fehlberg method (Fehlberg 1966, 1970), in which, two particular O(h⁵) and O(h⁶) Runge–Kutta methods are used jointly:

```
ỹₘ₊₁ = yₘ + 25/216 k₁ + 1408/2565 k₃ + 2197/4104 k₄ − 1/5 k₅,   (12.49)
yₘ₊₁ = yₘ + 16/135 k₁ + 6656/12,825 k₃ + 28,561/56,430 k₄ − 9/50 k₅ + 2/55 k₆.   (12.50)
```

The common defining coefficients are

```
k₁ = h f(tₘ, yₘ),   (12.51)
k₂ = h f( tₘ + 1/4 h, yₘ + 1/4 k₁ ),
k₃ = h f( tₘ + 3/8 h, yₘ + 3/32 k₁ + 9/32 k₂ ),
k₄ = h f( tₘ + 12/13 h, yₘ + 1932/2197 k₁ − 7200/2197 k₂ + 7296/2197 k₃ ),
k₅ = h f( tₘ + h, yₘ + 439/216 k₁ − 8 k₂ + 3680/513 k₃ − 845/4104 k₄ ),
k₆ = h f( tₘ + 1/2 h, yₘ − 8/27 k₁ + 2 k₂ − 3544/2565 k₃ + 1859/4104 k₄ − 11/40 k₅ ).
```

An estimate of the truncation error results by subtracting Equation 12.49 from Equation 12.50:

```
Δₘ₊₁ = yₘ₊₁ − ỹₘ₊₁ = 1/360 k₁ − 128/4275 k₃ − 2197/75,240 k₄ + 1/50 k₅ + 2/55 k₆ + O(h⁶),   (12.52)
```

and also provides, according to Equation 12.44, an approximation for the relative truncation error. These error estimates are obtained at each step by six evaluations of the right-hand-side function f, instead of double as many (3 × 4) in the case of applying step halving for the fourth-order Runge–Kutta method.

The overall structure, parameters, and functionality of the routine RKFehlberg given in Listing 12.6 are similar with those of function RKadapt. The main differences concern the replacement of the three