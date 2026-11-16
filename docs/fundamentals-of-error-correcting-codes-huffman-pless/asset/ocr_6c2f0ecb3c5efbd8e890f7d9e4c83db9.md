| Binary | Power | Binary | Power | Binary | Power | Binary | Power |
|---|---|---|---|---|---|---|---|
| 0000 | 0 | 1000 | \(\alpha^3\) | 1011 | \(\alpha^7\) | 1110 | \(\alpha^{11}\) |
| 0001 | 1 | 0011 | \(\alpha^4\) | 0101 | \(\alpha^8\) | 1111 | \(\alpha^{12}\) |
| 0010 | \(\alpha\) | 0110 | \(\alpha^5\) | 1010 | \(\alpha^9\) | 1101 | \(\alpha^{13}\) |
| 0100 | \(\alpha^2\) | 1100 | \(\alpha^6\) | 0111 | \(\alpha^{10}\) | 1001 | \(\alpha^{14}\) |

Example 5.4.3 Let C be the [15, 7] narrow-sense binary BCH code of designed distance \(\delta = 5\), which has defining set \(T = \{1, 2, 3, 4, 6, 8, 9, 12\}\). Using the primitive 15th root of unity \(\alpha\) from Table 5.1, the generator polynomial of C is \(g(x) = 1 + x^4 + x^6 + x^7 + x^8\).

Suppose that C is used to transmit a codeword and \(y(x) = 1 + x + x^5 + x^6 + x^9 + x^{10}\) is received. Using Table 5.1 and Theorem 5.4.1, Step 1 produces \(S_1 = 1 + \alpha + \alpha^5 + \alpha^6 + \alpha^9 + \alpha^{10} = \alpha^2\), \(S_2 = S_1^2 = \alpha^4\), \(S_3 = 1 + \alpha^3 + \alpha^{15} + \alpha^{18} + \alpha^{27} + \alpha^{30} = \alpha^{10}\), \(S_4 = S_2^2 = \alpha^8\).

For Step II, we note that \(M_2 = \begin{bmatrix} S_1 & S_2 \\ S_2 & S_3 \end{bmatrix} = \begin{bmatrix} \alpha^2 & \alpha^4 \\ \alpha^4 & \alpha^{11} \end{bmatrix}\) is nonsingular with inverse \(M_2^{-1} = \begin{bmatrix} \alpha^8 & \alpha \\ \alpha & \alpha^{14} \end{bmatrix}\).

Thus \(v = 2\) errors have been made, and we must solve \(\begin{bmatrix} S_1 & S_2 \\ S_2 & S_3 \end{bmatrix} \begin{bmatrix} \sigma_2 \\ \sigma_1 \end{bmatrix} = \begin{bmatrix} -S_3 \\ -S_4 \end{bmatrix}\) or \(\begin{bmatrix} \alpha^2 & \alpha^4 \\ \alpha^4 & \alpha^{11} \end{bmatrix} \begin{bmatrix} \sigma_2 \\ \sigma_1 \end{bmatrix} = \begin{bmatrix} \alpha^{11} \\ \alpha^{11} \end{bmatrix}\).

The solution is \([\sigma_2 \quad \sigma_1]^T = M_2^{-1} [\alpha^{11} \quad \alpha^{11}]^T = [\alpha^{14} \quad \alpha^2]^T\). Thus Step II produces the error locator polynomial \(\sigma(x) = 1 + \alpha^2 x + \alpha^{14} x^2\). Step III yields the roots \(\alpha^{11}\) and \(\alpha^5\) of \(\sigma(x)\) and hence the error location numbers \(X_1 = \alpha^4\) and \(X_2 = \alpha^{10}\). As the code is binary, we skip Step IV. So the error vector is \(e(x) = x^4 + x^{10}\), and the transmitted codeword is \(c(x) = 1 + x + x^4 + x^5 + x^6 + x^9\), which is \((1+x)g(x)\).

Example 5.4.4 Let C be the code of Example 5.4.3. Suppose that \(y(x) = 1 + x^2 + x^8\) is received. Then Step I produces \(S_1 = S_2 = S_3 = S_4 = 0\) and \(S_5 = \alpha^{10}\). In Step II, the matrix \(M_2 = \begin{bmatrix} S_1 & S_2 \\ S_2 & S_3 \end{bmatrix} = \begin{bmatrix} 0 & 0 \\ 0 & \alpha^{10} \end{bmatrix}\) is singular, as is \(M_1 = [S_1] = [0]\). Since the syndromes are not all 0 and we cannot complete the algorithm, we must conclude that more than two errors were made.