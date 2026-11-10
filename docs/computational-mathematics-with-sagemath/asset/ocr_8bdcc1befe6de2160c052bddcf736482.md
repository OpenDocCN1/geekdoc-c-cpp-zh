![](bbox=[0.175, 0.078, 0.813, 0.356])

FIGURE 14.2 – Interpolation using a degree-10 polynomial (thin line) of the function x ↦ 1/(1 + x²) (thick line) at 11 points equally spaced on [−10, 10]. Runge's phenomenon appears at endpoints.

with

$$I_1 = I_a^{(a+b)/2}(f) + I_{(a+b)/2}^{b}(f)$$

and we stop the subdivision process when $|I_0 - I_1|$ is small enough compared to $I_0$ with the required precision. Here comes into play the method order: for a quadrature rule of order $n$, dividing the interval in 2 will divide the theoretical error by $2^n$, i.e., without taking into account roundoff errors.

One of the interpolation methods available within Sage is the Gauss-Legendre method. In this method, the $n$ integration points are the roots of the Legendre polynomial of degree $n$ (with a translated interval of definition to match the considered range $[a,b]$). The properties of Legendre polynomials, which are orthogonal for the scalar product

$$\langle f,g\rangle = \int_a^b f(x)g(x)\,dx,$$

imply that the corresponding quadrature rule computes exactly the integrals of polynomials of degree up to $2n - 1$, instead of only $n - 1$ as in the general case. Moreover, the corresponding integration weights are always positive, which minimises the effect of numerical issues like cancellation$^{1}$.

To conclude on interpolation methods, the Gauss-Kronrod method with $2n + 1$ points is an “extension” of the Gauss-Legendre method with $n$ points:

+   - $n$ of the $2n + 1$ points are the Gauss-Legendre integration points;

¹This phenomenon happens when a sum of real numbers is significantly smaller (in absolute value) than the summands: each rounding error might then be larger than the final result, which yields a total loss of accuracy. See also §11.3.3.