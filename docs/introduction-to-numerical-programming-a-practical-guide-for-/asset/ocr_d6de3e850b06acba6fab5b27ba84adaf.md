the function arguments may be expressed as x = a + qh and the products occurring in the coefficients of the Lagrange polynomial can be rewritten as

$$\prod_{j\neq i}^{n}(x - x_j) = h^{n-1}\prod_{j\neq i}^{n}[q - (j - 1)],$$

$$\prod_{j\neq i}^{n}(x_i - x_j) = h^{n-1}\prod_{j\neq i}^{n}(i - j) = (-1)^{n-i}h^{n-1}\prod_{j=1}^{i-1}(i - j)\prod_{j=i+1}^{n}(j - i)$$ 

$$= (-1)^{n-i}h^{n-1}(i - 1)!(n - i)!$$

The Lagrange polynomial thus takes the form

$$P_{n-1}(x) = \sum_{i=1}^{n}\frac{\prod_{j\neq i}^{n}[q - (j - 1)]}{(-1)^{n-i}(i - 1)!(n - i)!}f_i,\qquad (10.7)$$

and the following approximation to the integral is obtained:

$$\int_{a}^{b}f(x)dx \approx \int_{a}^{b}P_{n-1}(x)dx = \sum_{i=1}^{n}A_i f_i,\qquad (10.8)$$

The coefficients $A_i$ weighting the integrand values can be successively transformed,

$$A_i = \int_{a}^{b}\frac{\prod_{j\neq i}^{n}[q - (j - 1)]dx}{(-1)^{n-i}(i - 1)!(n - i)!} = \frac{h\int_{0}^{n-1}\prod_{j\neq i}^{n}[q - (j - 1)]dq}{(-1)^{n-i}(i - 1)!(n - i)!},\qquad (10.9)$$

and, by factoring out explicitly the extent of the integration interval, $A_i = (b-a)H_i$, the classical Newton–Cotes quadrature formula results:

$$\int_{a}^{b}f(x)dx \approx (b - a)\sum_{i=1}^{n}H_i f_i.\qquad (10.10)$$

The corresponding Cotes coefficients are given by

$$H_i = \frac{\int_{0}^{n-1}\prod_{j\neq i}^{n}[q - (j - 1)]dq}{(-1)^{n-i}(i - 1)!(n - i)!(n - 1)},\qquad i = 1,2,\dots,n.\qquad (10.11)$$

It should be noted that, as per definition, the Cotes coefficients do neither depend on the integrated function, nor on the integration interval. In addition, they satisfy:

$$\sum_{i=1}^{n}H_i = 1,\quad H_i = H_{n-i+1}.\qquad (10.12)$$

The first property, reflecting the normalization of the coefficients, may be demonstrated by simply considering the particular integrand $f(x)\equiv 1$ in the general Newton–Cotes formula 10.10, while the second property, implying the symmetry of the coefficient sequence with respect to its median, follows from the