# Normed Linear Spaces

(ii) For \(q \ge p \ge 1\), from (i), we have

\(\|A\|_p = \max_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_p} \le \max_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_q} \le \max_{x \neq 0} \frac{n^{\frac{q-p}{pq}} \|Ax\|_q}{\|x\|_q} = n^{\frac{q-p}{pq}} \|A\|_q,\)

\(\|A\|_p = \max_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_p} \ge \max_{x \neq 0} \frac{\|Ax\|_p}{\|x\|_q^{\frac{q-p}{pq}} \|x\|_p} \ge \max_{x \neq 0} \frac{\|Ax\|_q}{\|x\|_q^{\frac{q-p}{pq}} \|x\|_q} = n^{\frac{p-q}{pq}} \|A\|_q.\)

**17.8.** Since \(A^t A\) is real and symmetric, in view of P8 (in Chapter 16), eigenvalues of \(A^t A\) are real. If \(\lambda\) is an eigenvalue of \(A^t A\) and \(u\) is the corresponding eigenvector, then \(\|Au\|_2^2 = ((Au), (Au)) = (Au)^t(Au) = u^t(A^t A)u = u^t \lambda u = \lambda u^t u = \lambda \|u\|_2^2\), and hence \(\lambda\) is nonnegative.

**17.9.** Since \(\|A^{-1}B\| < 1\) from Theorem 17.5, it follows that the matrix \((I + A^{-1}B)\) is nonsingular. Now since \(A + B = A(I + A^{-1}B)\), the matrix \(A + B\) is nonsingular, and \((A + B)^{-1} - A^{-1} = (I + A^{-1}B)^{-1} A^{-1} - A^{-1} = [(I + A^{-1}B)^{-1} - I]A^{-1}\). Now use (17.12).

**17.10.** (i) If \(u \neq v\), then \(u - v \neq 0\). Hence \(d(u, v) = \|u - v\| > 0\). Further, \(d(u, u) = \|u - u\| = \|0\| = 0\).

(ii) \(d(u, v) = \|u - v\| = \|-1(v - u)\| = |-1|\|v - u\| = \|v - u\|\)

(iii) \(d(u, v) = \|u - v\| = \|(u - w) + (w - v)\| \le \|u - w\| + \|w - v\| = d(u, w) + d(w, v)\).

153