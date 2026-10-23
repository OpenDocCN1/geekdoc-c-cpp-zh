Assume that the given functions $f(t,x,y)$ and $g(t,y)$ are square-integrable and also integrable in absolute value with respect to the time variable $t$:
$$\int_{-\infty}^{\infty} |f(t,x,y)|^2 dt < \infty,$$
$$\int_{-\infty}^{\infty} |f(t,x,y)| dt < \infty,$$
$$\int_{-\infty}^{\infty} |g(t,y)|^2 dt < \infty,$$
$$\int_{-\infty}^{\infty} |g(t,y)| dt < \infty.$$

Then, these functions, as well as the solution $u(t,x,y)$, can be written in the Fourier form
$$f(t,x,y) = \int_{-\infty}^{\infty} \exp(i\omega t) f_{\omega}(x,y) d\omega,$$
$$g(t,y) = \int_{-\infty}^{\infty} \exp(i\omega t) g_{\omega}(y) d\omega,$$
$$u(t,x,y) = \int_{-\infty}^{\infty} \exp(i\omega t) u_{\omega}(x,y) d\omega,$$

where $f_{\omega}(x,y)$ and $g_{\omega}(y)$ are the given Fourier coefficients of the $\omega$-frequency in the Fourier expansion (with respect to the time variable $t$), and $u_{\omega}(x,y)$ is the unknown Fourier coefficient for the unknown solution $u(t,x,y)$. More specifically,
$$f_{\omega}(x,y) = \int_{-\infty}^{\infty} \exp(-i\omega t) f(t,x,y) dt,$$
$$g_{\omega}(y) = \int_{-\infty}^{\infty} \exp(-i\omega t) g(t,y) dt,$$
$$u_{\omega}(x,y) = \int_{-\infty}^{\infty} \exp(-i\omega t) u(t,x,y) dt.$$

In order to find $u_{\omega}(x,y)$, we restrict the wave equation and the associated boundary conditions to the $\omega$-frequency. More precisely, we multiply the original equation by $\exp(-i\omega t)$ and integrate over $-\infty < t < \infty$. By integration by parts, it then follows that taking the $t$-derivative of $u$ translates into multiplying $u_{\omega}$ by $i\omega$, leading to
$$-\omega^2 u_{\omega}(x,y) - c^2 \left( u_{\omega}(x,y)_{xx} + u_{\omega}(x,y)_{yy} \right) = f_{\omega}(x,y),$$
with the boundary conditions
$$u_{\omega}(0,y) = g_{\omega}(y)$$
on the left edge of the square;
$$u_{\omega}(x,0)_y = u_{\omega}(x,1)_y = 0$$
on the top and bottom edges; and
$$u_{\omega}(1,y)_x + i \frac{\omega}{c} u_{\omega}(1,y) = 0$$
on the right edge, at which the wave exits the square.