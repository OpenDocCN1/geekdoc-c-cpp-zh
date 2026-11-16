the deformation gradient, the mixed variational formulations are categorized into two classes, the \( F \)-formulation and the \( \bar{F} \)-formulation [99]. In this section, we recall the \( F \)-formulation; for the \( \bar{F} \)-formulation, the reader is referred to [17, 99, 188] and references therein.

The basic idea is to introduce a function \( \widehat{W} \) such that \( W(x, F) = \widehat{W}(x, F, J) \) when \( J = \det F \), and its partial Legendre transformation,

```
\(\widehat{W}^*(x, F, \bar{q}) = \max_{\bar{q}} \{ \bar{q}(J - 1) - \widehat{W}(x, F, J) \}.\)
```

Provided that \( \widehat{W} \) is convex in the argument \( J \), the following duality relation holds:

```
\(\widehat{W}(x, F, J) = \max_{\bar{q}} \{ \bar{q}(J - 1) - \widehat{W}^*(x, F, \bar{q}) \}.\) (12.4)
```

Direct substitution of relation (12.4) in the principle of minimum potential energy (12.1)-(12.2) renders the following alternative mixed variational principle:

```
\(\widehat{\Pi}(u, \bar{p}) = \min_{v \in \mathcal{K}} \max_{\bar{q} \in \mathcal{Q}} \widehat{\Pi}(v, \bar{q}),\) (12.5)
```

with

```
\(\begin{aligned} \widehat{\Pi}(v, \bar{q}) &= \int_{\Omega} \{ -\widehat{W}^*(x, F(v), \bar{q}) + \bar{q}[\det F(v) - 1] \} \, dx \\ &\quad - \int_{\Omega} f \cdot v \, dx - \int_{\Gamma^u} t \cdot v \, ds. \end{aligned}\) (12.6)
```

In the above expression, \( \mathcal{Q} \) denotes the set of square-integrable scalar functions and the maximizing scalar field \( \bar{p} \) is directly related to the equilibrium Cauchy hydrostatic pressure field \( p := \text{tr } \sigma \) via [99]

```
\( p = \bar{p} - \frac{1}{3 \det F} \frac{\partial \widehat{W}^*}{\partial F}(x, F, \bar{p}) : F.\)
```

The weak form of the Euler-Lagrange equations associated with the variational principle (12.5)-(12.6) reads as

```
\(\begin{aligned} G^u(v, \bar{q}; \delta v) = \int_{\Omega} \left[ -\frac{\partial \widehat{W}^*}{\partial F}(x, F(v), \bar{q}) + \bar{q} \, \text{adj}(F^T(v)) \right] : \nabla(\delta v) \, dx \\ \quad - \int_{\Omega} f \cdot \delta v \, dx - \int_{\Gamma^u} t \cdot \delta v \, ds = 0 \quad \forall \delta v \in \mathcal{K}^0, \end{aligned}\)
```

```
\( G^{\bar{q}}(v, \bar{q}; \delta \bar{q}) = \int_{\Omega} \left[ \det F(v) - 1 - \frac{\partial \widehat{W}^*}{\partial \bar{q}}(x, F(v), \bar{q}) \right] \delta \bar{q} \, dx = 0 \quad \forall \delta \bar{q} \in \mathcal{Q},\)
```

where the test field \( \delta \bar{q} \) is the variation of \( \bar{q} \), and \( \text{adj}(\cdot) \) stands for the adjugate operator.