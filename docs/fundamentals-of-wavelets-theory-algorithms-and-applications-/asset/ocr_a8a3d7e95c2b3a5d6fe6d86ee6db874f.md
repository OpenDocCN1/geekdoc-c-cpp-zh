\(\chi_{[0,1)}(t) = \begin{cases} 1, & 0 \le t < 1; \\ 0 & \text{otherwise,} \end{cases}\)

is the characteristic function. The Haar basis clearly satisfies the orthogonality condition

\(\langle \phi_{H,j}(t), \phi_{H,k}(t) \rangle = \int_{-\infty}^{\infty} \chi_{[0,1)}(t-j) \overline{\chi_{[0,1)}(t-k)} dt = \delta_{j,k}.\)

To represent a global function \(f(t), t \in (-\infty, \infty)\) with a local basis \(\phi(t), t \in (a, b)\), functions that exist outside of the finite interval must be represented by integer shifts (delays) of the basis function along the real line. Integer shifts of global functions can also form bases for linear spaces. The Shannon function \(\phi_{SH}(t)\) is an example of such a basis.

# 2.4.2 Shannon Basis

The Shannon function is defined by

\(\phi_{SH}(t) = \frac{\sin \pi t}{\pi t},\)

and the basis is formed by

\(\phi_{SH,k}(t) = \frac{\sin \pi (t-k)}{\pi (t-k)}, \quad k \in \mathbb{Z}\)