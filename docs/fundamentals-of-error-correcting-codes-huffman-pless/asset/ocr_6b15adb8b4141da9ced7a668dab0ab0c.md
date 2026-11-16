**Example 5.4.5** Let $\mathcal{C}$ be the binary $[15, 5]$ narrow-sense BCH code of designed distance $\delta = 7$, which has defining set $T = \{1, 2, 3, 4, 5, 6, 8, 9, 10, 12\}$. Using the primitive 15th root of unity $\alpha$ in Table 5.1, the generator polynomial of $\mathcal{C}$ is
\(g(x) = 1 + x + x^2 + x^4 + x^5 + x^8 + x^{10}.\)

Suppose that using $\mathcal{C}$, \(y(x) = x + x^3 + x^5 + x^7 + x^9 + x^{12}\) is received. Step I produces \(S_1 = \alpha^4, S_2 = \alpha^{13}, S_3 = \alpha^{14}, S_4 = \alpha^{11}, S_5 = 1\), and \(S_6 = \alpha^{13}\). The matrix $M_2$ is singular, and we have

\(M_2 = \begin{bmatrix} S_1 & S_2 \\ S_2 & S_3 \end{bmatrix} = \begin{bmatrix} \alpha^{14} & \alpha^{13} \\ \alpha^{13} & \alpha^{14} \end{bmatrix} \text{ and } M_2^{-1} = \begin{bmatrix} \alpha^{10} & \alpha^9 \\ \alpha^9 & \alpha^{10} \end{bmatrix}.\)

Then \([\sigma_1 \ \sigma_2]^T = M_2^{-1} [\alpha^{11} \ \alpha^{11}]^T = [\alpha^6 \ \alpha^{11}]^T\). Thus Step II produces the error locator polynomial \(\sigma(x) = 1 + \alpha^6 x + \alpha^9 x^2\). Step III yields the roots $\alpha^2$ and $\alpha^4$ of $\sigma(x)$ and hence the error location numbers $X_1 = \alpha^{10}$ and $X_2 = \alpha^{11}$. Skipping Step IV, the error vector is \(e(x) = x^{10} + x^{11}\), and the transmitted codeword is \(c(x) = x + x^4 + x^5 + x^7 + x^9 + x^{10} + x^{11} + x^{12}\), which is $(x + x^2)g(x)$.

**Example 5.4.6** Let $\mathcal{C}$ be the $[15, 9]$ narrow-sense RS code over $\mathbb{F}_{16}$ of designed distance $\delta = 7$, which has defining set $T = \{1, 2, 3, 4, 5, 6\}$. Using the primitive 15th root of unity $\alpha$ in Table 5.1, the generator polynomial of $\mathcal{C}$ is
\(g(x) = (\alpha + x)(\alpha^2 + x) \cdots (\alpha^6 + x) = \alpha^6 + \alpha^8 x + \alpha^5 x^2 + \alpha^4 x^3 + \alpha^4 x^4 + \alpha^{10} x^5 + x^6.\)

Suppose that a codeword of $\mathcal{C}$ is received as \(y(x) = \alpha^7 + \alpha^{10} x^2 + x^3 + \alpha^4 x^4 + \alpha^5 x^5 + \alpha^6 x^6 + \alpha^4 x^7 + \alpha^7 x^{11}\).

Step I produces \(S_1 = \alpha^5, S_2 = \alpha^7, S_3 = \alpha^{10}, S_4 = \alpha^2, S_5 = \alpha^7\), and \(S_6 = \alpha^2\). The matrix $M_3$ is nonsingular and we have to solve

\(\begin{bmatrix} S_1 & S_2 & S_3 \\ S_2 & S_3 & S_4 \\ S_3 & S_4 & S_5 \end{bmatrix} \begin{bmatrix} \sigma_3 \\ \sigma_2 \\ \sigma_1 \end{bmatrix} = \begin{bmatrix} -S_4 \\ -S_5 \\ -S_6 \end{bmatrix} \text{ or } \begin{bmatrix} \alpha^5 & \alpha^7 & \alpha^{10} \\ \alpha^7 & \alpha^{10} & \alpha^2 \\ \alpha^{10} & \alpha^2 & \alpha^7 \end{bmatrix} \begin{bmatrix} \sigma_3 \\ \sigma_2 \\ \sigma_1 \end{bmatrix} = \begin{bmatrix} \alpha^7 \\ \alpha^2 \\ \alpha^3 \end{bmatrix}.\)

The solution is \(\sigma_1 = \alpha^5, \sigma_2 = \alpha^6\), and \(\sigma_3 = \alpha^4\). Thus Step II produces the error locator polynomial \(\sigma(x) = 1 + \alpha^5 x + \alpha^6 x^2 + \alpha^4 x^3\). Step III yields the roots $\alpha^{13}, \alpha^9$, and $\alpha^4$ of $\sigma(x)$ and hence the error location numbers $X_1 = \alpha^2, X_2 = \alpha^6$, and $X_3 = \alpha^{11}$. For Step IV, solve the first three equations of (5.8) or

\(\alpha^5 = E_1 \alpha^2 + E_2 \alpha^6 + E_3 \alpha^{11},\)
\(\alpha^7 = E_1 \alpha^4 + E_2 \alpha^{12} + E_3 \alpha^7,\)
\(\alpha^{10} = E_1 \alpha^6 + E_2 \alpha^2 + E_3 \alpha^3.\)

The solution is $E_1 = 1, E_2 = \alpha^4$, and $E_3 = \alpha^7$. Thus the error vector is \(e(x) = x^2 + \alpha^3 x^6 + \alpha^7 x^{11}\), and the transmitted codeword is \(c(x) = \alpha^7 + \alpha^3 x^2 + x^3 + \alpha^2 x^4 + \alpha^4 x^5 + \alpha^7 x^6 + \alpha^4 x^7\), which is $(\alpha + \alpha^4 x)g(x)$.