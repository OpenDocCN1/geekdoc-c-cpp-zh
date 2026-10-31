quadratic factor $1 - \alpha_{1j}z - \alpha_{2j}z^2$ is

$$f_{0j} = \frac{1}{2\pi}\cos^{-1}\left(\frac{a_{1j}}{2\sqrt{-a_{2j}}}\right).$$

Thus, an AR(p) model is fundamentally a combination of first and second-order components. Specifically, $\rho_k$ for an AR(p) process behaves as a mixture of damped exponentials and/or damped sinusoids. Each $j = 1, ..., m$ in Equation 3.76 corresponds to either a real root or a complex conjugate pair of roots. Without loss of generality, we let $j = 1, ..., m_r$ correspond to the real roots and $j = m_r + 1, ..., m$ to the pairs of complex conjugate roots. A useful reformulation of the general expression in Equation 3.49 for the autocorrelation of an AR(p) (with no repeated roots of the characteristic equation) can be rewritten as

$$\rho_k = \sum_{j=1}^{m_r} C_j (r_j^{-1})^k + \sum_{j=m_r+1}^{m} \left(C_{j1}(r_j^{-1})^k + C_{j2}(r_j^{*-1})^k\right) \tag{3.77}$$

$$= \sum_{j=1}^{m_r} C_j \alpha_j^k + \sum_{j=m_r+1}^{m} D_j (\sqrt{-\alpha_{2j}})^k \sin(2\pi f_{0j} k + \psi_j),$$

where

$$f_{0j} = \frac{1}{2\pi}\cos^{-1}\left(\frac{a_{1j}}{2\sqrt{-a_{2j}}}\right), \tag{3.78}$$

and where $C_j$, $j = 1, ..., m_r$ and $D_j$ and $\psi_j$, $j = m_r + 1, ..., m$ are real constants. Equation 3.77 shows that $\rho_k$ for an AR(p) process behaves like a mixture of damped exponentials and/or damped sinusoids. Thus, the factors of $\phi(z)$ determine the correlation structure of an AR(p) as well as the behavior of its realizations. The understanding of these factors is often critical to understanding the underlying physical phenomenon.

# EXAMPLE 3.10: AUTOCORRELATION FUNCTION FOR EXAMPLES 3.8 AND 3.9

Based on Equation 3.77, the autocorrelation function for the AR(3) model of Example 3.8 is

$$\rho_k = 0.66(0.95)^k + 0.3518(0.95)^k \sin(2\pi f_0 k + 1.31), \tag{3.79}$$