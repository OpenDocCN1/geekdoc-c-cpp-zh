$$f(t) = \sum_{k=-\infty}^{\infty} c_k \phi_k(t).$$ (2.16)

We compute the coefficients by taking the inner product of the function with the basis to yield

$$\begin{aligned} \langle f, \phi_k \rangle &= \int_{-\infty}^{\infty} f(t) \overline{\phi_k(t)} dt \\ &= \int_{-\infty}^{\infty} \sum_{l=-\infty}^{\infty} c_l \phi_l(t) \overline{\phi_k(t)} dt \\ &= \sum_{l=-\infty}^{\infty} c_l \delta_{l,k} \\ &= c_k. \end{aligned}$$ (2.17)

Computation of an inner product such as the one in (2.17) requires the knowledge of the function $f(t)$ for all $t$ and is not real-time computable.

We have seen that an orthonormal basis is an efficient and straightforward way to represent a signal. In some applications, however, the orthonormal basis function may lack certain desirable signal-processing properties, causing inconvenience in processing. Biorthogonal representation is a possible alternative to overcoming the constraint in orthogonality and producing a good approximation to a given function. Let $\{\phi_k(t)\}_{k \in \mathbb{Z}} \in L^2$ be a biorthogonal basis function set. If there exists another basis function set $\{\tilde{\phi}_k(t)\}_{k \in \mathbb{Z}} \in L^2$ such that