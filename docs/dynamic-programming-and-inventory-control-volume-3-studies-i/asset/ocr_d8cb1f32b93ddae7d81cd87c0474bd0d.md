A second example is the Gamma-Gamma model in which

(12.6.11) $$f(x, \lambda) = \frac{\lambda^x x^{k-1} \Gamma(k+a)}{(x+\lambda)^{k+a} \Gamma(a) \Gamma(k)}.$$

This probability density can be obtained by combining a Gamma probability density

$$\psi(x, y) = \frac{y^x x^{k-1} \exp^{-y}}{\Gamma(k)},$$

with another Gamma probability density

$$g(y, \lambda) = \frac{\lambda^a y^{a-1} \exp^{-y\lambda}}{\Gamma(a)}.$$

The probability density (12.6.11) is scalable if \(\rho(\lambda, x) = \lambda + x\). The functions \(q(\lambda), f(x), U(x)\) are defined by

(12.6.12) $$q(\lambda) = \lambda, \quad f(x) = \frac{x^{k-1} \Gamma(k+a)}{(1+x)^{k+a} \Gamma(a) \Gamma(k)}, \quad U(x) = 1+x.$$

Let us now show how the scalability property can be used to reduce the dimension of Bellman equation to 1.

Equation (12.6.7) is written as

(12.6.13) $$u(x, \lambda) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int u(\eta - \zeta, \rho(\lambda, \zeta)) f(\zeta, \lambda) d\zeta \right].$$

Replacing \(f(\zeta, \lambda)\) we get

$$u(x, \lambda) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int u(\eta - \zeta, \rho(\lambda, \zeta)) \frac{f\left(\frac{\zeta}{q(\lambda)}\right)}{q(\lambda)} d\zeta \right].$$

We can find a solution of the form

$$u(x, \lambda) = v\left(\frac{x}{q(\lambda)}\right) q(\lambda),$$

with \(v(x)\) solution of

(12.6.14) $$v(x) = hx^+ + px^- - cx + \inf_{\eta \ge x} \left[ c\eta + \alpha \int v\left(\frac{\eta - \zeta}{U(\zeta)}\right) U(\zeta) f(\zeta) d\zeta \right],$$

which is a one-dimensional problem.