On comparing the coefficients of \(\tilde{w}^k\) in (13.11) and (13.12), we get

\(\sum_{s=1}^m q_{ks}a_{sj}=\sum_{s=1}^n b_{ks}p_{sj},j=1,\cdots,n,k=1,\cdots,m.\) (13.13)

Thus, if \(Q=(q_{ks})_{m\times m}\), \(A=(a_{sj})_{m\times n}\), \(B=(b_{ks})_{m\times n}\), \(P=(p_{sj})_{n\times n}\) are the matrices, then (13.13) is the same as

\(QA=BP,\)

and since \(P\) is invertible, we have the required relation

\(B=QAP^{-1}.\) (13.14)

In the special case when \(V=W\), and \(S=T=\{u^1,\cdots,u^n\}\), \(\tilde{S}=\tilde{T}=\{\tilde{u}^1,\cdots,\tilde{u}^n\}\), we have \(P=Q\), and then the relation (13.14) reduces to

\(B=PAP^{-1},\) (13.15)

which is the same as

\(A=P^{-1}BP.\) (13.16)

**Example 13.3.** In addition to \(L\), \(S\), \(T\) given in Example 13.2, let \(\tilde{S}=\{(1,0,0)^t,(0,1,0)^t,(0,0,1)^t\}\) and \(\tilde{T}=\{(1,0)^t,(0,1)^t\}\). Then, we have

\(A=\left(\begin{array}{ c c c }
\frac{1}{3} & -\frac{2}{3} & \frac{1}{3} \\
\frac{1}{3} & \frac{4}{3} & \frac{1}{3}
\end{array}\right),B=\left(\begin{array}{ c c c }
1 & 1 & -1 \\
1 & -1 & 1
\end{array}\right),Q=\left(\begin{array}{ c c }
1 & 2 \\
2 & 1
\end{array}\right)\)

\(P=\left(\begin{array}{ c c c }
1 & 1 & 1 \\
1 & 1 & 0 \\
1 & 0 & 0
\end{array}\right),P^{-1}=\left(\begin{array}{ c c c }
0 & 0 & 1 \\
0 & 1 & -1 \\
1 & -1 & 0
\end{array}\right).\)

For these matrices relation (13.14) follows immediately.

**Example 13.4.** Let \(L:R^2\rightarrow R^2\) be the linear mapping defined by \(L(x,y)=(2x+y,x+2y)^t\), and let \(S=\{(1,1)^t,(1,0)^t\}\) and \(\tilde{S}=\{(0,1)^t,(1,1)^t\}\). Since

\(\begin{array}{ c c c }
L(1,1) & = & (3,3)^t=3(1,1)^t+0(1,0)^t \\
L(1,0) & = & (2,1)^t=1(1,1)^t+1(1,0)^t \\
L(0,1) & = & (1,2)^t=1(0,1)^t+1(1,1)^t \\
L(1,1) & = & (3,3)^t=0(0,1)^t+3(1,1)^t \\
(1,1)^t & = & 0(0,1)^t+1(1,1)^t \\
(1,0)^t & = & -1(0,1)^t+1(1,1)^t,
\end{array}\)

we have

\(A=\left(\begin{array}{ c c }
3 & 1 \\
0 & 1
\end{array}\right),B=\left(\begin{array}{ c c }
1 & 0 \\
1 & 3
\end{array}\right),P=\left(\begin{array}{ c c }
0 & -1 \\
1 & 1
\end{array}\right),P^{-1}=\left(\begin{array}{ c c }
1 & 1 \\
-1 & 0
\end{array}\right).\)