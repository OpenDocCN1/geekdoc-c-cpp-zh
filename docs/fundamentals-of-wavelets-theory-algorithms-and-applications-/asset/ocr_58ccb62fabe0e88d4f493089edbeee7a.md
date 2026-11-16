$G_0(z) = \left(\frac{1+z}{2}\right)^m S(z),$ (6.57)

where $S(z) \in \pi_{m-1}$. So our objective is to find $S(z)$. First, observe that since $G_0(1) = 1$, we must have $S(1) = 1$. Furthermore, we also want $S(-1) \neq 0$ because if $S(-1) = 0$, then $z+1$ is a factor of $S(z)$ and hence can be taken out. Now $G_0(z)$ is given by (6.57) must satisfy the orthogonality condition, namely

$|G_0(z)|^2 + |G_0(-z)|^2 = 1, \quad z = e^{-j\omega/2}$ (6.58) $$\Rightarrow \cos^{2m}(\frac{\omega}{4})|S(z)|^2 + \sin^{2m}(\frac{\omega}{4})|S(-z)|^2 = 1.$$ (6.59)

By defining

$x := \sin^2\left(\frac{\omega}{4}\right), \text{ and }$

$f(x) := |S(z)|^2,$

Equation (6.59) can be rewritten as

$$(1-x)^m f(x) + x^m f(1-x) = 1$$ $$\Rightarrow f(x) = (1-x)^m \{1 - x^m f(1-x)\}$$ $$= \sum_{k=0}^{m-1} \binom{m+k-1}{k} x^k + R_m(x),$$ (6.60)