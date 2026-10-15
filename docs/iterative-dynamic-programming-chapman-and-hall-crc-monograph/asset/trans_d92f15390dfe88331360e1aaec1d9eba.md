

a coil inserted in the reactor. The heat and mass balances for the reaction A → B in such a CSTR are given by

```
V c_P ρ dT_R/dθ = q c_P ρ (T_0 − T_R) − V U* + (−ΔH) V R   (1.52)
```

```
V d c_A / dθ = q (c_A0 − c_A) − V R   (1.53)
```

where

+   c_A = concentration of species A leaving reactor
+   c_A0 = concentration of species A in feed stream
+   T_R = temperature of reactants leaving reactor
+   T_0 = temperature of feed stream to reactor
+   θ = time
+   V = volume of reactor
+   q = volumetric flow rate of feed and output streams
+   R = reaction rate term
+   −ΔH = heat of reaction
+   c_P = heat capacity
+   ρ = density
+   U* = heat transfer term corresponding to cooling coil in reactor

As shown by Lapidus and Luus [11], these equations may be put into dimensionless form and, through a choice of a convenient set of parameters, transformed into the equations

```
dx_1/dt = −(2 + u)(x_1 + 0.25) + (x_2 + 0.5) exp[25 x_1 / (x_1 + 2)]   (1.54)
```

```
dx_2/dt = 0.5 − x_2 − (x_2 + 0.5) exp[25 x_1 / (x_1 + 2)]   (1.55)
```

where x_1 represents deviation from dimensionless steady-state temperature and x_2 represents deviation from dimensionless steady-state concentration. In the present work, the initial conditions x_1(0) = 0.09 and x_2(0) = 0.09 are used. We consider the case where the control u is unbounded. The optimal control problem is to determine u in the time interval 0 ≤ t < t_f that will minimize the performance index

```
I = ∫_0^{t_f} (x_1^2 + x_2^2 + 0.1 u^2) dt   (1.56)
```

where the dimensionless final time t_f is specified as 0.78. As was shown by Luus and Cormack [18], this system exhibits a local minimum I = 0.24425 and a global minimum I = 0.133094 when Pontryagin’s maximum principle is used, and the resulting boundary value problem is solved by control vector iteration. Therefore, this system is an interesting test problem for optimal control procedures.

### 1.8.3 Photochemical reaction in CSTR

A more challenging problem of higher dimension consists of a photochemical reaction in an isothermal CSTR, as formulated by Jensen [10] and used for optimal control studies in [11] and [25]. It served as an ideal system for testing iterative dynamic programming for moderate dimensional nonlinear optimal control problems [13]. The mechanism for the reactions among the species $A,B,C,D,E,F,$ and $G$ is given by

$$\begin{aligned}
A+B &\xrightarrow{k_1} 2D\\
C+B &\xrightarrow{k_2} CB\\
CB+B &\xrightarrow{k^*} 3E\\
E+D &\xrightarrow{k_3} 2F\\
A+F &\xrightarrow{k_4} 2G
\end{aligned}$$

where the fifth reaction is photochemical and its rate is proportional to the square root of the light intensity. The intermediate compound $CB$ is postulated to be present in immeasurably small quantities, so it satisfies the stationary condition, namely $d(CB)/dt=0$. By using a convenient set of parameters, Lapidus and Luus [11] showed that the system is described by the eight differential equations

$$\begin{aligned}
\frac{dx_1}{dt} &= u_4-qx_1-17.6x_1x_2-23x_1x_6u_3 \tag{1.57}\\
\frac{dx_2}{dt} &= u_1-qx_2-17.6x_1x_2-146x_2x_3 \tag{1.58}\\
\frac{dx_3}{dt} &= u_2-qx_3-73x_2x_3 \tag{1.59}\\
\frac{dx_4}{dt} &= -qx_4+35.2x_1x_2-51.3x_4x_5 \tag{1.60}\\
\frac{dx_5}{dt} &= -qx_5+219x_2x_3-51.3x_4x_5 \tag{1.61}\\
\frac{dx_6}{dt} &= -qx_6+102.6x_4x_5-23x_1x_6u_3 \tag{1.62}\\
\frac{dx_7}{dt} &= -qx_7+46x_1x_6u_3 \tag{1.63}\\
\frac{dx_8}{dt} &= 5.8(qx_1-u_4)-3.7u_1-4.1u_2+q(23x_4+11x_5+28x_6+35x_7)-5u_3^2-0.099 \tag{1.64}
\end{aligned}$$

where

+   $x_1,x_2,\ldots,x_7$ = weight fractions of species $A$, $B$, $\ldots$, $G$
+   $k_1,k_2,\ldots,k_4$ = reaction rate constants
+   $u_1,u_2,u_4$ = inlet feed rate of pure components $A$, $B$ and $C$
+   $u_3$ = square root of light intensity

q = u₁ + u₂ + u₄ is the total flow rate of inlet streams.

The initial state is

x(0) = [0.1883  0.2507  0.0467  0.0899  0.1804  0.1394  0.1046  0.0]ᵀ.  (1.65)

The constraints on the control variables are

0 ≤ u₁ ≤ 20  (1.66)

0 ≤ u₂ ≤ 6  (1.67)

0 ≤ u₃ ≤ 4  (1.68)

0 ≤ u₄ ≤ 20.  (1.69)

The optimal control problem is to choose u₁, u₂, u₃, and u₄ in the time interval 0 ≤ t < t_f, so that the performance index

I = x₈(t_f),  (1.70)

which gives the economic benefit, is maximized. The final time t_f is specified as 0.2 h. This problem served as a good test problem for iterative dynamic programming [13].

### 1.8.4 Production of secreted protein in a fed-batch reactor

Determination of the optimal feed rate into a fed-batch reactor to yield the maximum amount of the desired product is a very difficult optimal control problem. The model for the production of secreted protein in a fed-batch reactor presented by Park and Ramirez [24] has been used by several researchers in developing robust methods for handling problems of this nature. The differential equations describing the reactor are

dx₁/dt = g₁(x₂ − x₁) − (u/x₅)x₁  (1.71)

dx₂/dt = g₂x₃ − (u/x₅)x₂  (1.72)

dx₃/dt = g₃x₃ − (u/x₅)x₃  (1.73)

dx₄/dt = −7.3g₃x₃ − (u/x₅)(20 − x₄)  (1.74)

dx₅/dt = u  (1.75)

where

g₃ = 21.87x₄ / [(x₄ + 0.4)(x₄ + 62.5)]  (1.76)

```
g₂ = \frac{x₄ e^{-5 x₄}}{(x₄ + 0.1)} \tag{1.77}
```

```
g₁ = \frac{4.75 g₃}{(g₃ + 0.12)} \tag{1.78}
```

and

+   x₁ = level of secreted SUC-s2 in culture, arbitrary units/L
+   x₂ = level of total SUC-s2 in culture, arbitrary units/L
+   x₃ = culture cell density, g/L
+   x₄ = culture glucose level, g/L
+   x₅ = culture volume, L
+   u = feed flow rate, L/h.

The initial condition, as given by Park and Ramirez [24], is

```
x(0) = [0.0  0.0  1.0  5.0  1.0]ᵀ. \tag{1.79}
```

It should be noted that the three algebraic equations have been arranged in the “reverse” order so that they can be solved readily by direct substitution. Frequently, there are situations where the set of algebraic equations can not be rearranged to provide a solution in a straightforward manner. Therefore, in the next section we examine methods of solving a general set of algebraic equations numerically.

The control is bounded by

```
0 ≤ u ≤ 2. \tag{1.80}
```

The performance index to be maximized is the total amount of the desired product at the final time, given by

```
I = x₁(t_f) x₅(t_f) \tag{1.81}
```

where the final time t_f is specified as 15 h. Although there is only a scalar control variable, the optimal control policy is quite difficult to obtain, and therefore this problem is a good test for optimization procedures [20].

These four systems provide the reader a feel for the types of problems we wish to consider in this book. In later chapters a wider variety of systems, such as systems involving time delays, will be considered as well.

## 1.9 Solving algebraic equations

It is well known that the most efficient way of solving a set of linear algebraic equations is Gaussian elimination method, which consists of putting the equations into an echelon form and then using back-substitution to obtain the variables in reverse order. However, the solution of a set of nonlinear algebraic equations often requires some

Eq. (1.85) is a linear equation which can be easily solved by Gaussian elimination for δx and the next value of x is then chosen as

```
x^{j+1} = x^{j} + δx. (1.86)
```

It is noted that the partial derivatives are calculated in the presence of the simple equality constraints, so that these are difficult to obtain analytically, because x_{n+1}, x_{n+2}, ..., x_N are functions of the particular variable under consideration. This is illustrated by the first example. Computationally, however, the partial derivatives are easily obtained by perturbing the particular variable, and we can write

```
∂f_j(x_1, x_2, ..., x_i, ..., x_N) / ∂x_i = [f_j(x_1, x_2, ..., x_i + h_i, ..., x_N) - f_j(x_1, x_2, ..., x_i - h_i, ..., x_N)] / (2 h_i) (1.87)
```

where h_i is taken as a very small perturbation such as 10^{-6} x_i if x_i ≠ 0.

One great advantage of this method is the very rapid convergence in the vicinity of the solution. There is also considerable freedom in choosing how many and which equations to include in each of the two groups. Generally we try to have as many equations as possible in the first group, so that we have the smallest number of difficult equations. Since this method is so simple to program, and does not encounter the types of problems reported by the various methods considered by Shacham [28], it should really be the “first” approach to try.

### 1.9.2 Numerical examples

All computations were performed in double precision on a Pentium/120 personal digital computer using WATCOM version 9.5 FORTRAN compiler. For all the examples the perturbation h_i for evaluating the derivatives was 10^{-6} x_i if x_i ≠ 0 and 10^{-10} if x_i = 0. The computation times reported were obtained by reading the clock at the beginning and at the end of the calculations and therefore include the time taken to write to the screen and to the output files. These computation times are given only to provide an approximate idea of the computational effort required. We choose several examples for which difficulties have been reported in the recent literature.

## Example 1

Let us consider the example involving the oxidation of sulphur dioxide to sulphur trioxide presented by Fogler [6] and studied by [28], [29], and [31], where the set of algebraic equations can be arranged into the two groups:

+   (a) Set of two simple equations

```
x_2 = (43260 x_1 + 105128) / (1.84 x_1 + 77.3) (1.88)
```
