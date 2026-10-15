The recursive relation enabling the optimal evaluation of $R_{k,0}$, by implicitly reusing the previously calculated integrand values (avoiding redundant evaluations), reads:

$R_{k,0} = \frac{1}{2} \left[ R_{k-1,0} + h_{k-1} \sum_{i=1}^{n_{k-1}} f\left(a + (i - 1/2)h_{k-1}\right) \right], \quad k = 1,2,\dots,k_{\max}, \qquad (10.40)$

and it represents the exact transcription of Equation 10.30. Consistently, the first two approximations yielded by Simpson’s formula are:

$R_{1,1} = \frac{h_1}{3} \left[ f(a) + 4f(a + h_1) + f(b) \right] = \frac{4R_{1,0} - R_{0,0}}{3},$

$R_{2,1} = \frac{h_2}{3} \left[ f(a) + 4f(a + h_2) + 2f(a + 2h_2) + 4f(a + 3h_2) + f(b) \right]$

$= \frac{4R_{2,0} - R_{1,0}}{3}.$

Then, the general relationship 10.33 between the approximations based on Simpson’s formula and the trapezoidal rule takes the form:

$R_{k,1} = \frac{4R_{k,0} - R_{k-1,0}}{3} = \frac{4R_{k,0} - R_{k-1,0}}{4 - 1}, \quad k = 1,2,\dots,k_{\max}. \qquad (10.41)$

Pursuing the idea of recursively increasing the order of the basic Newton–Cotes formula, the first approximation of the next quadrature scheme is expected to rely on the nodes resulting by dividing the characteristic subintervals of the first approximation of Simpson’s formula, $R_{1,1}$, or, equivalently, on the nodes of the second approximation, $R_{2,1}$. This requirement is intrinsically met by the five-point Boole’s formula* (Boole and Moulton 2003), which essentially approximates the integrand by the fourth-order Lagrange interpolation polynomial:

$\int_{x_1}^{x_5} f(x) dx = \frac{2h}{45} \left[ 7f_1 + 32f_2 + 12f_3 + 32f_4 + 7f_5 \right] - \frac{8h^7 f^{(6)}(\xi)}{945}. \qquad (10.42)$

This first approximation based on Boole’s formula can be expressed in terms of the integration step $h_2$ corresponding to two consecutive halving iterations of the total integration interval $[a, b]$,

$R_{2,2} = \frac{2h_2}{45} \left[ 7f(a) + 32f(a + h_2) + 12f(a + 2h_2) + 32f(a + 3h_2) + 7f(b) \right], \qquad (10.43)$

and, moreover, can be related to the first two approximations provided by Simpson’s formula:

$R_{2,2} = \frac{16R_{2,1} - R_{1,1}}{15} = \frac{4^2 R_{2,1} - R_{1,1}}{4^2 - 1}. \qquad (10.44)$

It can be readily anticipated that the increase of the order of the basic quadrature scheme implies doubling the number of characteristic subintervals from $2^k$ (2 for Simpson’s formula) to $2^{k+1}$ (4 for Boole’s formula) and, inherently, doubling the order of the Lagrange interpolation polynomial by which the integrand is approximated. Consequently, except for the initial approximation $R_{0,0}$, all superior ones are based on integration grids with odd numbers of nodes, $(2^k + 1)$.

* Mistakenly referred to as “Bode’s formula.”