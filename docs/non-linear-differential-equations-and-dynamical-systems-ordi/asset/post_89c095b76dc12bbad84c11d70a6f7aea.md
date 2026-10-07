
## Unsteady, Non-Linear, and Chaotic Systems

and may be unsteady (4.508b), time independent or steady (4.580c), or a gradient (4.508d) system. The latter has a zero curl (4.509a) = (3.269c):

```
$$\frac{\partial g_n}{\partial x_m} = \frac{\partial g_m}{\partial x_n}, \quad E = \Phi + \sum_{n=1}^{N} x_n^2, \quad (4.509, b)$$
```

and a conserved first integral (4.509b). The iterated map (Figure 4.29a) or chaos (Figure 4.29c) extend to any dimension the integral curves by a directrix hypersurface not tangent to them. The dependence on P parameters to be considered (4.510a):

```
$$\dot{x}_n = f(x_m, t; q_n), \quad (4.510a, b)$$
```

using a space of P + 2N consisting of the product of: (i) the phase space $(x_n, \dot{x}_n)$ with 2N dimensions (4.508a-d); and (ii) the parameter space with P dimensions (4.510a). The exposition on dynamical systems emphasized mechanical devices, electrical circuits, and other applications; of many theorems in dynamical systems theory only a few are simpler and more have been intuitive. The material covered includes: (i) decay, amplification, and oscillations in linear and non-linear, and undamped, and forced systems; (ii) multiple examples of singularities of the second-order; and (iii) a few of the most frequent bifurcations, with no attempt at a systematic classification. The point of degree of a few (sections 4.1-4.2 and Figures 4.1a-f) serve as examples of singularities (section 4.9 and Figures 4.3a-i). The non-linear resonance (sections 4.4-4.5) and damping or amplification of bifurcations (sections 4.6-7) gives examples of transition to turbulence (subsection 4.8.9) and also involves parametric resonance (section 4.3). The bifurcations of dynamical systems (sections 4.8-9) are an example of the qualitative theory of differential equations (NOTE 4.2), which is complementary to solution of differential equations [Table 4.6]; (ii) the analytical exact (approximate) solution of differential equations [NOTES 4.3(4.4)]; (iii) the numerical methods (NOTE 4.5).

## NOTE 4.2: Qualitative Theory of Differential Equations

The aim of the qualitative theory of differential equations is to obtain some properties of the solution without explicitly solving the equation. The main advantage of this approach is that the qualitative theory applies to wider classes of differential equations than those that can be solved. The examples of the qualitative theory of differential equations (section 9.1) include: (i) existence theorems stating that a certain class of functions provides at least one solution; (ii) unicity theorems stating initial or boundary conditions that ensure that the solution is unique; and (iii) regularity terms indicating properties of the solution, such as differentiability or continuity with regard to parameters. The bifurcations are an example of non-regularity and/or non-unicity, since beyond the bifurcation point several may exist and be stable or unstable. The stability or instability of solutions can be established (section 9.2) by the qualitative theory for fairly general classes of differential equations. The singularities of the differential equation or of its solutions may limit the methods of solution that can be applied. The qualitative methods are very useful for preliminary investigation of the properties of fairly wide classes of differential equations; the inherent limitation is the lack of quantitative results that are essential in many scientific and technical applications.

## TABLE 4.6: Methods of Solution of Differential Equations

| Method Name | I Qualitative | II Exact Analytical | III Approximate Analytical | IV Numerical |
| --- | --- | --- | --- | --- |
| error of computation or accuracy | not quantifiable | truncation | truncation + systematic | truncation + discretization |
| copes with singularities | generally | always | sometimes | seldom |
| gives properties of solution | most | all | some | depends on interpretation |
| domain of application | very large | small | intermediate | large |

> Note: The solution of differential equations is based on qualitative and quantitative methods; the methods may be numerical or analytic; the analytic methods may be exact or approximate.

## NOTE 4.3: Exact Analytical Solutions of Differential Equations

In principle, the exact analytical solution of a differential equation should contain all properties with arbitrary accuracy. It must be ensured that what is obtained is the general integral that contains all particular integrals; if there are special integrals not included in the general integral they need to be investigated. An exact analytical solution has to be computed, and there are truncation errors that can be reduced by using more digits. The exact analytical solutions of some differential equations may be obtained in finite terms using only elementary functions. Wider classes of differential equations may still be amenable to exact analytical solution but only in terms of series, parametric integrals, continued fractions, infinite products, or other representations raising convergence issues (section 9,4–9.9). These solutions enlarge the class of ordinary functions to the special functions, e.g. hypergeometric, Legendre, Chebychev, Bessel, Hermite, etc., each having an associated theory that may be quite extensive (notes 9.1–9.47). The exact analytical solutions provide the most detailed understanding of the phenomena and processes described by a differential equation; however, the classes of differential equations amenable to analytical solution are limited and other methods are needed.

## NOTE 4.4: Analytical Approximations to the Solution of Differential Equations

If a differential equation in its general form has no known exact solution, it may be possible to simplify some terms so that it falls into one of the classes to which analytical methods apply. This introduces a systematic error associated with the approximation(s) made or term(s) omitted, in addition to the truncation error of computation. An example is the method of parametric expansions (section 4.5) that transforms a nonlinear equation into a sequence of linear equations solvable by recurrence. The approximation may also have limitations, for example the parametric solutions often can be obtained without excessive labor only for the lowest orders. They may also raise questions of validity, such as convergence. It may happen that the analytical solution of a differential equation can be obtained in finite terms using elementary functions whereas the exact analytical solution would require infinite expansions or special functions. The interpretation of the approximate analytical solution should take into account all the consequences of the approximation (i) properties that are not valid but due to the approximation; (ii) the possibility that other solutions are excluded by the assumptions made. The approximate analytical solution of a differential equation is an intermediate compromise: (a) the analytics solution (note 4.3) that is more accurate but may be more complex or unavailable for the differential equation (note 4.5) that will apply to wider classes of differential equations, while raising more issues.

## NOTE 4.5: Numerical Solution of Differential Equations

The chief attraction of numerical methods is that they provide quantitative solutions of the widest classes of differential equations, and in many cases are the only option available. Numerical methods can: (i) deceptively simple to apply; (ii) often much harder to justify fully than an analytic method; and (iii) almost always lead to some numbers at the end (except for overflows or underflows). When applying a numerical method, ensure that: (i) the problem has a unique solution; (ii) the method converges to
