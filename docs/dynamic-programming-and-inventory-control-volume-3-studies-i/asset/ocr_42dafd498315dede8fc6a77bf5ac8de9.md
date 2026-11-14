This implies

\(-\frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) - \lambda \int_0^{+\infty} m(x+\xi)\mu(\xi)d\xi = 0, x \in (s, +\infty)\)
\(m(x) = 0, x \le s \quad m'' \text{ discontinuous in } S\)

and we must have \(m \ge 0\) with the normalisation property \(\int_s^{+\infty} m(x)dx = 1\). Note that the condition

\(\frac{\sigma^2}{2}(m'(S+0) - m'(S-0) + m'(S) + \lambda) \int_s^{+\infty} m(x) \left( \int_{x-s}^{+\infty} \mu(\xi)d\xi \right) dx = 0,\)

is not an additional condition. It follows from (15.6.6) and the normalisation properties. So (15.6.6) and the normalisation properties constitute the equation for the invariant measure. Let us prove that (15.6.2) is a solution and the unique one. We can check that \(\exp \beta_2 x\) satisfies the integro-differential equation (15.6.6). It goes to 0 as \(x \to +\infty\). It cannot be the solution on \((s, +\infty)\), but if we impose the value at \(S\) equal to \(\exp \beta_2 S\) then it is the unique solution on \((S, +\infty)\). Note that imposing the normalisation condition or the value at a point are equivalent. So we may fix the value at \(S\) equal to \(\exp \beta_2 S\). There can then be only one solution of (15.6.6) which is \(C^2\) on \((s, +\infty)\) and vanishes at \(\infty\). This follows from maximum principle considerations.

We can then write the equation on \((s, S)\) as follows

\(-\frac{\sigma^2}{2}m''(x) - \nu m'(x) + \lambda m(x) - \lambda \int_0^{S-x} m(x+\xi)\mu(\xi)d\xi\)
\(= \lambda \exp \beta_2 x \int_{S-x}^{+\infty} \exp \beta_2 \xi \mu(\xi)d\xi, \quad s < x < S\)
\(m(s) = 0; \quad m(S) = \exp \beta_2 S\)

This equation can have only one solution, from maximum principle considerations. If we make the change of unknown function.

\(m(x) = v(x) \exp \beta_2 x,\)

then we obtain an equation for \(v(x)\), namely

\(-\frac{\sigma^2}{2}v''(x) - (\nu + \beta_2 \sigma^2)v'(x) + \lambda v(x)\tilde{\mu}(\beta_2)\)
\(-\lambda \int_0^{S-x} v(x+\xi) \exp \beta_2 \xi \mu(\xi)d\xi = \lambda \int_{S-x}^{+\infty} \exp \beta_2 \xi \mu(\xi)d\xi,\)
\(v(s) = 0, \quad v(S) = 1\)

Considering \(w(x) = v'(x)\) we get, taking into account the value \(v(S) = 1\)

\(-\frac{\sigma^2}{2}w''(x) - (\nu + \beta_2 \sigma^2)w'(x) + \lambda w(x)\tilde{\mu}(\beta_2) - \lambda \int_0^{S-x} w(x+\xi) \exp \beta_2 \xi \mu(\xi)d\xi = 0,\)

and if we write

\(w(x) = \exp -\beta_2 x z(S-x),\)

we see that \(z(x) = \Gamma(x)\). Collecting results, we obtain that \(\tilde{m}^{n,s}(x)\) is a solution of (15.6.6) with all conditions satisfied, with of course a different value at \(S\). Therefore \(m^{n,s}(x)\) is the unique invariant measure satisfying the regularity properties, the boundary conditions and the normalization property.