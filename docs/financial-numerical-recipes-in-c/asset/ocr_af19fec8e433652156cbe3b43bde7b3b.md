where the critical stock prices solves

$$S = X - P_2 \left( S, X, \frac{2T}{3}, r, \sigma \right) = \overline{S}_{T/3}$$

$$S = X - p \left( S, X, \frac{T}{3}, r, \sigma \right) = \overline{S}_{2T/3}$$

The main issue in implementation of this formula (besides keeping the notation straight) is the evaluation of $P_3$, since it involves the evaluation of a trivariate normal cumulative distribution. The evaluation of $N_3()$ is described later, since it involves calls to external routines for numerical integration.

To solve for

$$S = X - p \left( S, X, \frac{T}{2}, r, \sigma \right) = \overline{S}_{\frac{T}{2}}$$

involves Newton steps. Define

$$g(S) = S - X + p \left( S, X, \frac{T}{2}, r, \sigma \right)$$

Iterate on S

$$S_i = S_i - \frac{g}{g'}$$

until g is equal to zero with some given tolerance.