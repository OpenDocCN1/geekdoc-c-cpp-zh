![](bbox=[0.22, 0.12, 0.77, 0.34])

FIGURE 5.2 Plots of associated Legendre functions $P_3^0(x)$, $P_3^1(x)$, $P_3^2(x)$, and $P_3^3(x)$ as calculated by function aLegendre.

values for $m < 0$ can be simply obtained by applying property (5.42). For $l < m$, the function returns 0, as this amounts to differentiating the Legendre polynomial $P_l(x)$ a number $m$ of times which exceeds its degree $l$. For $m > 0$, the starting value $P_m^m(x)$ is calculated according to Equation 5.47 and stored in variable p, while for $l > m$, the recurrence relation (5.44) is applied for $i = m + 1, \dots, l$.

Figure 5.2 displays as examples the plots of the associated Legendre functions $P_3^0(x)$, $P_3^1(x)$, $P_3^2(x)$, and $P_3^3(x)$, obtained by using function aLegendre. Obviously, while increasing the upper index, the number of zeros reduces alongside with the reduction of the degree of the polynomial composing the associated Legendre function.

The real and imaginary parts of the spherical harmonics require the direct use of the associated Legendre functions and, for $m \ge 0$, we have

Re $Y_{lm}(\theta, \varphi) = \sqrt{\frac{2l + 1}{4\pi} \frac{(l - m)!}{(l + m)!}} P_l^m(\cos \theta) \cos m\varphi,$ (5.48)

Im $Y_{lm}(\theta, \varphi) = \sqrt{\frac{2l + 1}{4\pi} \frac{(l - m)!}{(l + m)!}} P_l^m(\cos \theta) \sin m\varphi.$ (5.49)

Function SpherY from Listing 5.7 implements these relations, using for output the parameters ReY and ImY. In calculating $(l + m)!/(l - m)!$, which occurs in the normalization factor, instead of evaluating factorials (which are time consuming if invoked often), only the distinct factors are multiplied:

$\frac{(l + m)!}{(l - m)!} = (l - m + 1)(l - m + 2)\cdots(l + m) = \prod_{i=l - m + 1}^{l + m} i.$