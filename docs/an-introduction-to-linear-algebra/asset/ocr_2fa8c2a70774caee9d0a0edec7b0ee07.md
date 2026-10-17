together with the initial conditions

\(D_{-1}=0,\quad D_0=1.\) (4.4)

The general solution of (4.3) can be written as

\(D_n=A\lambda_1^n+B\lambda_2^n,\) (4.5)

where \(\lambda_1,\lambda_2\) are the roots of the equation \(\lambda^2-x\lambda+1=0\). Using (4.4), it follows that

\(D_n=\left\{\begin{array}{ c c }
sinh(n+1)\theta/sinh\theta & \text{if}x=2cosh\theta>2 \\
n+1 & \text{if}x=2 \\
sin(n+1)\theta/sin\theta & \text{if}0\le x=2cos\theta<2.
\end{array}\right.\) (4.6)

Now let \(B_n=(b_{ij})\) be the inverse of \(A_n(x)\), i.e., \(A_n(x)B_n=I\). Then, for \(1\le j\le n\) it follows that

\(-b_{i-1,j}+xb_{ij}-b_{i+1,j}=\left\{\begin{array}{ c c }
0, & i=1,\cdots,j-1,b_{0j}=0 \\
1, & i=j \\
0, & i=j+1,\cdots,n,b_{n+1,j}=0.
\end{array}\right.\) (4.7)

Let \(x=2cosh\theta>2\). When \(1\le i\le j-1\), the general solution of (4.7) is \(b_{ij}=A\lambda_1^i+B\lambda_2^i\), where once again \(\lambda_1\), \(\lambda_2\) are the roots of the equation \(\lambda^2-x\lambda+1=0\). This solution is valid for \(0\le i\le j\), and in view of \(b_{0j}=0\) and (4.6) can be written as

\(b_{ij}=2Asinhi\theta=2AD_{i-1}sinh\theta,0\le i\le j.\) (4.8)

Similarly, when \(j+1\le i\le n\), the general solution of (4.7) is \(b_{ij}=C\lambda_1^i+D\lambda_2^i\), which is valid for \(j\le i\le n+1\). This solution in view of \(b_{n+1,j}=0\) and (4.6) appears as

\(b_{ij}=-2CD_{n-i}e^{(n+1)\theta}sinh\theta,j\le i\le n+1.\) (4.9)

Now equating (4.8) and (4.9) for \(i=j\), we obtain the equation

\(AD_{j-1}+Ce^{(n+1)\theta}D_{n-j}=0.\) (4.10)

Also, substituting (4.8) and (4.9) in (4.7) with \(i=j\), we get the equation

\(sinh\theta\left[AD_j+Ce^{(n+1)\theta}D_{n-j-1}\right]=\frac{1}{2}.\) (4.11)

Solving (4.10) and (4.11), we find

\(A=\frac{D_{n-j}}{2D_nsinh\theta},C=-\frac{D_{j-1}}{2D_ne^{(n+1)\theta}sinh\theta}.\) (4.12)