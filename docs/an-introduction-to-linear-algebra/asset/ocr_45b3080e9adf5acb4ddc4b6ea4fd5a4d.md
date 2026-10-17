# Answers or Hints

+   2.1. \(U=\begin{pmatrix}0&3&5\\0&0&7\\0&0&0\end{pmatrix},\quad L=\begin{pmatrix}1&0&0\\2&4&0\\6&-5&9\end{pmatrix}.\)

+   2.2. \(AB=C=(c_{ij})\), \(c_{ij}=0\) if \(i>j\) and \(c_{ij}=\sum_{k=i}^{j}a_{ik}b_{kj}\) if \(j\ge i\).

+   2.3. Direct computation.

+   2.4. Direct computation.

+   2.5. Direct computation.

+   2.6. \((A+B)^2=(A+B)(A+B)=A^2+AB+BA+B^2.\)

+   2.7. Consider \(A=\begin{pmatrix}1&1\\1&1\end{pmatrix}\). Then \(1\cdot A=\begin{pmatrix}1&0\\0&1\end{pmatrix}\ne A\). Hence, B10 is violated.

+   2.8. \(\begin{pmatrix}a&b\\c&d\end{pmatrix}=\begin{pmatrix}a&0\\0&0\end{pmatrix}+\begin{pmatrix}0&b\\0&0\end{pmatrix}+\begin{pmatrix}0&0\\c&0\end{pmatrix}+\begin{pmatrix}0&0\\0&d\end{pmatrix}.\)

+   2.9. Let \(C,D\in S\) and \(\alpha,\beta\in R\). Then, \((\alpha C+\beta D)B=\alpha CB+\beta DB=\alpha BC+\beta BD=B(\alpha C+\beta D)\).

+   2.10. Use the principal of mathematical induction.

+   2.11. Let \(A=(a_{ij})_{m\times n}\), \(B=(b_{ij})_{n\times p}\), \(C=(c_{ij})_{p\times r}\), then \(BC\) and \(AB\) are \(n\times r\) and \(m\times p\) matrices, and the \(ij\)-th element of \(A(BC)\) is
+   
+   \[\sum_{\mu=1}^{n}a_{i\mu}\left(\sum_{\nu=1}^{p}b_{\mu\nu}c_{\nu j}\right)=\sum_{\mu=1}^{n}\sum_{\nu=1}^{p}a_{i\mu}b_{\mu\nu}c_{\nu j}.\]
+   
+   and similarly, the \(ij\)-th element of \((AB)C\) is
+   
+   \[\sum_{\nu=1}^{p}\left(\sum_{\mu=1}^{n}a_{i\mu}b_{\mu\nu}\right)c_{\nu j}=\sum_{\nu=1}^{p}\sum_{\mu=1}^{n}a_{i\mu}b_{\mu\nu}c_{\nu j}.\]

+   2.12. Similar to Problem 2.11.

+   2.13. (iv) \((AB)^H_{ij}=\left(\sum_{k=1}^{n}a_{ik}b_{kj}\right)^H_{ij}=\left(\sum_{k=1}^{n}\overline{a_{ik}b_{kj}}\right)_{ji}=\left(\sum_{k=1}^{n}\overline{a_{ik}}\,\overline{b_{kj}}\right)_{ji}=(\overline{AB})^t_{ij}=(\overline{B}^{\,t}\overline{A}^{\,t})_{ij}=(B^H A^H)_{ij}.\)

+   2.14. Hermitian: \(\begin{pmatrix}1&i&2-i\\-i&2&5\\2+i&5&3\end{pmatrix}\)
+   
+   Skew-hermitian: \(\begin{pmatrix}i&i&2+i\\i&2i&5\\-2+i&-5&5i\end{pmatrix}\)
+   
+   Normal: \(\begin{pmatrix}-i&-2-i\\2-i&-3i\end{pmatrix}\).

+   2.15. (i) Let \(AB\) be hermitian. Then, \(AB=(AB)^H=B^HA^H=BA\), i.e., \(A,B\) commute. Conversely, let \(A,B\) commute. Then, \(AB=BA=B^HA^H=(AB)^H\), i.e., \(AB\) is hermitian.