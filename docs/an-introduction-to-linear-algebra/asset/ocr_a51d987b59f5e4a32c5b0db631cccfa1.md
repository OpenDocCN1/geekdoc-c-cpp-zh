\(R_3+8R_2\)

\(U=\left(\begin{array}{ c c c c }
3 & 2 & 3 & 1 \\
0 & -1 & 1 & 2 \\
0 & 0 & 16 & 19
\end{array}\right), L=\left(\begin{array}{ c c c }
1 & 0 & 0 \\
1 & 1 & 0 \\
-2 & -8 & 1
\end{array}\right).\)

# Example 7.2. Successively, we have

\(A=\left(\begin{array}{ c c c }
2 & 1 & 3 \\
4 & 3 & 5 \\
8 & 2 & 16 \\
-4 & 1 & -11 \\
-2 & 3 & -5
\end{array}\right), L=\left(\begin{array}{ c c c c c }
1 & 0 & 0 & 0 & 0 \\
\bullet & 1 & 0 & 0 & 0 \\
\bullet & \bullet & 1 & 0 & 0 \\
\bullet & \bullet & \bullet & 1 & 0 \\
\bullet & \bullet & \bullet & \bullet & 1
\end{array}\right)\)

\(R_2-2R_1, R_3-4R_1, R_4+2R_1, R_5+R_1\)

\(A\sim\left(\begin{array}{ c c c }
2 & 1 & 3 \\
0 & 1 & -1 \\
0 & -2 & 4 \\
0 & 3 & -5 \\
0 & 4 & -2
\end{array}\right), L=\left(\begin{array}{ c c c c c }
1 & 0 & 0 & 0 & 0 \\
2 & 1 & 0 & 0 & 0 \\
4 & \bullet & 1 & 0 & 0 \\
-2 & \bullet & \bullet & 1 & 0 \\
-1 & \bullet & \bullet & \bullet & 1
\end{array}\right)\)

\(R_3+2R_2, R_4-3R_2, R_5-4R_2\)

\(A\sim\left(\begin{array}{ c c c }
2 & 1 & 3 \\
0 & 1 & -1 \\
0 & 0 & 2 \\
0 & 0 & -2 \\
0 & 0 & 2
\end{array}\right), L=\left(\begin{array}{ c c c c c }
1 & 0 & 0 & 0 & 0 \\
2 & 1 & 0 & 0 & 0 \\
4 & -2 & 1 & 0 & 0 \\
-2 & 3 & \bullet & 1 & 0 \\
-1 & 4 & \bullet & \bullet & 1
\end{array}\right)\)

\(R_4+R_3, R_5-R_3\)

\(U=\left(\begin{array}{ c c c }
2 & 1 & 3 \\
0 & 1 & -1 \\
0 & 0 & 2 \\
0 & 0 & 0 \\
0 & 0 & 0
\end{array}\right), L=\left(\begin{array}{ c c c c c }
1 & 0 & 0 & 0 & 0 \\
2 & 1 & 0 & 0 & 0 \\
4 & -2 & 1 & 0 & 0 \\
-2 & 3 & -1 & 1 & 0 \\
-1 & 4 & 1 & \bullet & 1
\end{array}\right).\)

In _L_ the remaining \(\bullet\) is finally replaced by 0.

# Remark 7.1 (\(LD\hat{U}\) factorization). From the matrix _U_ in Theorem 7.1, we can factor out an \(m\times m\) diagonal matrix _D_ so that \(U=D\hat{U}\), where the nonzero elements in _U_ and \(\hat{U}\) are at the same position; however, in \(\hat{U}\) all pivot elements are 1. Clearly, with such an adjustment \(A=LD\hat{U}\).

# Example 7.3. For the matrix in Example 4.2, we have

\(A=\left(\begin{array}{ c c c }
2 & -1 & 1 \\
3 & 2 & -5 \\
1 & 3 & -2
\end{array}\right)=\left(\begin{array}{ c c c }
1 & 0 & 0 \\
\frac{3}{2} & 1 & 0 \\
\frac{1}{2} & 1 & 1
\end{array}\right)\left(\begin{array}{ c c c }
2 & -1 & 1 \\
0 & \frac{7}{2} & -\frac{13}{2} \\
0 & 0 & \frac{1}{4}
\end{array}\right)\)